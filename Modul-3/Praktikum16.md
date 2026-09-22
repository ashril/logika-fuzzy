# Praktikum 16 — Final Project Exhibition dan Presentasi Produk Akhir
## Pameran Produk Individual, Presentasi Demonstrasi Aplikasi, Evaluasi Komprehensif, dan Laporan Akhir (Bobot: 20%)

---

## A. Tujuan Pertemuan 16
Pertemuan 16 merupakan sesi puncak (*Cap-Stone Exhibition*) dari seluruh rangkaian perkuliahan dan praktikum Logika Fuzzy. Pada sesi ini, mahasiswa mendemonstrasikan produk perangkat lunak individual yang telah dikembangkan secara bertahap sejak Modul 1. Mahasiswa diharapkan mampu:
1. Mempresentasikan solusi berbasis logika fuzzy di hadapan dosen penguji dan audiens akademik secara sistematis dan percaya diri.
2. Mendemonstrasikan fungsionalitas aplikasi web (*Live Demo*) dalam merespons berbagai skenario masukan nyata.
3. Mempertahankan argumen ilmiah terkait perancangan fungsi keanggotaan, komposisi basis aturan, dan pemilihan metode inferensi.
4. Memaparkan hasil evaluasi kinerja sistem berbasis metrik empiris (MAE, RMSE, dan waktu komputasi).
5. Melakukan refleksi kritis mengenai keterbatasan sistem serta potensi pengembangan ke arah sistem cerdas hibrida (*Neuro-Fuzzy / ANFIS*).

---

## B. Format Pelaksanaan Pameran Produk (*Product Exhibition*)

Pameran produk diselenggarakan dalam bentuk **Simposium / Demo Day**:
- Setiap mahasiswa memiliki stan digital (*Digital Booth*) untuk menjalankan aplikasi web Streamlit mereka secara langsung.
- Sesi presentasi individu berdurasi **10 menit**:
  - **5 Menit:** Presentasi slide ringkas (Latar belakang masalah, arsitektur FIS, dan hasil pengujian).
  - **3 Menit:** Demonstrasi aplikasi langsung (*Live Interactive Demo*).
  - **2 Menit:** Sesi tanya jawab dan pengujian acak oleh dosen penguji (*Defending Session*).

---

## C. Sistematika Slide Presentasi (Maksimal 8 Slide)

1. **Slide 1 — Judul Produk & Identitas:** Nama aplikasi, nama mahasiswa, NIM, dan Program Studi S1 Teknologi Informasi.
2. **Slide 2 — Latar Belakang & Urgensi Masalah:** Fenomena ketidakpastian dunia nyata yang diselesaikan dan batasan logika konvensional.
3. **Slide 3 — Desain Variabel Linguistik:** Tabel semesta pembicaraan, domain, dan bentuk kurva keanggotaan input/output.
4. **Slide 4 — Basis Pengetahuan & Aturan (Rule Base):** Matriks aturan IF-THEN dan rasionalitas logikanya.
5. **Slide 5 — Mesin Inferensi & Defuzzifikasi:** Alasan pemilihan metode (Mamdani/Sugeno/Tsukamoto) dan proses kalkulasi.
6. **Slide 6 — Arsitektur Aplikasi & Cuplikan UI:** Struktur modular software dan antarmuka Streamlit.
7. **Slide 7 — Hasil Evaluasi Kinerja (Dataset Testing):** Tabel akurasi, nilai MAE/RMSE, dan grafik komparasi aktual vs prediksi.
8. **Slide 8 — Kesimpulan & Rencana Pengembangan Masa Depan:** Refleksi produk dan penutup.

---

## D. Rubrik Penilaian Produk Akhir (Bobot Mata Kuliah: 20%)

Berdasarkan RPS resmi Mata Kuliah Logika Fuzzy, penilaian produk akhir dinilai secara komprehensif mengacu pada rubrik standar berikut:

| No | Aspek Penilaian Produk Akhir | Bobot | Deskripsi Indikator Keberhasilan |
|:--:|---|:---:|---|
| 1 | **Identifikasi & Formulasi Masalah** | **15%** | Permasalahan nyata bidang TI jelas, relevansi logika fuzzy tepat, dan batasan masalah terdefinisi baik. |
| 2 | **Perancangan Model Fuzzy** | **20%** | Variabel input/output lengkap, semesta logis, bentuk kurva keanggotaan proporsional, dan overlap antar-label tepat. |
| 3 | **Implementasi Python** | **20%** | Kode terstruktur modular, bersih, efisien, bebas bug, dan mematuhi kaidah *clean code*. |
| 4 | **Rule Base & Inferensi** | **15%** | Aturan IF-THEN lengkap dan konsisten, proses inferensi dan defuzzifikasi berjalan akurat. |
| 5 | **Pengujian & Evaluasi Sistem** | **10%** | Pengujian dataset minimal 10 kasus terdokumentasi, analisis error kuantitatif (MAE/RMSE) tersaji. |
| 6 | **Antarmuka / Aplikasi (UI)** | **10%** | Tampilan Streamlit interaktif, responsif, estetis, dilengkapi validasi input dan visualisasi hasil. |
| 7 | **Presentasi & Demonstrasi Produk** | **5%** | Komunikasi lugas, demo aplikasi lancar, dan mampu menjawab pertanyaan penguji secara ilmiah. |
| 8 | **Dokumentasi & Repositori GitHub** | **5%** | Repositori GitHub tertata rapi, commit log deskriptif, dan `README.md` informatif. |
| | **TOTAL KESELURUHAN** | **100%** | *(Memberikan kontribusi 20% terhadap nilai akhir semester)* |

---

## E. Checklist Berkas Penyerahan Akhir (Final Submission)

Sebelum sesi pameran dimulai, pastikan repositori GitHub Anda telah memuat:

```text
[X] 1. Berkas source code lengkap pada folder Modul-1/, Modul-2/, dan Modul-3/
[X] 2. Aplikasi web Streamlit yang siap dijalankan dengan `streamlit run src/app.py`
[X] 3. File requirements.txt yang valid
[X] 4. File dataset pengujian data/test_cases.csv
[X] 5. Laporan Akhir Proyek format Markdown / PDF
[X] 6. Tautan rekaman video demo produk
[X] 7. Slide presentasi (format PDF/PPTX) disimpan di folder presentation/
```

---

## F. Penutup dan Refleksi Akhir Semester

Selamat! Anda telah menyelesaikan seluruh rangkaian 16 pertemuan praktikum Logika Fuzzy:
1. **Modul 1 (Pertemuan 1–5):** Menguasai dasar himpunan fuzzy, variabel linguistik, fungsi keanggotaan, dan fuzzifikasi manual serta database.
2. **Modul 2 (Pertemuan 6–10):** Menguasai perancangan rule base, mesin inferensi Mamdani, Sugeno, Tsukamoto, dan teknik defuzzifikasi.
3. **Modul 3 (Pertemuan 11–16):** Mengembangkan aplikasi web interaktif nyata dengan Streamlit, melakukan validasi empiris berbasis dataset, dan memamerkan produk cerdas Anda.

Kompetensi yang Anda raih menjadi bekal berharga dalam mendesain sistem cerdas di bidang *Artificial Intelligence*, *Decision Support Systems*, dan *Smart Computing* di era modern.
