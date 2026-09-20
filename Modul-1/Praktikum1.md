# Praktikum Modul 1
## Implementasi Fungsi Keanggotaan Fuzzy dengan MySQL dan Python

## A. Tujuan Praktikum
Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:
1. Memahami hubungan antara fungsi keanggotaan fuzzy dan persamaan matematika.
2. Menghitung persamaan fungsi keanggotaan secara manual.
3. Menyimpan interval fungsi keanggotaan ke dalam database MySQL.
4. Menghubungkan Python dengan database MySQL.
5. Mengambil informasi fungsi keanggotaan dari database.
6. Menentukan fungsi yang harus digunakan berdasarkan nilai crisp.
7. Mengeksekusi fungsi keanggotaan Python secara dinamis.
8. Menghasilkan nilai derajat keanggotaan `μ(x)` tanpa menggunakan library fuzzy.

> **Catatan penting:**
> Pada praktikum ini mahasiswa **tidak diperbolehkan menggunakan library fuzzy** seperti `scikit-fuzzy` untuk menghitung derajat keanggotaan.
> Tujuan praktikum adalah memahami proses fuzzifikasi dari dasar, mulai dari persamaan matematika sampai implementasinya dalam Python.

# B. Konsep Dasar

Pada praktikum sebelumnya telah dipelajari bahwa fungsi keanggotaan fuzzy dapat dibentuk dari beberapa titik.
Sebagai contoh, fungsi keanggotaan **Usia Remaja** berbentuk segitiga:

```text
μ(x)
1.0                    ● (15,1)
                      / \
                     /   \
                    /     \
                   /       \
                  /         \
0.0 ─────────────●───────────●────────────────
                 10          20

                 Usia
```

Fungsi tersebut mempunyai tiga bagian:

1. Bagian sebelum usia 10 tahun → derajat keanggotaan `0`.
2. Bagian naik usia 10–15 tahun → menggunakan fungsi linear naik.
3. Bagian turun usia 15–20 tahun → menggunakan fungsi linear turun.
4. Bagian setelah usia 20 tahun → derajat keanggotaan `0`.

---

# C. Menghitung Fungsi Keanggotaan Secara Manual
> **Catatan penting:**
> Ini hanya contoh saja, pada saat praktikum, gunakan sesuai dengan fungsi yang Anda buat pada Tugas 1 atau Tugas 1 yang sudah Anda perbaiki

Misalkan fungsi keanggotaan **Remaja** ditentukan oleh titik:

```text
(10, 0)
(15, 1)
(20, 0)
```

## 1. Fungsi naik
Fungsi naik berada pada interval:

```text
10 ≤ x ≤ 15
```

Dengan titik:

```text
(x1, y1) = (10, 0)
(x2, y2) = (15, 1)
```

Gunakan persamaan garis:

$$
\frac{y-y_1}{y_2-y_1}
=
\frac{x-x_1}{x_2-x_1}
$$

Substitusi:

$$
\frac{y-0}{1-0}
=
\frac{x-10}{15-10}
$$

Sehingga:

$$
y = \frac{x-10}{5}
$$

Maka fungsi keanggotaan naik adalah:

$$
\boxed{\mu(x)=\frac{x-10}{5}}
$$

---

## 2. Fungsi turun

Fungsi turun berada pada interval:

```text
15 ≤ x ≤ 20
```

Dengan titik:

```text
(x1, y1) = (15, 1)
(x2, y2) = (20, 0)
```

Gunakan persamaan garis:

$$
\frac{y-1}{0-1}
=
\frac{x-15}{20-15}
$$

Sehingga:

$$
y = \frac{20-x}{5}
$$

Maka fungsi keanggotaan turun adalah:

$$
\boxed{\mu(x)=\frac{20-x}{5}}
$$

---

# D. Fungsi Keanggotaan dalam Python
Setelah mendapatkan persamaan secara manual, persamaan tersebut diterjemahkan ke dalam fungsi Python.

```python
def fungsi_remaja_naik(x):
    return (x - 10) / 5


def fungsi_remaja_turun(x):
    return (20 - x) / 5
```

Contoh:

```python
print(fungsi_remaja_naik(12))
```

Hasil:

```text
0.4
```

Karena:

$$
\mu(12)=\frac{12-10}{5}=0.4
$$

Contoh lainnya:

```python
print(fungsi_remaja_turun(17))
```

Hasil:

```text
0.6
```

Karena:

$$
\mu(17)=\frac{20-17}{5}=0.6
$$

---

# E. Menyimpan Fungsi dalam Database

Pada praktikum ini digunakan database MySQL dengan nama:

```text
fuzzy_modul1
```

