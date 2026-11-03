# SPEC.md: Spesifikasi Teknis Kalkulator Subnet & VLSM

## 1. Tujuan

Dokumen ini mendefinisikan spesifikasi teknis dan aturan bisnis untuk aplikasi web Kalkulator Subnetting & VLSM berbasis Python 3.12, FastAPI, dan HTML/JS sederhana. Spesifikasi ini bertujuan untuk memastikan presisi tinggi dalam kalkulasi IPv4 (termasuk kasus khusus RFC 3021 untuk `/31` dan host tunggal untuk `/32`), validasi input yang ketat, serta konsistensi penanganan error yang siap diuji menggunakan `pytest`.

---

## 2. Aturan Validasi Input

### 2.1 Standard Alamat IPv4

Alamat IPv4 dinyatakan valid jika dan hanya jika memenuhi semua syarat berikut:

1. **Format String**: Menggunakan notasi desimal bertitik (*dotted-decimal*) dengan tepat **4 oktet** yang dipisahkan oleh karakter titik (`.`).
2. **Rentang Nilai**: Setiap oktet harus berupa bilangan bulat dalam rentang `0` hingga `255` (inklusif).
3. **Strict No Leading Zeros**: Oktet dengan lebih dari satu digit tidak boleh diawali dengan angka nol (`0`).
* Valid: `192.168.0.1`, `10.0.0.1`
* Tidak Valid: `192.168.01.1` (ditolak untuk menghindari ambiguitas notasi oktal), `192.168.001.1`


4. **Tanpa Whitespace**: String tidak boleh mengandung karakter spasi di awal, tengah, maupun akhir.
5. **Karakter Non-Numerik**: String yang mengandung huruf atau simbol khusus selain titik (`.`) dinyatakan tidak valid.

### 2.2 Standard Prefix Subnet

Prefix subnet dinyatakan valid jika dan hanya jika:

1. **Tipe Data**: Berupa bilangan bulat (*integer*).
2. **Rentang Nilai**: Berada pada rentang `0` hingga `32` (inklusif).

---

## 3. Kontrak Fungsi (Python Core Logic)

### 3.1 Fungsi `hitung_subnet`

Menerima satu alamat IP dan prefix, lalu mengembalikan dictionary berisi informasi kalkulasi subnet.

* **Signature**:
```python
def hitung_subnet(ip: str, prefix: int) -> dict

```


* **Struktur Return Value (`dict`)**:
```python
{
    "mask": str,           # contoh: "255.255.255.128"
    "network": str,        # hasil bitwise AND (IP, mask)
    "broadcast": str | None, # str IPv4, atau None untuk /31 dan /32
    "first_host": str,     # IP host pertama yang valid
    "last_host": str,      # IP host terakhir yang valid
    "usable_hosts": int    # jumlah total host yang usable
}

```


* **Aturan Kalkulasi Bitwise & Edge Cases**:
* **Kalkulasi General (`/0` sampai `/30`)**:
* `network` = `IP` AND `subnet_mask` (dihitung secara bitwise).
* `broadcast` = `network` OR (NOT `subnet_mask`).
* `first_host` = `network` + 1.
* `last_host` = `broadcast` - 1.
* `usable_hosts` = $2^{(32 - \text{prefix})} - 2$.


* **Aturan Special `/31` (Point-to-Point per RFC 3021)**:
* `usable_hosts` = `2`.
* `broadcast` = `None`.
* `first_host` = `network` (misal: `.0`).
* `last_host` = `broadcast_address_standar` (misal: `.1`).


* **Aturan Special `/32` (Single Host / Loopback)**:
* `usable_hosts` = `1`.
* `broadcast` = `None`.
* `first_host` = `IP`.
* `last_host` = `IP`.


* **Penanganan Error**:
* Meng-`raise ValueError` dengan pesan eksplisit jika format IP atau prefix melanggar aturan pada **Bagian 2**.





---

### 3.2 Fungsi `alokasi_vlsm`

Menerima CIDR network utama dan daftar kebutuhan host tiap subnet, lalu mengalokasikan subnet secara berurutan berdasarkan efisiensi VLSM.

* **Signature**:
```python
def alokasi_vlsm(network_cidr: str, kebutuhan_host: list[int]) -> list[dict]

```


* **Aturan Kalkulasi VLSM**:
1. **Pengurutan Kebutuhan**: Kebutuhan host wajib diurutkan dari yang **terbesar ke terkecil** sebelum alokasi dilakukan.
2. **Penentuan Ukuran Blok**:
* Cari nilai $2^n \ge (\text{kebutuhan} + 2)$.
* Hitung prefix = $32 - n$.
* Prefix terkecil yang diizinkan dalam alokasi VLSM ini adalah `/30` (ukuran blok minimal 4 IP).


