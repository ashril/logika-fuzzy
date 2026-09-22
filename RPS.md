# RENCANA PEMBELAJARAN SEMESTER (RPS)
## Mata Kuliah: Logika Fuzzy

> **Pengantar Kurikulum:**  
> Untuk Program Studi Teknologi Informasi, mata kuliah Logika Fuzzy diarahkan pada:  
> **Pemahaman Konsep $\to$ Perancangan Sistem Fuzzy $\to$ Implementasi Python $\to$ Produk/Aplikasi**.  
> Dengan demikian, teori dan praktikum berjalan terintegrasi melalui pola **3 Modul, 16 Pertemuan, 3 Asesmen**, di mana setiap modul menghasilkan satu tugas praktikum (*final practical assignment*) yang berkembang secara bertahap menjadi produk akhir mahasiswa.

---

## 1. Identitas Mata Kuliah

| Komponen | Keterangan |
|---|---|
| **Program Studi** | S1 Teknologi Informasi |
| **Fakultas** | Sesuai struktur perguruan tinggi |
| **Mata Kuliah** | Logika Fuzzy |
| **Kode Mata Kuliah** | Disesuaikan |
| **Bobot** | 3 SKS |
| **Semester** | Disesuaikan |
| **Sifat Mata Kuliah** | Keilmuan/Keahlian Teknologi Informasi |
| **Prasyarat** | Matematika Diskrit / Matematika Dasar dan Pemrograman Dasar |
| **Bentuk Pembelajaran** | Kuliah teori dan praktikum |
| **Bahasa Pemrograman** | Python |
| **Perangkat Utama** | Jupyter Notebook / Google Colab, NumPy, Matplotlib, scikit-fuzzy |
| **Model Pembelajaran** | Project-Based Learning dan Problem-Based Learning |

---

## 2. Deskripsi Mata Kuliah

Mata kuliah **Logika Fuzzy** membahas konsep, prinsip, metode, dan implementasi sistem berbasis logika fuzzy untuk menyelesaikan permasalahan pengambilan keputusan dan pengendalian yang mengandung ketidakpastian atau nilai linguistik.

Pembelajaran dimulai dari konsep dasar himpunan fuzzy, fungsi keanggotaan, variabel linguistik, operasi himpunan fuzzy, dan aturan fuzzy. Selanjutnya mahasiswa mempelajari proses inferensi fuzzy, metode Mamdani, Sugeno, dan Tsukamoto, serta defuzzifikasi.

Materi teori diintegrasikan dengan praktikum menggunakan Python sehingga mahasiswa tidak hanya mampu menghitung proses fuzzy secara manual, tetapi juga mampu membangun sistem fuzzy yang dapat digunakan untuk menyelesaikan permasalahan nyata.

Perkuliahan dilaksanakan dalam **tiga modul**. Setiap modul menghasilkan tugas akhir praktikum yang menjadi bagian dari pengembangan produk akhir. Pada akhir semester setiap mahasiswa wajib menghasilkan sebuah produk berbasis logika fuzzy, seperti sistem rekomendasi, sistem penilaian, sistem klasifikasi berbasis aturan fuzzy, atau sistem pendukung keputusan sederhana.

---

## 3. Capaian Pembelajaran Lulusan (CPL) yang Didukung

Mata kuliah ini mendukung beberapa CPL Program Studi Teknologi Informasi, khususnya:

- **CPL-1 — Pengetahuan:**  
  Mahasiswa mampu memahami konsep matematika, logika, komputasi, dan teknologi informasi yang mendukung pengembangan solusi berbasis komputer.
- **CPL-2 — Keterampilan Umum:**  
  Mahasiswa mampu menerapkan pemikiran logis, kritis, sistematis, dan inovatif dalam menyelesaikan permasalahan di bidang Teknologi Informasi.
- **CPL-3 — Keterampilan Khusus:**  
  Mahasiswa mampu merancang dan mengimplementasikan solusi komputasional menggunakan bahasa pemrograman dan perangkat teknologi informasi.
