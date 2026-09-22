# Praktikum 14 — Penyempurnaan dan Pengujian Produk Fuzzy
## Refactoring Kode, Pengujian Black-Box Sistem, Penanganan Eksepsi (Error Handling), dan Dokumentasi Teknis

---

## A. Tujuan Praktikum
Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:
1. Melakukan refaktorisasi kode program (*code refactoring*) agar terstruktur rapi, modular, dan mematuhi konvensi PEP 8.
2. Menerapkan mekanisme penanganan kesalahan (*error handling* dan *input validation*) pada aplikasi web fuzzy.
3. Menyusun rencana pengujian perangkat lunak berbasis kotak hitam (*Black-Box Testing*) untuk menguji fungsi sistem dari sudut pandang pengguna.
4. Melakukan penyempurnaan antarmuka pengguna (UI/UX) pada aplikasi Streamlit agar lebih komunikatif dan informatif.
5. Menyusun dokumentasi teknis (*Technical Documentation*) dan buku panduan pengguna (*User Guide*).

---

## B. Konsep Dasar

### 1. Dari Prototipe Menuju Produk Beta
Pada Pertemuan 13, mahasiswa telah berhasil membangun aplikasi dasar (*prototype*). Namun, sebelum produk dirilis untuk asesmen akhir, prototipe tersebut harus melalui tahap penyempurnaan (*refinement*):
- **Keandalan (*Robustness*):** Apakah sistem macet jika pengguna memasukkan angka nol, nilai di luar semesta, atau karakter tak terduga?
- **Kejelasan Komunikasi (*Clarity*):** Apakah pengguna awam memahami alasan sistem menghasilkan rekomendasi tertentu?
- **Kerapian Kode (*Clean Code*):** Apakah kode terdokumentasi dengan docstring dan mudah dirawat?

### 2. Pengujian Black-Box (Black-Box Testing)
Pengujian Black-Box adalah metode pengujian perangkat lunak yang berfokus pada fungsionalitas input dan output tanpa melihat kode program internal. Teknik yang digunakan meliputi:
- **Equivalence Partitioning:** Membagi domain input ke dalam partisi-partisi valid dan tidak valid.
- **Boundary Value Analysis (BVA):** Menguji titik-titik tepat di batas minimum, tepat di bawah batas, dan tepat di atas batas semesta pembicaraan.

---

## C. Matriks Pengujian Black-Box

Setiap mahasiswa wajib merancang tabel pengujian minimal 10 kasus uji (*Test Cases*):

| ID Uji | Skenario Pengujian | Input 1 (Waktu) | Input 2 (Urgensi) | Output yang Diharapkan | Output Aktual Sistem | Status (Pass/Fail) |
|:--:|---|:---:|:---:|---|---|:---:|
| TC-01 | Batas Bawah Semesta | 0.0 jam | 0.0 poin | Prioritas Rendah (< 30) | Skor: 20.0 (Rendah) | **PASS** |
| TC-02 | Batas Atas Semesta | 24.0 jam | 100.0 poin | Prioritas Kritis (> 90) | Skor: 95.0 (Kritis) | **PASS** |
| TC-03 | Nilai Tengah (Transisi) | 12.0 jam | 50.0 poin | Prioritas Sedang | Skor: 55.0 (Sedang) | **PASS** |
| TC-04 | Waktu Lama, Urgensi Nol | 20.0 jam | 5.0 poin | Prioritas Rendah-Sedang | Skor: 42.5 (Sedang) | **PASS** |
| TC-05 | Waktu Singkat, Urgensi Maks | 0.5 jam | 95.0 poin | Prioritas Sedang-Tinggi | Skor: 65.0 (Tinggi) | **PASS** |
| TC-06 | Input Negatif (Di Luar Batas) | -2.0 jam | 50.0 poin | Sistem Menolak / Pesan Error | Error Validasi Ditampilkan | **PASS** |
| TC-07 | Input Melebihi Batas | 28.0 jam | 50.0 poin | Sistem Menolak / Pesan Error | Error Validasi Ditampilkan | **PASS** |
| TC-08 | Uji Kasus Tipikal A | 4.0 jam | 30.0 poin | Prioritas Rendah | Skor: 28.0 (Rendah) | **PASS** |
| TC-09 | Uji Kasus Tipikal B | 8.0 jam | 70.0 poin | Prioritas Tinggi | Skor: 76.5 (Tinggi) | **PASS** |
| TC-10 | Uji Kasus Tipikal C | 15.0 jam | 85.0 poin | Prioritas Kritis | Skor: 91.2 (Kritis) | **PASS** |

