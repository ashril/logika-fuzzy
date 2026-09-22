# Praktikum 10 — Asesmen Modul 2: Fuzzy Decision System
## Final Practical Assignment 2: Fuzzy Decision Support System (Bobot: 25%)

---

## A. Tujuan Asesmen Modul 2
Asesmen Modul 2 dirancang untuk menguji kompetensi mahasiswa dalam merancang sistem inferensi fuzzy end-to-end yang mengintegrasikan model variabel dari Modul 1 dengan penalaran aturan, inferensi, dan defuzzifikasi. Setelah menyelesaikan proyek ini, mahasiswa mampu:
1. Mengembangkan model fuzzy dari Modul 1 menjadi sebuah sistem pengambil keputusan (*Fuzzy Decision System*).
2. Merancang basis aturan IF-THEN yang konsisten, lengkap (*complete*), dan bebas konflik.
3. Memilih dan menjustifikasi metode inferensi yang tepat (**Mamdani, Sugeno, atau Tsukamoto**) berdasarkan karakteristik kasus.
4. Mengimplementasikan mesin inferensi dan defuzzifikasi secara utuh menggunakan Python.
5. Memvisualisasikan kurva inferensi dan permukaan keputusan (*decision surface*).
6. Mendokumentasikan dan mempresentasikan mekanisme kerja sistem secara ilmiah dan profesional.

---

## B. Deskripsi Tugas Proyek

Proyek ini merupakan kelanjutan langsung dari **Modul 1 (Tahap 1: Modeling)** menuju **Tahap 2: Decision System**:

```text
TAHAP 1 (Modul 1)                      TAHAP 2 (Modul 2 - Pertemuan 10)
Variabel & Fuzzifikasi  ───►  Basis Aturan (≥ 6 Rules) ───► Mesin Inferensi ───► Defuzzifikasi
                                                                                       │
                                                                                       ▼
                                                  (Siap diintegrasikan ke Web App Modul 3)
```

Mahasiswa menggunakan topik masalah yang sama dengan yang telah dirancang pada Modul 1 (atau melakukan revisi perbaikan jika ada masukan).

---

## C. Persyaratan Teknis Minimal

Sistem yang dibangun wajib memenuhi kriteria berikut:

| Komponen | Persyaratan Minimal |
|---|---|
| **Variabel Input** | Minimal **2 variabel input** numerik |
| **Variabel Output** | Minimal **1 variabel output** numerik |
| **Himpunan Fuzzy** | Minimal **3 himpunan/label linguistik** per variabel |
| **Basis Aturan** | Minimal **6 aturan IF-THEN** (disarankan matriks penuh $3 \times 3 = 9$ aturan) |
| **Metode Inferensi** | Memilih salah satu: **Mamdani**, **Sugeno**, atau **Tsukamoto** |
| **Justifikasi Metode** | Wajib menjelaskan secara tertulis alasan pemilihan metode tersebut |
| **Defuzzifikasi** | Centroid/MOM (Mamdani) atau Weighted Average (Sugeno/Tsukamoto) |
| **Visualisasi** | Grafik kurva agregasi atau *Decision Surface Plot* 3D |
| **Bahasa Pemrograman** | Python 3 (menggunakan `scikit-fuzzy` atau implementasi murni) |

---

## D. Panduan Langkah Pengerjaan

### Langkah 1: Penyusunan Matriks Basis Aturan
Susun tabel matriks kombinasi label input dan tentukan konklusi output secara logis:

*Contoh Matriks Aturan Sistem Prioritas Tiket Helpdesk:*
| Waktu Tunggu \ Urgensi Masalah | Rendah | Sedang | Tinggi |
|---|---|---|---|
| **Cepat** | R1: Ringan | R2: Ringan | R3: Sedang |
| **Sedang** | R4: Ringan | R5: Sedang | R6: Tinggi |
| **Lama** | R7: Sedang | R8: Tinggi | R9: Kritis |

### Langkah 2: Justifikasi Pemilihan Metode Inferensi
Tuliskan 1 paragraf argumentatif mengenai metode yang Anda pilih:
- *Contoh jika memilih Mamdani:* "Metode Mamdani dipilih karena sistem penilaian beasiswa ini membutuhkan penalaran yang mudah dipahami oleh komite seleksi (intuitif), di mana konklusi output berupa derajat linguistik kelayakan yang halus dan kontinu."
- *Contoh jika memilih Sugeno:* "Metode Sugeno dipilih karena sistem kendali pendingin server memerlukan respon kalkulasi matematis yang cepat dan langsung berupa besaran angka RPM kipas tanpa komputasi integral defuzzifikasi yang membebani CPU."