- **CPL-4 — Pengembangan Solusi:**  
  Mahasiswa mampu menghasilkan solusi Teknologi Informasi berdasarkan analisis kebutuhan dan karakteristik permasalahan.

---

## 4. Capaian Pembelajaran Mata Kuliah (CPMK)

Setelah mengikuti mata kuliah ini, mahasiswa mampu:

- **CPMK-1:** Menjelaskan konsep dasar logika fuzzy, himpunan fuzzy, fungsi keanggotaan, variabel linguistik, dan operasi fuzzy.
- **CPMK-2:** Merancang representasi masalah nyata menggunakan variabel input, variabel output, himpunan fuzzy, dan fungsi keanggotaan.
- **CPMK-3:** Menerapkan proses inferensi fuzzy menggunakan aturan IF-THEN dan metode inferensi yang sesuai.
- **CPMK-4:** Mengimplementasikan sistem fuzzy menggunakan Python dan library yang relevan.
- **CPMK-5:** Menganalisis dan mengevaluasi hasil sistem fuzzy berdasarkan skenario pengujian.
- **CPMK-6:** Merancang dan menghasilkan produk/aplikasi sederhana berbasis logika fuzzy untuk menyelesaikan permasalahan nyata.

---

## 5. Struktur Modul Pembelajaran

| Modul | Topik Utama | Pertemuan | Asesmen |
|---|---|:---:|---|
| **Modul 1** | Dasar-Dasar Logika Fuzzy dan Fuzzifikasi | 1–5 | Asesmen 1 |
| **Modul 2** | Inferensi dan Sistem Fuzzy | 6–10 | Asesmen 2 |
| **Modul 3** | Implementasi, Evaluasi, dan Pengembangan Produk | 11–16 | Asesmen 3 + Produk Akhir |

> **Pola Setiap Modul:**  
> $\text{Teori} \to \text{Contoh Kasus} \to \text{Praktikum} \to \text{Tugas Proyek} \to \text{Asesmen Modul}$

---

### MODUL 1: Dasar-Dasar Logika Fuzzy dan Fuzzifikasi
**Tujuan Modul:**  
Mahasiswa mampu memahami konsep dasar logika fuzzy dan mengubah permasalahan nyata menjadi representasi fuzzy menggunakan variabel linguistik dan fungsi keanggotaan.

#### Pertemuan 1 — Pengantar Logika Fuzzy
- **Materi:**
  - Permasalahan pengambilan keputusan dalam kondisi ketidakpastian
  - Logika Boolean/crisp versus fuzzy
  - Konsep derajat keanggotaan
  - Sejarah dan perkembangan logika fuzzy
  - Contoh penerapan fuzzy pada Teknologi Informasi
  - Contoh sistem rekomendasi dan sistem pendukung keputusan
- **Praktikum:**
  - Pengenalan Python/Jupyter Notebook
  - Representasi data crisp dan fuzzy
  - Visualisasi konsep derajat keanggotaan

#### Pertemuan 2 — Himpunan Fuzzy dan Variabel Linguistik
- **Materi:**
  - Himpunan crisp vs himpunan fuzzy
  - Derajat keanggotaan
  - Variabel linguistik
  - Domain dan semesta pembicaraan
  - Label linguistik
- **Praktikum:**
  - Membuat himpunan fuzzy menggunakan Python
  - Visualisasi himpunan fuzzy
  - Representasi variabel linguistik

#### Pertemuan 3 — Fungsi Keanggotaan
- **Materi:**
  - Fungsi keanggotaan
  - Fungsi segitiga
  - Fungsi trapesium
  - Fungsi Gaussian
  - Fungsi sigmoid
  - Pemilihan fungsi keanggotaan berdasarkan karakteristik data
- **Praktikum:**
  - Implementasi fungsi keanggotaan menggunakan NumPy
  - Visualisasi fungsi keanggotaan menggunakan Matplotlib
  - Implementasi menggunakan scikit-fuzzy