3. **Proses Alokasi**:
* Alokasi pertama dimulai tepat pada alamat `network` dari `network_cidr`.
* Subnet berikutnya dimulai pada alamat IP setelah `broadcast` dari subnet sebelumnya.


4. **Struktur Item Return Value (`list[dict]`)**:
Tiap elemen list mengembalikan dictionary:
```python
{
    "kebutuhan": int,        # jumlah host yang diminta
    "network_cidr": str,     # hasil alokasi CIDR, misal: "192.168.1.0/25"
    "mask": str,
    "network": str,
    "broadcast": str | None,
    "first_host": str,
    "last_host": str,
    "usable_hosts": int
}

```




* **Penanganan Error**:
Meng-`raise ValueError` apabila:
* `network_cidr` bukan format IPv4 CIDR valid (misal: `192.168.1.0/24`) atau IP yang dimasukkan bukan alamat awal network-nya.
* `kebutuhan_host` berupa list kosong (`[]`).
* `kebutuhan_host` berisi elemen bernilai $< 1$ (nol, negatif, atau non-integer).
* Total alokasi blok IP melebihi batas kapasitas `network_cidr` yang diberikan (*overcapacity*).



---

## 4. Kontrak API (FastAPI Endpoint)

### 4.1 `GET /api/subnet`

Menghitung informasi subnetting berdasarkan query parameter IP dan Prefix.

* **Query Parameters**:
* `ip` (string, required): Alamat IPv4.
* `prefix` (integer, required): Prefix subnet (`0-32`).


* **Response Status**:
* `200 OK`: Kalkulasi berhasil.
* `400 Bad Request`: Format input tidak valid.


* **Contoh Response `200 OK**`:
```json
{
  "mask": "255.255.255.128",
  "network": "172.16.5.128",
  "broadcast": "172.16.5.255",
  "first_host": "172.16.5.129",
  "last_host": "172.16.5.254",
  "usable_hosts": 126
}

```


* **Contoh Response `400 Bad Request**`:
```json
{
  "detail": "Format IP tidak valid: 192.168.01.1 mengandung leading zero."
}

```



---

### 4.2 `POST /api/vlsm`

Mengalkulasikan pembagian subnet VLSM berdasarkan network utama dan kebutuhan host.

* **Request Body (JSON)**:
```json
{
  "network": "192.168.1.0/24",
  "kebutuhan_host": [100, 50, 20, 2]
}

```


* **Response Status**:
* `200 OK`: Kalkulasi VLSM berhasil.
* `400 Bad Request`: Validasi gagal / kapasitas network tidak cukup.


* **Contoh Response `200 OK**`:
```json
[
  {
    "kebutuhan": 100,
    "network_cidr": "192.168.1.0/25",
    "mask": "255.255.255.128",
    "network": "192.168.1.0",
    "broadcast": "192.168.1.127",
    "first_host": "192.168.1.1",
    "last_host": "192.168.1.126",
    "usable_hosts": 126
  },
  {
    "kebutuhan": 50,
    "network_cidr": "192.168.1.128/26",
    "mask": "255.255.255.192",
    "network": "192.168.1.128",
    "broadcast": "192.168.1.191",
    "first_host": "192.168.1.129",
    "last_host": "192.168.1.190",
    "usable_hosts": 62
  }
]

```


* **Contoh Response `400 Bad Request**`:
```json
{
  "detail": "Kapasitas network 192.168.1.0/24 tidak cukup untuk menampung total kebutuhan host."
}

```



---

### 4.3 `GET /`

Menyajikan halaman antarmuka web tunggal (`index.html`).

* **Response Status**: `200 OK` (`text/html`)

---

## 5. Halaman Web (Frontend Contract)

Aplikasi dibangun sebagai *Single Page Application* (SPA) menggunakan satu file `index.html` statis:

1. **Navigasi Mode**: Menyediakan tab atau toggle untuk beralih antara Mode **Subnetting** dan Mode **VLSM**.
2. **Form Input Subnetting**:
* Input Field IP Address & Input Field Prefix.
* Tombol "Hitung Subnet".


3. **Form Input VLSM**:
* Input Field Network CIDR (misal: `192.168.1.0/24`).
* Dynamic Input Field / Textarea untuk memasukkan daftar kebutuhan host (misal dipisahkan koma: `100, 50, 20, 2`).
* Tombol "Hitung VLSM".


4. **Visualisasi Output**:
* Hasil kalkulasi ditampilkan dalam bentuk tabel yang mudah dibaca oleh guru/siswa tanpa perlu membaca source code.


