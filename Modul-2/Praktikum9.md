# Praktikum 9 — Metode Sugeno dan Tsukamoto
## Implementasi Sistem Inferensi Takagi-Sugeno-Kang (TSK Orde 0 & 1), Metode Tsukamoto, dan Komparasi dengan Mamdani

---

## A. Tujuan Praktikum
Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:
1. Memahami prinsip kerja metode inferensi **Takagi-Sugeno-Kang (TSK / Sugeno)** orde 0 dan orde 1.
2. Memahami prinsip kerja metode inferensi **Tsukamoto** yang menggunakan fungsi keanggotaan monotonik.
3. Melakukan perhitungan manual untuk proses inferensi Sugeno dan Tsukamoto menggunakan teknik rata-rata terbobot (*Weighted Average*).
4. Mengimplementasikan algoritma Sugeno dan Tsukamoto secara modular menggunakan bahasa pemrograman Python.
5. Membandingkan karakteristik, akurasi, efisiensi komputasi, dan pemilihan metode antara **Mamdani, Sugeno, dan Tsukamoto**.

---

## B. Konsep Dasar

### 1. Metode Sugeno (Takagi-Sugeno-Kang)
Diperkenalkan oleh **Takagi, Sugeno, dan Kang (1985)**. Pada metode Sugeno, konsekuen aturan **bukanlah himpunan fuzzy**, melainkan persamaan matematika tegas (*crisp*).

#### A. Sugeno Orde 0 (Konstanta)
Konsekuen berbentuk nilai konstanta skalar:
$$\textbf{Rule } i: \textbf{IF } x \text{ is } A_i \textbf{ AND } y \text{ is } B_i \textbf{ THEN } z_i = k_i$$

#### B. Sugeno Orde 1 (Fungsi Linear)
Konsekuen merupakan kombinasi linear dari variabel-variabel input:
$$\textbf{Rule } i: \textbf{IF } x \text{ is } A_i \textbf{ AND } y \text{ is } B_i \textbf{ THEN } z_i = p_i x + q_i y + r_i$$

#### Defuzzifikasi Sugeno: Rata-Rata Terbobot (*Weighted Average*)
Karena setiap aturan menghasilkan nilai tegas $z_i$, proses defuzzifikasi tidak memerlukan integrasi kurva yang rumit:
$$z^* = \frac{\sum_{i=1}^{N} \alpha_i \cdot z_i}{\sum_{i=1}^{N} \alpha_i}$$

---

### 2. Metode Tsukamoto
Pada metode Tsukamoto, setiap aturan memiliki konsekuen berupa himpunan fuzzy yang fungsi keanggotaannya harus **monoton tegas** (selalu naik atau selalu turun).

```text
    Kurva Monoton Naik                              Kurva Monoton Turun
μ(z)                                            μ(z)
1.0 ──────────────┐                             1.0 ──────┐
                 /│                                       │\
                / │                                       │ \
   α ──────────●  │                                α ─────┼──●
              /│  │                                       │ /│
0.0 ─────────┴─┼──┴──────── z                   0.0 ──────┴─┼┴──────── z
             a z* b                                         a z* b
      z* = a + α(b - a)                               z* = b - α(b - a)
```

Untuk setiap aturan $i$:
1. Hitung $\alpha_i$ dari premis antecedent.
2. Cari nilai tegas $z_i$ secara langsung menggunakan fungsi invers keanggotaan: $z_i = \mu^{-1}(\alpha_i)$.
3. Defuzzifikasi akhir dihitung dengan rata-rata terbobot:
   $$z^* = \frac{\sum_{i=1}^{N} \alpha_i \cdot z_i}{\sum_{i=1}^{N} \alpha_i}$$

---

## C. Contoh Perhitungan Manual

### Studi Kasus: Penentuan Bonus Kinerja Tim IT
- **Input 1:** Target Tercapai ($x = 80\%$)
- **Input 2:** Jam Lembur ($y = 10$ jam)
- **Output:** Bonus ($z$ dalam Juta Rupiah)

Fuzzifikasi:
- Target: $\mu_{\text{Cukup}} = 0.4$, $\mu_{\text{Bagus}} = 0.6$
- Lembur: $\mu_{\text{Sedikit}} = 0.2$, $\mu_{\text{Banyak}} = 0.8$

