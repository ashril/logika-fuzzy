# Praktikum 15 — Asesmen Modul 3: Aplikasi Fuzzy
## Final Practical Assignment 3: Fuzzy Application Deployment (Bobot: 25%)

---

## A. Tujuan Asesmen Modul 3
Asesmen Modul 3 merupakan puncak pengembangan teknis (*technical milestone*) di mana mahasiswa mewujudkan model fuzzy dan mesin inferensi yang telah dirancang menjadi sebuah aplikasi perangkat lunak interaktif yang berfungsi penuh. Setelah menyelesaikan proyek ini, mahasiswa mampu:
1. Menghasilkan aplikasi berbasis web interaktif menggunakan Python dan Streamlit.
2. Mengintegrasikan seluruh siklus inferensi fuzzy (fuzzifikasi, inferensi aturan, dan defuzzifikasi) ke dalam arsitektur perangkat lunak modular.
3. Menyediakan visualisasi dan interpretasi keputusan yang mudah dipahami oleh pengguna.
4. Memvalidasi keandalan fungsional aplikasi menggunakan dataset pengujian minimal 10 kasus.
5. Menyusun dokumentasi perangkat lunak lengkap dan membuat video demonstrasi produk singkat.

---

## B. Kriteria dan Persyaratan Minimal Aplikasi

Aplikasi yang diserahkan wajib memenuhi seluruh daftar periksa (*checklist*) berikut:

| No | Komponen Produk | Persyaratan Minimal | Status Verifikasi |
|:--:|---|---|:---:|
| 1 | **Antarmuka Masukan (UI)** | Menggunakan Streamlit dengan slider / formulir input interaktif | [ ] |
| 2 | **Validasi Masukan** | Memiliki proteksi input di luar rentang semesta (*error handling*) | [ ] |
| 3 | **Fuzzy Engine Backend** | Terpisah secara modular dalam berkas tersendiri (`fuzzy_engine.py`) | [ ] |
| 4 | **Mesin Inferensi** | Mengimplementasikan Mamdani, Sugeno, atau Tsukamoto secara benar | [ ] |
| 5 | **Defuzzifikasi** | Menghasilkan nilai output numerik riil (*crisp output*) | [ ] |
| 6 | **Interpretasi Keputusan** | Menyajikan label kategori, badge status, atau teks rekomendasi | [ ] |
| 7 | **Visualisasi Interaktif** | Menampilkan grafik kurva keanggotaan atau aktivasi aturan di web | [ ] |
| 8 | **Dataset Pengujian** | Menyediakan berkas dataset CSV minimal **10 skenario pengujian** | [ ] |
| 9 | **Dokumentasi Lengkap** | Berkas `README.md` panduan instalasi dan penggunaan aplikasi | [ ] |
| 10 | **Video Demo Singkat** | Rekaman video demo berdurasi 3–5 menit yang menjelaskan fitur | [ ] |

---

## C. Struktur Berkas Repositori Proyek Asesmen 3

Setiap mahasiswa menata folder proyek di repositori GitHub dengan susunan:

```text
Modul-3/Asesmen3_<NIM>_<Nama>/
├── README.md                      # Dokumentasi teknis & panduan instalasi
├── requirements.txt               # Daftar dependensi pustaka Python
├── data/
│   └── test_cases.csv             # Dataset pengujian minimal 10 kasus
├── src/
│   ├── __init__.py
│   ├── fuzzy_engine.py            # Logika murni inferensi fuzzy
│   └── app.py                     # Antarmuka web interaktif Streamlit
├── assets/
│   └── screenshot_aplikasi.png    # Gambar tangkapan layar antarmuka
└── demo/
    └── link_video_demo.txt        # Tautan video rekaman demo (YouTube / Google Drive)
```

---

## D. Panduan Pembuatan Video Demo Produk

Video demonstrasi berdurasi **3 hingga 5 menit** dengan format:
1. **Menit 0:00 - 1:00:** Perkenalan mahasiswa, judul produk, dan penjelasan latar belakang masalah nyata yang diselesaikan.
2. **Menit 1:00 - 2:00:** Penjelasan singkat arsitektur sistem (variabel input, basis aturan, dan metode inferensi yang dipilih).
3. **Menit 2:00 - 4:00:** Demonstrasi langsung (*Live Demo*) aplikasi Streamlit:
   - Menjalankan perintah `streamlit run app.py`.
   - Menguji skenario input normal.
   - Menguji skenario input ekstrem/kritis.
   - Memperlihatkan grafik visualisasi keputusan yang terbentuk.
4. **Menit 4:00 - 5:00:** Kesimpulan, keterbatasan sistem saat ini, dan rencana pengembangan masa depan.

---

## E. Rubrik Penilaian Asesmen Modul 3 (Bobot: 25%)

| No | Aspek Penilaian | Indikator Kinerja | Bobot |
|:--:|---|---|:---:|
| 1 | **Fungsionalitas Aplikasi (CPMK-4, 6)** | Aplikasi berjalan lancar tanpa error, inferensi fuzzy akurat, input interaktif, dan visualisasi informatif. | 35% |
| 2 | **Kualitas Kode & Arsitektur (CPMK-4)** | Pemisahan kode bersih (clean code), modularitas (`src/`), validasi data, dan efisiensi eksekusi. | 20% |
| 3 | **Validasi & Dataset Uji (CPMK-5)** | Kelengkapan pengujian minimal 10 kasus nyata pada file CSV dan analisis hasil evaluasi. | 15% |
| 4 | **Dokumentasi Perangkat Lunak (CPMK-6)** | Kejelasan panduan instalasi, kelengkapan `requirements.txt`, dan kemudahan replikasi pengujian. | 15% |
| 5 | **Video Demonstrasi Produk (CPMK-6)** | Kejelasan penyampaian, profesionalitas demo, dan ketepatan penjelasan alur logika sistem. | 15% |
| | **TOTAL** | | **100%** |

---

## F. Ketentuan Pengumpulan
1. Seluruh kode program, dataset, dan berkas dokumentasi diunggah ke repositori GitHub.
2. Pastikan file `requirements.txt` telah dicoba pada environment baru agar dosen/penguji dapat menjalankan program secara mandiri:
   ```bash
   pip install -r requirements.txt
   streamlit run src/app.py
   ```
3. Lakukan git commit dan push:
   ```bash
   git add Modul-3/
   git commit -m "feat(modul3): rilis final practical assignment 3 fuzzy application"
   git push origin main
   ```
