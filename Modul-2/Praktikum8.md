# Praktikum 8 — Metode Mamdani dan Metode Defuzzifikasi
## Implementasi Sistem Inferensi Mamdani (Max-Min) dan Komparasi Metode Defuzzifikasi: Centroid, Bisector, MOM, SOM, dan LOM

---

## A. Tujuan Praktikum
Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:
1. Memahami prinsip kerja metode penalaran inferensi **Mamdani** (*Max-Min*).
2. Melakukan proses implikasi pemotongan kurva (*clipping*) dan agregasi maksimum.
3. Memahami dan mengimplementasikan lima metode defuzzifikasi:
   - **Centroid** (*Center of Gravity - COG*)
   - **Bisector** (*Pembagi Luas Area Seimbang*)
   - **Mean of Maximum (MOM)**
   - **Smallest of Maximum (SOM)**
   - **Largest of Maximum (LOM)**
4. Mengimplementasikan sistem Mamdani menggunakan Python murni dan pustaka `scikit-fuzzy`.
5. Membandingkan sensitivitas nilai output hasil dari masing-masing metode defuzzifikasi.

---

## B. Konsep Dasar

### 1. Karakteristik Metode Mamdani
Metode Mamdani, yang diperkenalkan oleh **Ebrahim Mamdani pada tahun 1975**, adalah metode inferensi fuzzy yang paling intuitif dan banyak digunakan. Ciri khas utama metode Mamdani adalah:
- **Konsekuen Aturan:** Berupa himpunan fuzzy (bukan fungsi linear atau konstanta).
- **Implikasi:** Menggunakan operator *Minimum* untuk memotong fungsi keanggotaan output setinggi $\alpha$-predikat.
- **Agregasi:** Menggabungkan seluruh kurva output menggunakan operator *Maksimum*.
- **Defuzzifikasi:** Memerlukan integrasi numerik untuk menghitung nilai tegas (*crisp*).

$$\mu_{\text{Agg}}(z) = \max_{i} \left[ \min(\alpha_i, \mu_{C_i}(z)) \right]$$

---

## C. Ragam Metode Defuzzifikasi

Setelah kurva agregasi $\mu_{\text{Agg}}(z)$ terbentuk pada semesta output $Z$, terdapat beberapa metode untuk mengambil satu nilai crisp perwakilan ($z^*$):

```text
μ(z)
1.0 ────
0.8 ────             ┌─────────────┐  <--- Wilayah Maksimum (μ = 0.8)
                     │             │
0.4 ────       ┌─────┤             ├─────┐
0.0 ────┴──────┴─────┴─────────────┴─────┴──────┴─── z
              SOM         MOM           LOM
                      ▲          ▲
                   Bisector   Centroid
```

### 1. Centroid (Center of Gravity / COG)
Metode paling populer dan stabil. Menghitung titik pusat berat bidang dua dimensi:
$$z^*_{\text{Centroid}} = \frac{\int z \cdot \mu_{\text{Agg}}(z) \, dz}{\int \mu_{\text{Agg}}(z) \, dz}$$

### 2. Bisector
Mencari nilai $z^*$ yang membagi luas total daerah fuzzy menjadi dua bagian yang sama persis:
$$\int_{-\infty}^{z^*} \mu_{\text{Agg}}(z) \, dz = \int_{z^*}^{\infty} \mu_{\text{Agg}}(z) \, dz$$

### 3. Mean of Maximum (MOM)
Menghitung rata-rata dari semua nilai $z$ yang memiliki derajat keanggotaan maksimum tertinggi ($\mu_{\max}$):
$$z^*_{\text{MOM}} = \frac{\sum_{z \in M} z}{|M|}, \quad \text{di mana } M = \{z \mid \mu(z) = \mu_{\max}\}$$

### 4. Smallest of Maximum (SOM)
Mengambil nilai $z$ terkecil (paling kiri) yang memiliki derajat keanggotaan maksimum:
$$z^*_{\text{SOM}} = \min \{z \mid \mu(z) = \mu_{\max}\}$$

### 5. Largest of Maximum (LOM)
Mengambil nilai $z$ terbesar (paling kanan) yang memiliki derajat keanggotaan maksimum:
$$z^*_{\text{LOM}} = \max \{z \mid \mu(z) = \mu_{\max}\}$$

---

## D. Implementasi dalam Python

### 1. Instalasi Library scikit-fuzzy
```bash
pip install scikit-fuzzy
```

### 2. Kode Program Komparasi Defuzzifikasi
Simpan sebagai `pertemuan8_mamdani_defuzz.py`:

