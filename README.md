# Modul Praktikum Logika Fuzzy (Fuzzy Logic)
### Program Studi S1 Teknologi Informasi — Bobot 3 SKS

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![Streamlit](https://img.shields.io/badge/Framework-Streamlit-FF4B4B.svg)](https://streamlit.io/)
[![scikit-fuzzy](https://img.shields.io/badge/Library-scikit--fuzzy-orange.svg)](https://pythonhosted.org/scikit-fuzzy/)

Repositori ini memuat materi ajar, panduan praktikum laboratorium, kode program, dan pedoman asesmen proyek untuk mata kuliah **Logika Fuzzy**. Materi disusun secara terintegrasi dengan pendekatan **Problem-Based Learning (PBL)** dan **Project-Based Learning (PjBL)** yang diarahkan untuk menghasilkan produk perangkat lunak cerdas berbasis komputasi lunak (*Soft Computing*).

---

## 🎯 Capaian Pembelajaran Mata Kuliah (CPMK)

Setelah menyelesaikan seluruh modul praktikum ini, mahasiswa diharapkan mampu:
- **CPMK-1:** Menjelaskan konsep dasar logika fuzzy, himpunan fuzzy, fungsi keanggotaan, variabel linguistik, dan operasi himpunan fuzzy.
- **CPMK-2:** Merancang representasi masalah nyata menggunakan variabel input, variabel output, semesta pembicaraan, dan fungsi keanggotaan.
- **CPMK-3:** Menerapkan proses inferensi fuzzy menggunakan aturan IF-THEN dengan metode **Mamdani**, **Sugeno**, dan **Tsukamoto**.
- **CPMK-4:** Mengimplementasikan sistem fuzzy menggunakan bahasa pemrograman **Python** dan pustaka relevan.
- **CPMK-5:** Menganalisis dan mengevaluasi hasil sistem inferensi fuzzy berdasarkan dataset dan skenario pengujian empiris.
- **CPMK-6:** Merancang dan memproduksi aplikasi web cerdas interaktif berbasis **Streamlit** untuk menyelesaikan permasalahan nyata di bidang Teknologi Informasi.

---

## 📚 Struktur Silabus & Daftar Pertemuan (16 Pertemuan)

Materi perkuliahan terbagi ke dalam **3 Modul Utama** yang berkembang secara kumulatif membentuk satu produk perangkat lunak utuh:

### 🔹 Modul 1: Dasar-Dasar Logika Fuzzy dan Fuzzifikasi (Pertemuan 1 – 5)
*Fokus: Pemahaman konsep dasar, representasi matematika, perancangan fungsi keanggotaan, dan fuzzifikasi.*

| Pertemuan | Dokumen Modul | Topik Materi | Luaran / Output Utama |
|:---:|---|---|---|
| **1** | [Praktikum 1](Modul-1/Praktikum1.md) | **Pengantar Logika Fuzzy & Derajat Keanggotaan** | Visualisasi perbandingan logika Crisp vs Fuzzy |
| **2** | [Praktikum 2](Modul-1/Praktikum2.md) | **Himpunan Fuzzy & Variabel Linguistik** | Pemodelan variabel linguistik multi-label |
| **3** | [Praktikum 3](Modul-1/Praktikum3.md) | **Fungsi Keanggotaan & Fuzzifikasi Dinamis** | Implementasi manual & integrasi database MySQL/Python |
| **4** | [Praktikum 4](Modul-1/Praktikum4.md) | **Operasi Himpunan Fuzzy** | Eksperimen Zadeh Min-Max, T-Norm, & T-Conorm |
| **5** | [Praktikum 5](Modul-1/Praktikum5.md) | **Asesmen Modul 1: Pemodelan Fuzzy** | **Tugas Proyek 1: Fuzzy Modeling (Bobot 20%)** |

---

### 🔹 Modul 2: Inferensi dan Sistem Fuzzy (Pertemuan 6 – 10)
*Fokus: Perancangan aturan IF-THEN, penalaran mesin inferensi, komparasi metode Mamdani, Sugeno, Tsukamoto, dan defuzzifikasi.*

| Pertemuan | Dokumen Modul | Topik Materi | Luaran / Output Utama |
|:---:|---|---|---|
| **6** | [Praktikum 6](Modul-2/Praktikum6.md) | **Fuzzy Rule Base & Knowledge Base** | Struktur aturan IF-THEN & evaluasi firing strength |
| **7** | [Praktikum 7](Modul-2/Praktikum7.md) | **Arsitektur Fuzzy Inference System (FIS)** | Pipeline komputasi FIS end-to-end |
| **8** | [Praktikum 8](Modul-2/Praktikum8.md) | **Metode Mamdani & Metode Defuzzifikasi** | Komparasi Centroid, Bisector, MOM, SOM, dan LOM |
| **9** | [Praktikum 9](Modul-2/Praktikum9.md) | **Metode Sugeno dan Tsukamoto** | Implementasi TSK Orde 0 & 1 serta Tsukamoto Monotonik |
| **10** | [Praktikum 10](Modul-2/Praktikum10.md) | **Asesmen Modul 2: Fuzzy Decision System** | **Tugas Proyek 2: Decision System (Bobot 25%)** |

---

### 🔹 Modul 3: Implementasi, Evaluasi, dan Pengembangan Produk (Pertemuan 11 – 16)
*Fokus: Integrasi dataset dunia nyata, evaluasi kuantitatif (MAE/RMSE), pembuatan aplikasi web interaktif Streamlit, dan pameran produk.*

| Pertemuan | Dokumen Modul | Topik Materi | Luaran / Output Utama |
|:---:|---|---|---|
| **11** | [Praktikum 11](Modul-3/Praktikum11.md) | **Fuzzy pada Permasalahan Nyata** | Formulasi kebutuhan & Proposal Produk TI |
| **12** | [Praktikum 12](Modul-3/Praktikum12.md) | **Evaluasi Sistem Menggunakan Dataset** | Pengujian batch data, evaluasi error MAE & RMSE |
| **13** | [Praktikum 13](Modul-3/Praktikum13.md) | **Pengembangan Web App dengan Streamlit** | Antarmuka web interaktif & visualisasi keputusan |
| **14** | [Praktikum 14](Modul-3/Praktikum14.md) | **Penyempurnaan & Pengujian Black-Box** | Refactoring kode, error handling, & pengujian UI |
| **15** | [Praktikum 15](Modul-3/Praktikum15.md) | **Asesmen Modul 3: Aplikasi Fuzzy** | **Tugas Proyek 3: Fuzzy Application (Bobot 25%)** |
| **16** | [Praktikum 16](Modul-3/Praktikum16.md) | **Final Project Exhibition & Demo Produk** | **Pameran Produk Akhir & Presentasi (Bobot 20%)** |

---

## 📊 Skema Asesmen & Bobot Penilaian

Penilaian kelulusan praktikum mengacu pada akumulasi evaluasi berkala:

```text
┌────────────────────────────────────────────────────────────┬─────────┐
│ Komponen Penilaian                                         │  Bobot  │
├────────────────────────────────────────────────────────────┼─────────┤
│ Asesmen Modul 1: Fuzzy Modeling (Pertemuan 5)              │   20%   │
│ Asesmen Modul 2: Fuzzy Decision System (Pertemuan 10)      │   25%   │
│ Asesmen Modul 3: Fuzzy Application (Pertemuan 15)          │   25%   │
│ Final Product Exhibition & Presentasi (Pertemuan 16)       │   20%   │
│ Aktivitas Praktikum, Tugas Mandiri, & Partisipasi Lab      │   10%   │
├────────────────────────────────────────────────────────────┼─────────┤
│ TOTAL KESELURUHAN                                          │  100%   │
└────────────────────────────────────────────────────────────┴─────────┘
```

---

## 🛠️ Prasyarat & Lingkungan Pengembangan

### Pustaka Perangkat Lunak
Pastikan komputer Anda telah terpasang **Python 3.9+**. Pustaka yang digunakan:
- `numpy`: Komputasi array numerik dan operasi matriks.
- `matplotlib`: Visualisasi kurva keanggotaan dan grafik permukaan keputusan.
- `pandas`: Pengolahan dataset pengujian.
- `scikit-fuzzy`: Toolkit inferensi logika fuzzy.
- `streamlit`: Kerangka kerja antarmuka web interaktif.
- `mysql-connector-python` *(opsional)*: Konektor database MySQL untuk Praktikum 3.

### Panduan Instalasi Cepat
Kloning repositori ini dan pasang seluruh pustaka dependensi:

```bash
# 1. Kloning repositori
git clone https://github.com/username/modul-logika-fuzzy.git
cd modul-logika-fuzzy

# 2. Buat virtual environment (disarankan)
python -m venv .venv

# Aktivasi di Windows (PowerShell):
.venv\Scripts\Activate.ps1
# Atau di Linux/macOS:
source .venv/bin/activate

# 3. Pasang dependensi pustaka
pip install numpy matplotlib pandas scikit-fuzzy streamlit mysql-connector-python
```

---

## 🚀 Alur Kerja Pengerjaan & Git Workflow

Setiap mahasiswa wajib mempraktikkan manajemen kode berbasis Git:

```bash
# Periksa status perubahan berkas
git status

# Tambahkan perubahan berkas yang telah dikerjakan
git add Modul-1/

# Buat commit dengan pesan yang deskriptif dan terstandarisasi
git commit -m "feat(modul1): selesaikan tugas praktikum 1"

# Unggah perubahan ke repositori GitHub masing-masing
git push origin main
```

---

## 🏛️ Struktur Direktori Repositori

```text
modul-logika-fuzzy/
├── README.md                      # Panduan utama silabus dan repositori
├── RPS.md                         # Dokumen Rencana Pembelajaran Semester (format Markdown)
├── Modul-1/                       # MODUL 1: Fuzzifikasi & Fungsi Keanggotaan
│   ├── Praktikum1.md              # Pertemuan 1: Crisp vs Fuzzy & Derajat Keanggotaan
│   ├── Praktikum2.md              # Pertemuan 2: Variabel & Label Linguistik
│   ├── Praktikum3.md              # Pertemuan 3: Fungsi Keanggotaan & Integrasi MySQL
│   ├── Praktikum4.md              # Pertemuan 4: Operasi Himpunan Fuzzy
│   ├── Praktikum5.md              # Pertemuan 5: Asesmen 1 (Fuzzy Modeling)
│   └── Modul_1_Dasar_Logika_Fuzzy_dan_Fuzzifikasi.ipynb
├── Modul-2/                       # MODUL 2: Inferensi dan Sistem Fuzzy
│   ├── Praktikum6.md              # Pertemuan 6: Fuzzy Rule Base & Firing Strength
│   ├── Praktikum7.md              # Pertemuan 7: Arsitektur Pipeline FIS
│   ├── Praktikum8.md              # Pertemuan 8: Metode Mamdani & 5 Metode Defuzzifikasi
│   ├── Praktikum9.md              # Pertemuan 9: Metode Sugeno & Tsukamoto
│   └── Praktikum10.md             # Pertemuan 10: Asesmen 2 (Fuzzy Decision System)
└── Modul-3/                       # MODUL 3: Pengembangan Produk & Evaluasi
    ├── Praktikum11.md             # Pertemuan 11: Proposal Produk Kasus Nyata TI
    ├── Praktikum12.md             # Pertemuan 12: Evaluasi Dataset & Metrik Error
    ├── Praktikum13.md             # Pertemuan 13: Aplikasi Web Streamlit
    ├── Praktikum14.md             # Pertemuan 14: Pengujian Black-Box & Refactoring
    ├── Praktikum15.md             # Pertemuan 15: Asesmen 3 (Fuzzy Application)
    └── Praktikum16.md             # Pertemuan 16: Final Project Exhibition & Demo
```

---

## 📄 Lisensi

Materi ajar ini dilisensikan di bawah [MIT License](LICENSE). Bebas digunakan untuk keperluan pendidikan dan akademik.