#### Pertemuan 4 — Operasi Himpunan Fuzzy
- **Materi:**
  - Union (Gabungan/OR)
  - Intersection (Irisan/AND)
  - Complement (Komplemen/NOT)
  - AND dan OR fuzzy
  - T-norm
  - T-conorm
  - Interpretasi hasil operasi fuzzy
- **Praktikum:**
  - Implementasi operasi fuzzy
  - Eksperimen perubahan nilai keanggotaan
  - Analisis hasil operasi

#### Pertemuan 5 — Asesmen Modul 1
- **Final Practical Assignment 1: Fuzzy Modeling (Bobot: 20%)**  
  Mahasiswa memilih satu permasalahan sederhana, kemudian:
  1. Menentukan permasalahan.
  2. Menentukan variabel input dan output.
  3. Menentukan domain masing-masing variabel.
  4. Menentukan himpunan linguistik.
  5. Menentukan fungsi keanggotaan.
  6. Mengimplementasikan fungsi keanggotaan menggunakan Python.
  7. Membuat visualisasi.
  8. Melakukan fuzzifikasi terhadap beberapa data input.
- **Output:** Jupyter Notebook, Laporan singkat, Presentasi/demo.

---

### MODUL 2: Inferensi dan Sistem Fuzzy
**Tujuan Modul:**  
Mahasiswa mampu merancang aturan fuzzy, melakukan proses inferensi, dan menghasilkan output menggunakan metode fuzzy.

#### Pertemuan 6 — Fuzzy Rule dan Knowledge Base
- **Materi:**
  - Konsep IF-THEN
  - Antecedent dan consequent
  - Penyusunan fuzzy rule
  - Knowledge base
  - Rule base
  - Contoh sistem rekomendasi
- **Praktikum:**
  - Menyusun rule fuzzy
  - Implementasi rule menggunakan Python
  - Pengujian beberapa kombinasi input

#### Pertemuan 7 — Fuzzy Inference System
- **Materi:**
  - Konsep Fuzzy Inference System (FIS)
  - Fuzzifikasi
  - Rule evaluation
  - Aggregation
  - Defuzzifikasi
  - Arsitektur sistem fuzzy
- **Praktikum:**
  - Membangun FIS sederhana
  - Simulasi proses inferensi
  - Visualisasi proses fuzzy

#### Pertemuan 8 — Metode Mamdani
- **Materi:**
  - Konsep metode Mamdani
  - Fuzzifikasi
  - Implikasi
  - Agregasi
  - Defuzzifikasi: Centroid, Bisector, Mean of Maximum (MOM)
- **Praktikum:**
  - Implementasi sistem Mamdani
  - Menggunakan library scikit-fuzzy
  - Membandingkan beberapa metode defuzzifikasi

#### Pertemuan 9 — Metode Sugeno dan Tsukamoto
- **Materi:**
  - Konsep metode Sugeno
  - Model Sugeno orde 0 dan orde 1
  - Konsep metode Tsukamoto
  - Perbedaan Mamdani, Sugeno, dan Tsukamoto
  - Pemilihan metode berdasarkan kebutuhan
- **Praktikum:**
  - Implementasi sistem Sugeno sederhana
  - Simulasi Tsukamoto
  - Perbandingan hasil metode

#### Pertemuan 10 — Asesmen Modul 2
- **Final Practical Assignment 2: Fuzzy Decision System (Bobot: 25%)**  
  Mahasiswa mengembangkan sistem fuzzy berdasarkan model pada Modul 1. Minimal sistem memiliki:
  - 2 variabel input
  - 1 variabel output
  - Minimal 3 himpunan fuzzy untuk setiap variabel
  - Minimal 6 fuzzy rules
  - Proses fuzzifikasi, inferensi, dan defuzzifikasi
  - Visualisasi hasil
  - Mahasiswa wajib menjelaskan alasan pemilihan metode fuzzy.
- **Output:** Program Python, Notebook, Dokumentasi sistem, Video/demo singkat.

---