```python
import numpy as np
import matplotlib.pyplot as plt
import skfuzzy as fuzz

# ==========================================================
# 1. DEFINISI SEMESTA DAN BENTUK KURVA AGREGASI
# ==========================================================
# Semesta output: Tingkat Risiko Keamanan TI [0 - 100%]
z = np.linspace(0, 100, 1000)

# Bentuk fungsi keanggotaan output
mf_rendah = fuzz.trapmf(z, [0, 0, 20, 40])
mf_sedang = fuzz.trimf(z, [30, 50, 70])
mf_tinggi = fuzz.trapmf(z, [60, 80, 100, 100])

# Simulasi Firing Strength dari aturan
alpha_rendah = 0.3
alpha_sedang = 0.7
alpha_tinggi = 0.5

# Implikasi Min
imp_rendah = np.fmin(alpha_rendah, mf_rendah)
imp_sedang = np.fmin(alpha_sedang, mf_sedang)
imp_tinggi = np.fmin(alpha_tinggi, mf_tinggi)

# Agregasi Max
agregasi = np.fmax(imp_rendah, np.fmax(imp_sedang, imp_tinggi))


# ==========================================================
# 2. PERHITUNGAN 5 METODE DEFUZZIFIKASI DENGAN SCIKIT-FUZZY
# ==========================================================
defuzz_methods = ['centroid', 'bisector', 'mom', 'som', 'lom']
hasil_defuzz = {}

for method in defuzz_methods:
    val = fuzz.defuzz(z, agregasi, method)
    hasil_defuzz[method] = val


# ==========================================================
# 3. MENAMPILKAN HASIL DAN VISUALISASI
# ==========================================================
print("=" * 60)
print("HASIL KOMPARASI METODE DEFUZZIFIKASI MAMDANI")
print("=" * 60)
for m, v in hasil_defuzz.items():
    print(f" - Metode {m.upper():<10} : {v:.3f}%")
print("=" * 60)

plt.figure(figsize=(12, 6.5))
plt.plot(z, agregasi, 'b', linewidth=2.5, label='Kurva Agregasi Fuzzy')
plt.fill_between(z, 0, agregasi, color='skyblue', alpha=0.4)

colors = {
    'centroid': 'red',
    'bisector': 'purple',
    'mom': 'black',
    'som': 'green',
    'lom': 'orange'
}

for method, val in hasil_defuzz.items():
    plt.axvline(x=val, color=colors[method], linestyle='--', linewidth=2, 
                label=f'{method.upper()} ({val:.2f})')
    # Ambil nilai mu pada titik tersebut
    idx = np.abs(z - val).argmin()
    plt.scatter([val], [agregasi[idx]], color=colors[method], s=60, zorder=6)

plt.title('Perbandingan 5 Metode Defuzzifikasi pada Metode Mamdani', fontsize=13, fontweight='bold')
plt.xlabel('Tingkat Risiko Keamanan (%)', fontsize=11)
plt.ylabel('Derajat Keanggotaan μ(z)', fontsize=11)
plt.ylim(-0.05, 1.05)
plt.grid(True, linestyle=':', alpha=0.6)
plt.legend(loc='upper right', fontsize=10)
plt.tight_layout()

plt.savefig('komparasi_metode_defuzzifikasi.png', dpi=300)
plt.show()
```

---

## E. Analisis Hasil Komparasi Metode

| Metode | Nilai Output Tipikal | Karakteristik Utama | Rekomendasi Kasus |
|---|:---:|---|---|
| **Centroid (COG)** | $\approx 54.2\%$ | Halus, kontinu, mempertimbangkan seluruh luas kurva | Sistem kendali otomatis, penilaian performa |
| **Bisector** | $\approx 53.8\%$ | Membagi massa area seimbang, mirip centroid | Sistem keseimbangan, alokasi sumber daya |
| **MOM** | $\approx 50.0\%$ | Mengambil titik tengah dari puncak tertinggi | Sistem klasifikasi yang mengutamakan keyakinan tertinggi |
| **SOM** | $\approx 46.5\%$ | Memilih batas bawah dari daerah puncak | Sistem konservatif (contoh: estimasi pengeluaran minimum) |
| **LOM** | $\approx 53.5\%$ | Memilih batas atas dari daerah puncak | Sistem *fail-safe* (contoh: alarm bahaya, firewall security) |

---

## F. Tugas Praktikum 8

### Studi Kasus: Penilaian Kualitas Sinyal WiFi Kampus
Variabel Output: `Kualitas Sinyal` ($0 - 100$ dBm ekuivalen).
1. Rancang 3 fungsi keanggotaan output: `Jelek` (trapesium $[0, 0, 25, 45]$), `Sedang` (segitiga $[35, 55, 75]$), `Bagus` (trapesium $[65, 85, 100, 100]$).
2. Simulasikan kondisi firing rules:
   - $\alpha_{\text{Jelek}} = 0.5$
   - $\alpha_{\text{Sedang}} = 0.8$
   - $\alpha_{\text{Bagus}} = 0.2$
3. Hitung hasil defuzzifikasi menggunakan kelima metode di atas.
4. Buat tabel perbandingannya dan grafik visualisasi.
5. Manakah metode yang paling aman dipilih oleh administrator jaringan jika tujuannya adalah menjamin sinyal tidak terputus? Jelaskan alasannya.

---

## G. Pertanyaan Analisis

1. Mengapa metode Centroid memiliki komputasi yang lebih berat dibandingkan MOM pada mikrokontroler atau sistem berdaya rendah (*embedded systems*)?
2. Dalam skenario darurat (*emergency braking system* pada mobil otonom), metode manakah antara SOM dan LOM yang lebih tepat digunakan untuk menentukan besarnya gaya rem? Jelaskan implikasi keselamatannya!
3. Jika kurva agregasi memiliki dua puncak terpisah yang simetris (bimodal distribution), apakah kelemahan metode MOM?

---

## H. Ketentuan & Pengumpulan
1. Mahasiswa mengumpulkan script Python `Modul-2/Praktikum8_<NIM>.py` dan gambar grafik.
2. Commit git: `feat(modul2): selesaikan metode mamdani dan 5 metode defuzzifikasi praktikum 8`.

---

## I. Kesimpulan
Metode Mamdani memberikan representasi penalaran manusia yang alami dengan konsekuen berbentuk himpunan fuzzy. Pemilihan metode defuzzifikasi yang tepat (Centroid, Bisector, MOM, SOM, atau LOM) memungkinkan perancang sistem menyesuaikan profil keputusan: apakah netral-kontinu, konservatif, agresif, atau mengutamakan titik kepastian tertinggi.