Database tidak menyimpan seluruh nilai derajat keanggotaan.

Database hanya menyimpan:

* batas bawah interval,
* batas atas interval,
* fungsi yang harus digunakan.

Dengan demikian database bertugas menentukan:

> Nilai crisp ini berada pada interval mana dan fungsi Python mana yang harus dijalankan?

# F. Membuat Database MySQL

Buka MySQL atau phpMyAdmin.

Jalankan:

```sql
CREATE DATABASE fuzzy_modul1;
```

Kemudian pilih database:

```sql
USE fuzzy_modul1;
```

# G. Membuat Tabel `usia_remaja`

Buat tabel:

```sql
CREATE TABLE usia_remaja (
    id INT AUTO_INCREMENT PRIMARY KEY,
    usia_min INT NOT NULL,
    usia_max INT NOT NULL,
    nilai_fuzzy VARCHAR(50) NOT NULL
);
```

Perhatikan bahwa kolom:

```text
nilai_fuzzy
```

menggunakan tipe:

```text
VARCHAR
```

karena kolom tersebut dapat berisi:

```text
0
fungsi_remaja_naik
fungsi_remaja_turun
```

# H. Memasukkan Data Fungsi Keanggotaan

Masukkan data:

```sql
INSERT INTO usia_remaja
(usia_min, usia_max, nilai_fuzzy)
VALUES
(0, 10, '0'),
(10, 15, 'fungsi_remaja_naik'),
(15, 20, 'fungsi_remaja_turun'),
(20, 150, '0');
```

Periksa data:

```sql
SELECT * FROM usia_remaja;
```

Hasil:

| id | usia_min | usia_max | nilai_fuzzy         |
| -: | -------: | -------: | ------------------- |
|  1 |        0 |       10 | 0                   |
|  2 |       10 |       15 | fungsi_remaja_naik  |
|  3 |       15 |       20 | fungsi_remaja_turun |
|  4 |       20 |      150 | 0                   |


# I. Semesta Pembicaraan

Pada contoh ini, semesta pembicaraan usia dibatasi:

```text
0 ≤ usia ≤ 150
```

Artinya sistem hanya menerima usia antara 0 sampai 150 tahun.

Fungsi keanggotaan:

```text
0 – 10    → 0
10 – 15   → fungsi naik
15 – 20   → fungsi turun
20 – 150  → 0
```

Secara visual:

```text
μ(x)
1.0                    ●
                      / \
                     /   \
                    /     \
                   /       \
                  /         \
0.0 ─────────────●───────────●────────────────
                 10   15     20              150

                 Usia
```


# J. Instalasi Library MySQL untuk Python

Python membutuhkan library untuk berkomunikasi dengan MySQL.

Buka terminal VS Code:

```bash
pip install mysql-connector-python
```

Jika menggunakan Python tertentu:

```bash
python -m pip install mysql-connector-python
```

Untuk memastikan library telah terpasang:

```bash
pip show mysql-connector-python
```

# K. Membuat Koneksi Python ke MySQL

Buat file:

```text
fuzzy_usia.py
```

Masukkan kode:

```python
import mysql.connector


db = mysql.connector.connect(
    host="localhost",
    user="root",
    password="PASSWORD_MYSQL_ANDA",
    database="fuzzy_modul1"
)

print("Koneksi database berhasil!")

db.close()
```

Ganti:

```text
PASSWORD_MYSQL_ANDA
```

dengan password MySQL yang digunakan pada komputer Anda.

Jika MySQL tidak menggunakan password:

```python
password=""
```


# L. Membuat Fungsi Keanggotaan

Tambahkan fungsi berikut:

```python
def fungsi_remaja_naik(x):
    return (x - 10) / 5


def fungsi_remaja_turun(x):
    return (20 - x) / 5
```

Fungsi tersebut berasal dari hasil perhitungan manual.


# M. Menghubungkan Nama Fungsi Database dengan Fungsi Python

Database menyimpan nama:

```text
fungsi_remaja_naik
```

atau:

```text
fungsi_remaja_turun
```

Python harus mengetahui bahwa nama tersebut mengacu pada fungsi Python.

Gunakan dictionary:

```python
fungsi = {
    "fungsi_remaja_naik": fungsi_remaja_naik,
    "fungsi_remaja_turun": fungsi_remaja_turun
}
```

Dengan demikian:

```text
fungsi_remaja_naik
        ↓
fungsi Python fungsi_remaja_naik()

fungsi_remaja_turun
        ↓
fungsi Python fungsi_remaja_turun()
```

# N. Membuat Fungsi Fuzzifikasi

Selanjutnya buat fungsi:

```python
def fuzzifikasi_usia(x):

    cursor = db.cursor()

    query = """
        SELECT usia_min, usia_max, nilai_fuzzy
        FROM usia_remaja
        WHERE %s >= usia_min
        AND %s <= usia_max
    """

    cursor.execute(query, (x, x))

    data = cursor.fetchone()

    cursor.close()

    if data is None:
        return None

    usia_min, usia_max, nama_fungsi = data

    if nama_fungsi == "0":
        return 0

    if nama_fungsi in fungsi:

        fungsi_y = fungsi[nama_fungsi]

        nilai = fungsi_y(x)

        return nilai

    raise ValueError(
        f"Fungsi '{nama_fungsi}' belum dibuat di Python."
    )
```


# O. Memahami Cara Kerja Fungsi Fuzzifikasi

Misalkan:

```python
x = 17
```

Program akan mencari ke database.

Query yang dijalankan secara konsep adalah:

```sql
SELECT usia_min, usia_max, nilai_fuzzy
FROM usia_remaja
WHERE 17 >= usia_min
AND 17 <= usia_max;
```

Database menemukan:

```text
usia_min = 15
usia_max = 20
nilai_fuzzy = fungsi_remaja_turun
```

Kemudian Python mendapatkan:

```python
nama_fungsi = "fungsi_remaja_turun"
```

Python mencari fungsi:

```python
fungsi_y = fungsi[nama_fungsi]
```

yang sama dengan:

```python
fungsi_y = fungsi_remaja_turun
```

Kemudian:

```python
nilai = fungsi_y(17)
```

sama dengan:

```python
nilai = fungsi_remaja_turun(17)
```

Kemudian:

$$
\mu(17)=\frac{20-17}{5}
$$

$$
\mu(17)=0.6
$$


# P. Program Lengkap

Berikut program lengkap yang dapat digunakan sebagai dasar praktikum:

```python
import mysql.connector


# ==========================================================
# 1. KONEKSI DATABASE
# ==========================================================

db = mysql.connector.connect(
    host="localhost",
    user="root",
    password="PASSWORD_MYSQL_ANDA",
    database="fuzzy_modul1"
)

print("Koneksi database berhasil!")


# ==========================================================
# 2. FUNGSI KEANGGOTAAN
# ==========================================================

def fungsi_remaja_naik(x):
    """
    Fungsi keanggotaan remaja bagian naik.

    Domain:
    10 <= x <= 15

    Persamaan:
    μ(x) = (x - 10) / 5
    """
    return (x - 10) / 5


def fungsi_remaja_turun(x):
    """
    Fungsi keanggotaan remaja bagian turun.

    Domain:
    15 <= x <= 20

    Persamaan:
    μ(x) = (20 - x) / 5
    """
    return (20 - x) / 5


# ==========================================================
# 3. DAFTAR FUNGSI
# ==========================================================

fungsi = {
    "fungsi_remaja_naik": fungsi_remaja_naik,
    "fungsi_remaja_turun": fungsi_remaja_turun
}


# ==========================================================
# 4. FUNGSI FUZZIFIKASI
# ==========================================================

def fuzzifikasi_usia(x):

    cursor = db.cursor()

    query = """
        SELECT usia_min, usia_max, nilai_fuzzy
        FROM usia_remaja
        WHERE %s >= usia_min
        AND %s <= usia_max
    """

    cursor.execute(query, (x, x))

    data = cursor.fetchone()

    cursor.close()

    if data is None:
        return None

    usia_min, usia_max, nama_fungsi = data

    # Jika database memberikan nilai 0
    if nama_fungsi == "0":
        return 0

    # Jika database memberikan nama fungsi
    if nama_fungsi in fungsi:

        fungsi_y = fungsi[nama_fungsi]

        nilai = fungsi_y(x)

        return nilai

    raise ValueError(
        f"Fungsi '{nama_fungsi}' belum dibuat di Python."
    )


# ==========================================================
# 5. INPUT USIA
# ==========================================================

usia = float(input("Masukkan usia: "))


# ==========================================================
# 6. PROSES FUZZIFIKASI
# ==========================================================

nilai_keanggotaan = fuzzifikasi_usia(usia)


# ==========================================================
# 7. MENAMPILKAN HASIL
# ==========================================================

print()
print("================================")
print("HASIL FUZZIFIKASI")
print("================================")
print(f"Usia               : {usia}")
print(f"Keanggotaan remaja : {nilai_keanggotaan}")
print("================================")


# ==========================================================
# 8. MENUTUP DATABASE
# ==========================================================

db.close()
```

---

# Q. Pengujian Program

Lakukan pengujian menggunakan beberapa nilai usia.

## Pengujian 1