### MODUL 3: Implementasi, Evaluasi, dan Pengembangan Produk
**Tujuan Modul:**  
Mahasiswa mampu mengembangkan sistem fuzzy menjadi aplikasi/produk yang dapat digunakan untuk menyelesaikan permasalahan nyata.

#### Pertemuan 11 — Fuzzy pada Permasalahan Nyata
- **Materi:**
  - Identifikasi masalah
  - Analisis kebutuhan sistem
  - Pemilihan variabel fuzzy
  - Perancangan rule base
  - Penggunaan data nyata
  - Studi kasus bidang Teknologi Informasi (Sistem rekomendasi, penentuan prioritas, penilaian mahasiswa, seleksi penerima bantuan, prediksi tingkat kepuasan, kualitas layanan, smart tourism, smart campus)
- **Praktikum:**
  - Menentukan ide produk
  - Menentukan problem statement
  - Menentukan input/output sistem
  - Menyusun rancangan awal produk

#### Pertemuan 12 — Fuzzy dengan Data dan Evaluasi Sistem
- **Materi:**
  - Data sebagai input sistem fuzzy
  - Data preprocessing sederhana
  - Pengujian sistem
  - Sensitivity analysis
  - Error dan validasi
  - Perbandingan output fuzzy dengan keputusan aktual / aturan pembanding
- **Praktikum:**
  - Memasukkan dataset
  - Melakukan pengujian
  - Mengukur performa sistem
  - Membuat tabel hasil pengujian
  - Visualisasi hasil

#### Pertemuan 13 — Pengembangan Aplikasi Fuzzy
- **Materi:**
  - Arsitektur aplikasi fuzzy
  - Pemisahan logic dan interface
  - Input pengguna
  - Output sistem
  - Visualisasi hasil
  - Konsep deployment aplikasi
- **Praktikum:**
  - Mengubah notebook menjadi aplikasi sederhana
  - Implementasi menggunakan Streamlit
  - Membuat form input
  - Menampilkan hasil inferensi

#### Pertemuan 14 — Pengembangan dan Penyempurnaan Produk
- **Materi:**
  - User interface sederhana
  - Interpretasi hasil
  - Pengujian black-box
  - Dokumentasi aplikasi
  - Code organization
  - Versioning dan pengelolaan proyek
- **Praktikum:**
  - Penyempurnaan aplikasi
  - Pengujian
  - Perbaikan rule base & fungsi keanggotaan
  - Penyusunan dokumentasi

#### Pertemuan 15 — Asesmen Modul 3
- **Final Practical Assignment 3: Fuzzy Application (Bobot: 25%)**  
  Mahasiswa mengembangkan sistem fuzzy menjadi aplikasi yang dapat digunakan. Produk minimal memiliki:
  - Interface input
  - Proses fuzzifikasi, fuzzy inference, defuzzifikasi
  - Output keputusan/rekomendasi
  - Visualisasi atau interpretasi hasil
  - Dokumentasi
  - Dataset atau skenario pengujian (minimal 10 kasus)
- **Output:** Source code, Aplikasi, Dataset, Dokumentasi, Video demo.

#### Pertemuan 16 — Final Project Exhibition dan Presentasi Produk
- **Aktivitas Mahasiswa:**
  - Presentasi produk
  - Demonstrasi aplikasi secara langsung
  - Penjelasan permasalahan dan model fuzzy
  - Demonstrasi proses inferensi dan hasil
  - Evaluasi produk dan refleksi pengembangan
- **Output Akhir:** **Individual Fuzzy Product** (Aplikasi/sistem berbasis logika fuzzy untuk menyelesaikan masalah nyata, bobot: 20%).

---

## 6. Rencana Pembelajaran 16 Pertemuan