### Langkah 3: Implementasi Program Python Lengkap
Susun script Python yang dapat menerima input nilai crisp dari pengguna dan mengeluarkan nilai keputusan konkret.

### Langkah 4: Pembuatan Visualisasi Permukaan Keputusan (*Decision Surface Plot*)
Gambarkan grafik 3D yang menunjukkan korelasi antara Input 1 (Sumbu X), Input 2 (Sumbu Y), dan Output Keputusan (Sumbu Z).

*Contoh Template Kode Decision Surface:*
```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Grid input
x1_range = np.linspace(0, 10, 30)
x2_range = np.linspace(0, 100, 30)
X1, X2 = np.meshgrid(x1_range, x2_range)
Z_out = np.zeros_like(X1)

# Hitung output inferensi untuk setiap titik grid (X1[i, j], X2[i, j])
for i in range(X1.shape[0]):
    for j in range(X1.shape[1]):
        Z_out[i, j] = evaluasi_sistem_fuzzy(X1[i, j], X2[i, j])

fig = plt.figure(figsize=(10, 7))
ax = fig.add_subplot(111, projection='3d')
surf = ax.plot_surface(X1, X2, Z_out, cmap='viridis', edgecolor='none', alpha=0.9)
ax.set_xlabel('Input 1')
ax.set_ylabel('Input 2')
ax.set_zlabel('Output Keputusan')
ax.set_title('Decision Surface Plot Sistem Fuzzy', fontweight='bold')
fig.colorbar(surf, shrink=0.5, aspect=5)
plt.savefig('decision_surface.png', dpi=300)
plt.show()
```

### Langkah 5: Pengujian Minimal 5 Skenario Kasus Nyata
Uji sistem dengan minimal 5 kombinasi data ekstrem dan normal, kemudian buat tabel analisis perbandingannya.

---

## E. Template Struktur Laporan Asesmen 2

Laporan disusun dalam format Markdown (`Laporan_Asesmen2_<NIM>.md`) dengan sistematika:
1. **Identitas & Judul Proyek**
2. **Ringkasan Model Variabel Fuzzy (Review Modul 1)**
3. **Perancangan Basis Aturan (*Rule Base Matrix*)**
4. **Metode Inferensi & Justifikasi Pemilihan**
5. **Implementasi Program Python (Full Code & Penjelasan)**
6. **Hasil Pengujian dan Analisis Decision Surface**
7. **Rencana Integrasi ke Aplikasi Web (Tahap Modul 3)**

---

## F. Rubrik Penilaian Asesmen Modul 2 (Bobot: 25%)

| No | Kriteria Penilaian | Bobot |
|:--:|---|:---:|
| 1 | **Struktur Basis Aturan (CPMK-3):** Kelengkapan, konsistensi, dan ketepatan logika kombinasi aturan. | 25% |
| 2 | **Implementasi Mesin Inferensi & Defuzzifikasi (CPMK-3, 4):** Kebenaran proses kalkulasi dan modularitas kode Python. | 30% |
| 3 | **Ketepatan Justifikasi Metode (CPMK-3):** Argumentasi ilmiah pemilihan metode Mamdani/Sugeno/Tsukamoto. | 15% |
| 4 | **Visualisasi & Decision Surface (CPMK-4):** Kualitas grafik kurva dan plot permukaan keputusan 3D. | 15% |
| 5 | **Pengujian Sistem & Analisis Kasus (CPMK-5):** Kedalaman analisis respon sistem pada skenario pengujian. | 15% |
| | **TOTAL** | **100%** |

---

## G. Ketentuan Pengumpulan
1. Seluruh berkas (kode program, notebook, laporan markdown, dan gambar grafik) dikumpulkan di folder:
   `Modul-2/Asesmen2_<NIM>_<Nama>/`
2. Push ke GitHub:
   ```bash
   git add Modul-2/
   git commit -m "feat(modul2): kumpulkan final practical assignment 2 fuzzy decision system"
   git push origin main
   ```