Input:

```text
5
```

Database menemukan:

```text
0 – 10 → 0
```

Hasil:

```text
μ(5) = 0
```

---

## Pengujian 2

Input:

```text
12
```

Database menemukan:

```text
10 – 15 → fungsi_remaja_naik
```

Python menghitung:

$$
\mu(12)=\frac{12-10}{5}
$$

Hasil:

```text
μ(12) = 0.4
```

---

## Pengujian 3

Input:

```text
17
```

Database menemukan:

```text
15 – 20 → fungsi_remaja_turun
```

Python menghitung:

$$
\mu(17)=\frac{20-17}{5}
$$

Hasil:

```text
μ(17) = 0.6
```

---

## Pengujian 4

Input:

```text
25
```

Database menemukan:

```text
20 – 150 → 0
```

Hasil:

```text
μ(25) = 0
```

---

# R. Tugas Praktikum

Buat fungsi fuzzy untuk semua variabel usia yang ada pada Tugas 1 Anda, lakukan pengembangan berikut.

## Tugas Praktikum 1 — Verifikasi Fungsi

Hitung secara manual nilai keanggotaan --> Sudah dilakukan pada Tugas 1.
Buat tabel dalam database

## Tugas 2 — Pengujian Program

Jalankan program dengan minimal **2 usia di setiap variabel usia** yang berbeda.

Catat hasilnya:

| No | Input Usia | Interval Database | Fungsi | μ(x) |
| -: | ---------: | ----------------- | ------ | ---: |
|  1 |            |                   |        |      |
|  2 |            |                   |        |      |
|  3 |            |                   |        |      |
|  4 |            |                   |        |      |
|  5 |            |                   |        |      |
|  6 |            |                   |        |      |
|  7 |            |                   |        |      |
|  8 |            |                   |        |      |
|  9 |            |                   |        |      |
| 10 |            |                   |        |      |

---

# S. Pertanyaan Analisis

Jawab pertanyaan berikut.

### 1.

Mengapa database tidak menyimpan semua nilai derajat keanggotaan?

### 2.

Apa fungsi dari kolom:

```text
usia_min
```

### 3.

Apa fungsi dari kolom:

```text
usia_max
```

### 4.

Mengapa `nilai_fuzzy` menggunakan tipe data `VARCHAR`?

### 5.

Apa yang terjadi ketika nilai crisp `17` diberikan kepada program?

Jelaskan prosesnya mulai dari:

```text
Input → Database → Fungsi Python → Hasil
```

### 6.

Apa yang terjadi jika database memberikan:

```text
fungsi_remaja_turun
```

tetapi fungsi tersebut tidak dibuat di Python?

### 7.

Mengapa pada praktikum ini tidak digunakan library `scikit-fuzzy`?

### 8.

Apa hubungan antara persamaan garis lurus yang dihitung secara manual dengan fungsi Python?


# U. Ketentuan Praktikum

1. Persamaan fungsi harus dihitung **secara manual terlebih dahulu**.
2. Mahasiswa wajib menunjukkan proses mendapatkan persamaan.
3. Tidak diperbolehkan menggunakan `scikit-fuzzy` untuk menghitung fungsi keanggotaan.
4. Fungsi keanggotaan harus dibuat sendiri menggunakan Python.
5. Database harus menggunakan MySQL.
6. Program harus mengambil informasi interval dari database.
7. Program harus menentukan fungsi berdasarkan data dari database.
8. Program harus mengeksekusi fungsi Python yang sesuai.
9. Hasil program harus dibandingkan dengan hasil perhitungan manual.
10. Setiap mahasiswa harus dapat menjelaskan alur:

```text
Nilai Crisp
    ↓
Database
    ↓
Interval
    ↓
Nama Fungsi
    ↓
Fungsi Python
    ↓
Nilai Keanggotaan μ(x)
```

# V. Kesimpulan

Pada praktikum ini, mahasiswa membangun proses fuzzifikasi sederhana tanpa menggunakan library fuzzy.

Konsep utama yang harus dipahami adalah:

```text
Persamaan Matematika
        ↓
Fungsi Python
        ↓
Database menyimpan interval
        ↓
Database menentukan fungsi
        ↓
Python mengeksekusi fungsi
        ↓
Derajat Keanggotaan
```

Database **tidak menggantikan fungsi Python**.

Database berperan sebagai sumber informasi untuk menentukan:

> **"Untuk nilai crisp ini, fungsi keanggotaan yang mana yang harus digunakan?"**

Sedangkan Python berperan sebagai:

> **"Mesin yang menjalankan persamaan fungsi tersebut."**
tanpa mengubah prinsip dasarnya.