Aturan:
- **R1:** IF Target Cukup AND Lembur Sedikit THEN Bonus ...
  - $\alpha_1 = \min(0.4, 0.2) = 0.2$
- **R2:** IF Target Cukup AND Lembur Banyak THEN Bonus ...
  - $\alpha_2 = \min(0.4, 0.8) = 0.4$
- **R3:** IF Target Bagus AND Lembur Sedikit THEN Bonus ...
  - $\alpha_3 = \min(0.6, 0.2) = 0.2$
- **R4:** IF Target Bagus AND Lembur Banyak THEN Bonus ...
  - $\alpha_4 = \min(0.6, 0.8) = 0.6$

#### 1. Perhitungan Sugeno Orde 0
Konstanta: $z_1 = 2$, $z_2 = 4$, $z_3 = 5$, $z_4 = 8$
$$z^* = \frac{(0.2 \times 2) + (0.4 \times 4) + (0.2 \times 5) + (0.6 \times 8)}{0.2 + 0.4 + 0.2 + 0.6} = \frac{0.4 + 1.6 + 1.0 + 4.8}{1.4} = \frac{7.8}{1.4} = \mathbf{5.571} \text{ Juta}$$

#### 2. Perhitungan Tsukamoto
Monoton naik ($[2, 10]$): $z = 2 + \alpha(10 - 2) = 2 + 8\alpha$
- $z_1 = 2 + 8(0.2) = 3.6$
- $z_2 = 2 + 8(0.4) = 5.2$
- $z_3 = 2 + 8(0.2) = 3.6$
- $z_4 = 2 + 8(0.6) = 6.8$
$$z^* = \frac{(0.2 \times 3.6) + (0.4 \times 5.2) + (0.2 \times 3.6) + (0.6 \times 6.8)}{1.4} = \frac{0.72 + 2.08 + 0.72 + 4.08}{1.4} = \frac{7.60}{1.4} = \mathbf{5.429} \text{ Juta}$$

---

## D. Implementasi dalam Python

Simpan kode pembanding berikut sebagai `pertemuan9_sugeno_tsukamoto.py`:

```python
import numpy as np

# ==========================================================
# 1. IMPLEMENTASI SISTEM SUGENO (ORDE 0 DAN ORDE 1)
# ==========================================================
def hitung_sugeno(alphas, z_values):
    """
    alphas: list firing strength [alpha_1, alpha_2, ...]
    z_values: list output tegas aturan [z_1, z_2, ...]
    """
    alphas = np.array(alphas)
    z_values = np.array(z_values)
    
    total_alpha = np.sum(alphas)
    if total_alpha == 0:
        return 0.0
    return np.sum(alphas * z_values) / total_alpha


# ==========================================================
# 2. IMPLEMENTASI SISTEM TSUKAMOTO
# ==========================================================
def invers_monoton_naik(alpha, a, b):
    """z = a + alpha * (b - a)"""
    return a + alpha * (b - a)


def invers_monoton_turun(alpha, a, b):
    """z = b - alpha * (b - a)"""
    return b - alpha * (b - a)


def hitung_tsukamoto(alphas, fungsi_invers_list):
    """
    fungsi_invers_list: list lambda fungsi invers untuk setiap aturan
    """
    z_values = [func(alpha) for alpha, func in zip(alphas, fungsi_invers_list)]
    return hitung_sugeno(alphas, z_values), z_values


# ==========================================================
# 3. PENGUJIAN DAN KOMPARASI KASUS
# ==========================================================
alphas_kasus = [0.2, 0.4, 0.2, 0.6]

# A. Sugeno Orde 0
z_sugeno0 = [2.0, 4.0, 5.0, 8.0]
hasil_sugeno0 = hitung_sugeno(alphas_kasus, z_sugeno0)

# B. Sugeno Orde 1: z = 0.05*Target + 0.3*Lembur + c
# Misal untuk input Target=80, Lembur=10:
# R1: z1 = 0.03*80 + 0.1*10 + 0.5 = 2.4 + 1.0 + 0.5 = 3.9
# R2: z2 = 0.04*80 + 0.2*10 + 1.0 = 3.2 + 2.0 + 1.0 = 6.2
# R3: z3 = 0.05*80 + 0.1*10 + 1.5 = 4.0 + 1.0 + 1.5 = 6.5
# R4: z4 = 0.06*80 + 0.3*10 + 2.0 = 4.8 + 3.0 + 2.0 = 9.8
z_sugeno1 = [3.9, 6.2, 6.5, 9.8]
hasil_sugeno1 = hitung_sugeno(alphas_kasus, z_sugeno1)

# C. Tsukamoto
fungsi_tsukamoto = [
    lambda a: invers_monoton_naik(a, 2.0, 10.0),
    lambda a: invers_monoton_naik(a, 2.0, 10.0),
    lambda a: invers_monoton_naik(a, 2.0, 10.0),
    lambda a: invers_monoton_naik(a, 2.0, 10.0),
]
hasil_tsukamoto, z_tsuka_values = hitung_tsukamoto(alphas_kasus, fungsi_tsukamoto)

# Cetak Hasil
print("=" * 65)
print("HASIL KOMPARASI METODE SUGENO DAN TSUKAMOTO")
print("=" * 65)
print(f"1. Sugeno Orde 0       : Rp {hasil_sugeno0:.3f} Juta")
print(f"2. Sugeno Orde 1       : Rp {hasil_sugeno1:.3f} Juta")
print(f"3. Tsukamoto           : Rp {hasil_tsukamoto:.3f} Juta (z_rules: {[round(z, 2) for z in z_tsuka_values]})")
print("=" * 65)
```