---

## D. Implementasi Error Handling dan Validasi pada Streamlit

Perbarui kode `app.py` Anda untuk menangani eksepsi:

```python
import streamlit as st
from fuzzy_engine import hitung_prioritas_tiket

st.sidebar.subheader("Validasi Input Khusus")

try:
    waktu_manual = st.sidebar.number_input("Input Waktu Manual (Jam):", value=5.0)
    urgensi_manual = st.sidebar.number_input("Input Skor Urgensi Manual:", value=50.0)
    
    # Validasi Batas Semesta
    if waktu_manual < 0 or waktu_manual > 24:
        st.error("⚠️ Error: Waktu tunggu harus berada pada rentang 0 hingga 24 jam!")
    elif urgensi_manual < 0 or urgensi_manual > 100:
        st.error("⚠️ Error: Skor urgensi harus berada pada rentang 0 hingga 100 poin!")
    else:
        skor, kategori, _ = hitung_prioritas_tiket(waktu_manual, urgensi_manual)
        st.success(f"Hasil Eksekusi Valid: Skor = {skor} ({kategori})")

except Exception as e:
    st.error(f"Terjadi kesalahan komputasi: {str(e)}")
```

---

## E. Penyusunan Dokumentasi Pengguna (User Guide)

Dokumentasi pengguna disusun pada file `README_APP.md` di folder proyek dengan konten:
1. **Deskripsi Singkat Aplikasi:** Tujuan dan manfaat penggunaan sistem.
2. **Prasyarat Instalasi:** Versi Python dan pustaka yang dibutuhkan (`requirements.txt`).
3. **Cara Menjalankan:** Perintah CLI untuk menyalakan server lokal Streamlit.
4. **Panduan Antarmuka:** Penjelasan setiap widget input dan cara membaca hasil rekomendasi.
5. **Tabel Interpretasi Keputusan:** Arti dari setiap kategori output dan tindakan lanjutan yang disarankan.

---

## F. Tugas Praktikum 14

1. Lakukan pengujian Black-Box terhadap aplikasi Streamlit Anda untuk **minimal 10 skenario pengujian**.
2. Buat tabel laporan pengujian Black-Box lengkap seperti format Bagian C.
3. Tambahkan validasi batas input dan pesan error yang ramah pengguna.
4. Buat file `requirements.txt` yang memuat seluruh dependensi proyek:
   ```text
   streamlit>=1.30.0
   numpy>=1.24.0
   matplotlib>=3.7.0
   pandas>=2.0.0
   scikit-fuzzy>=0.4.2
   ```
5. Susun berkas dokumentasi panduan pengguna `Modul-3/README_APP.md`.

---

## G. Pertanyaan Analisis

1. Mengapa pengujian titik batas (*Boundary Value Analysis*) sering kali menjadi tempat ditemukannya anomali atau bug pada sistem fuzzy?
2. Bagaimana cara membuktikan kepada pengguna bahwa sistem fuzzy yang Anda buat tidak menghasilkan keputusan yang bias atau diskriminatif?
3. Mengapa penyediaan file `requirements.txt` dan dokumentasi pengguna yang jelas sangat penting dalam repositori proyek GitHub?

---

## H. Kesimpulan
Penyempurnaan produk melalui refaktorisasi kode, penanganan error, dan pengujian black-box yang ketat memastikan bahwa sistem pendukung keputusan fuzzy yang dibangun tidak hanya unggul secara teori, tetapi juga andal, aman, dan siap digunakan oleh pengguna nyata.