5. **Penanganan Error Visual**:
* Jika API mengembalikan status `400 Bad Request`, UI akan menampilkan kotak peringatan (*alert box*) berwarna merah yang memuat isi pesan dari field `"detail"`.



---

## 6. Tabel Test Case (`test_main.py`)

Seluruh kasus uji di bawah ini wajib diimplementasikan menggunakan kerangka kerja `pytest`.

| No | Modul / Feature | Input Test Case | Ekspektasi Hasil / Detail Assertion | Status / Tipe |
| --- | --- | --- | --- | --- |
| 1 | Subnet Calc | IP: `172.16.5.130`<br>

<br>Prefix: `25` | `network`: `"172.16.5.128"`<br>

<br>`broadcast`: `"172.16.5.255"`<br>

<br>`usable_hosts`: `126`<br>

<br>`first_host`: `"172.16.5.129"`<br>

<br>`last_host`: `"172.16.5.254"` | **Pasti (Valid)** |
| 2 | Subnet Calc | IP: `10.0.0.0`<br>

<br>Prefix: `30` | `network`: `"10.0.0.0"`<br>

<br>`broadcast`: `"10.0.0.3"`<br>

<br>`usable_hosts`: `2`<br>

<br>`first_host`: `"10.0.0.1"`<br>

<br>`last_host`: `"10.0.0.2"` | **Pasti (Valid)** |
| 3 | Subnet Calc (/31) | IP: `192.168.1.0`<br>

<br>Prefix: `31` | `network`: `"192.168.1.0"`<br>

<br>`broadcast`: `None`<br>

<br>`usable_hosts`: `2`<br>

<br>`first_host`: `"192.168.1.0"`<br>

<br>`last_host`: `"192.168.1.1"` | **Pasti (RFC 3021)** |
| 4 | Subnet Calc (/32) | IP: `192.168.1.5`<br>

<br>Prefix: `32` | `network`: `"192.168.1.5"`<br>

<br>`broadcast`: `None`<br>

<br>`usable_hosts`: `1`<br>

<br>`first_host`: `"192.168.1.5"`<br>

<br>`last_host`: `"192.168.1.5"` | **Pasti (Single Host)** |
| 5 | Validation IP | IP: `256.1.1.1`, Prefix: `24` | Raise `ValueError` / HTTP 400 (`detail` memuat pesan error oktet > 255) | **Pasti (Ditolak)** |
| 6 | Validation IP | IP: `192.168.01.1`, Prefix: `24` | Raise `ValueError` / HTTP 400 (`detail` memuat pesan error leading zero) | **Pasti (Ditolak)** |
| 7 | Validation IP | IP: `192.168.1`, Prefix: `24` | Raise `ValueError` / HTTP 400 (`detail` memuat pesan error jumlah oktet kurang) | **Pasti (Ditolak)** |
| 8 | Validation IP | IP: `abc`, Prefix: `24` | Raise `ValueError` / HTTP 400 (`detail` memuat pesan error non-numeric) | **Pasti (Ditolak)** |
| 9 | Validation IP | IP: `""` (kosong), Prefix: `24` | Raise `ValueError` / HTTP 400 (`detail` memuat pesan error input kosong) | **Pasti (Ditolak)** |
| 10 | Validation Prefix | IP: `192.168.1.1`, Prefix: `33` | Raise `ValueError` / HTTP 400 (`detail` memuat pesan error prefix > 32) | **Pasti (Ditolak)** |
| 11 | Validation Prefix | IP: `192.168.1.1`, Prefix: `-1` | Raise `ValueError` / HTTP 400 (`detail` memuat pesan error prefix < 0) | **Pasti (Ditolak)** |
| 12 | VLSM Calc | Net: `192.168.1.0/24`<br>

<br>Host: `[100, 50, 20, 2]` | Subnet 1: `192.168.1.0/25`<br>

<br>Subnet 2: `192.168.1.128/26`<br>

<br>Subnet 3: `192.168.1.192/27`<br>

<br>Subnet 4: `192.168.1.224/30` | **Pasti (Valid)** |
| 13 | VLSM Calc | Net: `192.168.1.0/24`<br>

<br>Host: `[200, 100]` | Raise `ValueError` / HTTP 400 (`detail` memuat pesan error alokasi tidak muat) | **Pasti (Ditolak)** |

---

## 7. Di Luar Cakupan (Out of Scope)

1. Perhitungan dan alokasi alamat IPv6.
2. Penyimpanan data ke basis data (database/persistence layer).
3. Otentikasi pengguna, manajemen hak akses, dan *session tracking*.
4. Konversi subnet mask ke notasi Wildcard Mask.
5. Export hasil kalkulasi ke format PDF, CSV, atau Excel.