---

## E. Matriks Perbandingan: Mamdani vs Sugeno vs Tsukamoto

| Kriteria Komparasi | Metode Mamdani | Metode Sugeno (TSK) | Metode Tsukamoto |
|---|---|---|---|
| **Bentuk Konsekuen** | Himpunan Fuzzy (Kurva) | Konstanta (Orde 0) / Fungsi Linear (Orde 1) | Himpunan Fuzzy Monoton |
| **Kecepatan Komputasi** | Lambat (integrasi/resolusi tinggi) | **Sangat Cepat** (aljabar murni) | Cepat (fungsi invers) |
| **Representasi Penalaran** | Sangat alami & intuitif | Kurang intuitif untuk bahasa manusia | Moderat |
| **Cocok untuk** | Sistem Pakar, SPK, Penilaian Kualitatif | Kendali Kontinu, Optimasi, Sistem Real-Time | Sistem dengan tren keputusan monoton |
| **Optimasi Matematika** | Sulit diintegrasikan ke Machine Learning | Mudah digabung dengan Neural Network (ANFIS) | Sulit diotomasi penuh |

---

## F. Tugas Praktikum 9

### Kasus: Sistem Pengaturan Alokasi Bandwidth Dinamis
Dua input:
- `Jumlah Pengguna Aktif` ($0 - 100$ user)
- `Tingkat Trafik Saat Ini` ($0 - 100\%$)
Output: `Alokasi Bandwidth` ($10 - 100$ Mbps).

1. Rancang 4 aturan inferensi.
2. Implementasikan dalam Python menggunakan **Sugeno Orde 0**.
3. Implementasikan dalam Python menggunakan **Metode Tsukamoto**.
4. Ujilah kedua sistem dengan 5 variasi input data beban jaringan.
5. Buat tabel perbandingan hasil alokasi bandwidth kedua metode dan analisislah selisih keputusannya.

---

## G. Pertanyaan Analisis

1. Mengapa metode Sugeno jauh lebih disukai dibandingkan Mamdani pada sistem kontrol industri waktu-nyata (*real-time industrial control*)?
2. Apa syarat mutlak yang harus dipenuhi oleh fungsi keanggotaan konsekuen pada metode Tsukamoto? Mengapa kurva segitiga simetris tidak dapat digunakan sebagai konsekuen Tsukamoto?
3. Pada kondisi apakah metode Sugeno Orde 1 menghasilkan akurasi yang lebih superior dibandingkan Sugeno Orde 0?

---

## H. Ketentuan & Pengumpulan
1. Mahasiswa mengumpulkan file script Python `Modul-2/Praktikum9_<NIM>.py`.
2. Commit git: `feat(modul2): selesaikan metode sugeno dan tsukamoto praktikum 9`.

---

## I. Kesimpulan
Metode Sugeno dan Tsukamoto menawarkan alternatif inferensi berkecepatan komputasi tinggi tanpa memerlukan defuzzifikasi integrasi numerik yang berat. Sugeno sangat unggul dalam aplikasi kontrol teknik dan integrasi sistem cerdas adaptif, sementara Tsukamoto memberikan penalaran transparan berbasis fungsi monotonik terbalik.