| Ptm | Modul | Materi | Aktivitas | Output |
|:---:|:---:|---|---|---|
| **1** | M1 | Pengantar Logika Fuzzy | Teori + Python | Notebook 1 |
| **2** | M1 | Himpunan Fuzzy | Teori + Praktikum | Himpunan fuzzy |
| **3** | M1 | Fungsi Keanggotaan | Teori + Praktikum | Visualisasi MF |
| **4** | M1 | Operasi Fuzzy | Teori + Praktikum | Implementasi operasi |
| **5** | M1 | Asesmen 1 | Project | Fuzzy Modeling |
| **6** | M2 | Fuzzy Rule | Teori + Praktikum | Rule base |
| **7** | M2 | Fuzzy Inference | Teori + Praktikum | FIS |
| **8** | M2 | Mamdani | Teori + Praktikum | Mamdani system |
| **9** | M2 | Sugeno & Tsukamoto | Teori + Praktikum | Perbandingan metode |
| **10** | M2 | Asesmen 2 | Project | Fuzzy Decision System |
| **11** | M3 | Fuzzy Problem Solving | Teori + Project | Proposal produk |
| **12** | M3 | Data & Evaluasi | Teori + Praktikum | Hasil pengujian |
| **13** | M3 | Pengembangan Aplikasi | Praktikum | Prototype |
| **14** | M3 | Penyempurnaan Produk | Praktikum | Produk beta |
| **15** | M3 | Asesmen 3 | Project | Fuzzy Application |
| **16** | M3 | Final Project | Presentasi & Demo | Produk akhir |

---

## 7. Skema Asesmen

| Komponen | Bobot |
|---|:---:|
| Asesmen Modul 1 – Fuzzy Modeling | 20% |
| Asesmen Modul 2 – Fuzzy Decision System | 25% |
| Asesmen Modul 3 – Fuzzy Application | 25% |
| Final Product & Exhibition | 20% |
| Aktivitas / latihan / praktikum | 10% |
| **Total** | **100%** |

---

## 8. Konsep Pengembangan Produk Bertahap

Produk akhir tidak dibuat dari nol pada minggu terakhir, melainkan dibangun secara kumulatif:

```text
Tahap 1 — Modeling (Modul 1)
Problem ──► Variable ──► Membership Function ──► Fuzzification
   │
   ▼
Tahap 2 — Decision System (Modul 2)
Fuzzification ──► Rule Base ──► Inference ──► Defuzzification
   │
   ▼
Tahap 3 — Application (Modul 3)
Dataset/Input ──► Fuzzy Engine ──► Decision ──► Interface ──► Evaluation
   │
   ▼
Final Product (Pertemuan 16)
Aplikasi / Sistem Berbasis Logika Fuzzy
```

> **Catatan Penting:**  
> Dengan pola ini, tiga asesmen sebenarnya merupakan tahapan pengembangan satu produk yang sama, bukan tiga tugas yang terpisah.

---

## 9. Contoh Tema Produk Akhir

Mahasiswa bebas memilih masalah, asalkan produk memiliki komponen fuzzy yang jelas:

- **Bidang Smart Campus:**
  - Sistem penentuan prioritas penerima beasiswa
  - Sistem evaluasi kepuasan mahasiswa
  - Sistem penentuan prioritas perbaikan fasilitas kampus
  - Sistem rekomendasi mata kuliah
- **Bidang Smart Tourism:**
  - Sistem rekomendasi destinasi wisata
  - Sistem penilaian kualitas destinasi wisata
  - Sistem rekomendasi hotel
  - Sistem penentuan tingkat kepuasan wisatawan
  - Sistem prioritas pengembangan destinasi
- **Bidang Teknologi Informasi:**
  - Sistem penentuan prioritas tiket helpdesk
  - Sistem penilaian kualitas jaringan
  - Sistem rekomendasi spesifikasi komputer
  - Sistem penentuan tingkat risiko keamanan informasi
  - Sistem prioritas pemeliharaan perangkat
- **Bidang Bisnis:**
  - Sistem rekomendasi produk
  - Sistem penentuan tingkat kepuasan pelanggan
  - Sistem penilaian kelayakan pelanggan
  - Sistem penentuan prioritas calon pelanggan

---

## 10. Kriteria Produk Akhir

Produk akhir mahasiswa minimal memenuhi:

| Komponen | Persyaratan |
|---|---|
| **Permasalahan** | Permasalahan nyata dan jelas |
| **Input** | Minimal 2 variabel |
| **Membership Function** | Dirancang berdasarkan karakteristik masalah |
| **Rule** | Minimal 6 aturan |
| **Fuzzy Inference** | Menggunakan metode yang jelas |
| **Output** | Keputusan / rekomendasi / nilai |
| **Implementasi** | Python |
| **Interface** | Aplikasi sederhana (Web App Streamlit) |
| **Pengujian** | Minimal 10 skenario |
| **Dokumentasi** | Tersedia lengkap |
| **Presentasi** | Demo produk secara langsung |

---

## 11. Metode Pembelajaran

Pembelajaran menggunakan kombinasi:
- Case-Based Learning
- Problem-Based Learning
- Project-Based Learning
- Ceramah interaktif
- Demonstrasi
- Praktikum pemrograman
- Diskusi, Presentasi, Peer review, dan Project exhibition

**Proporsi Pembelajaran:**  
Sekitar **40% teori + 60% praktikum/proyek**.

---

## 12. Teknologi dan Tools

- **Bahasa Pemrograman:** Python
- **Library:** NumPy, Pandas, Matplotlib, scikit-fuzzy
- **Lingkungan Pengembangan:** Google Colab atau Jupyter Notebook
- **Pengembangan Aplikasi:** Streamlit
- **Manajemen Kode:** Git / GitHub

---

## 13. Bentuk Produk Akhir

Produk akhir diarahkan menjadi sebuah **Fuzzy Decision Support Application** dengan alur:

```text
USER
 │
 ▼
INPUT DATA
 │
 ▼
FUZZIFICATION
 │
 ▼
FUZZY RULE BASE
 │
 ▼
FUZZY INFERENCE
 │
 ▼
DEFUZZIFICATION
 │
 ▼
HASIL KEPUTUSAN
 │
 ▼
VISUALISASI / REKOMENDASI
```

Mahasiswa diharapkan mampu menjelaskan seluruh proses komputasi tersebut, bukan hanya menggunakan *black-box library*.

---

## 14. Rubrik Penilaian Produk Akhir

| No | Aspek | Bobot |
|:--:|---|:---:|
| 1 | Identifikasi dan formulasi masalah | 15% |
| 2 | Perancangan model fuzzy | 20% |
| 3 | Implementasi Python | 20% |
| 4 | Rule base dan inferensi | 15% |
| 5 | Pengujian dan evaluasi | 10% |
| 6 | Interface / aplikasi | 10% |
| 7 | Presentasi dan demonstrasi | 5% |
| 8 | Dokumentasi | 5% |
| | **Total** | **100%** |

---

## 15. Strategi Integrasi Teori dan Praktikum

Setiap pertemuan mengikuti pola:  
$$\text{Konsep} \to \text{Contoh Manual} \to \text{Implementasi Python} \to \text{Eksperimen} \to \text{Analisis}$$

Sebagai contoh pada materi **Mamdani**:
1. **Teori:** Mahasiswa memahami fuzzifikasi, rule evaluation, aggregation, dan defuzzifikasi.
2. **Perhitungan Manual:** Mahasiswa menyelesaikan satu kasus sederhana secara manual di atas kertas.
3. **Python:** Mahasiswa mengimplementasikan kasus tersebut ke dalam kode.
4. **Eksperimen:** Mahasiswa mengubah parameter membership function dan rule.
5. **Analisis:** Mahasiswa menjelaskan bagaimana perubahan parameter memengaruhi keputusan sistem.

---

## 16. Target Kompetensi Akhir

Pada akhir semester, mahasiswa diharapkan mampu:
> *"Merancang, mengimplementasikan, menguji, dan mendemonstrasikan sebuah aplikasi berbasis logika fuzzy untuk menyelesaikan permasalahan nyata menggunakan Python."*

Dengan demikian, luaran mata kuliah bukan hanya nilai ujian atau laporan praktikum, melainkan produk Teknologi Informasi nyata yang dapat dipresentasikan dan dikembangkan lebih lanjut.
