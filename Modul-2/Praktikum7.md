# Praktikum 7 — Arsitektur Fuzzy Inference System (FIS)
## Alur Kerja Komprehensif Sistem Inferensi Fuzzy: Fuzzifikasi, Evaluasi Aturan, Agregasi, dan Defuzzifikasi

---

## A. Tujuan Praktikum
Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:
1. Memahami arsitektur lengkap dan empat pilar utama *Fuzzy Inference System* (FIS).
2. Menjelaskan aliran transformasi data: dari nilai konkret (*crisp input*) $\to$ derajat keanggotaan $\to$ evaluasi aturan $\to$ agregasi konsekuen $\to$ keputusan konkret (*crisp output*).
3. Mengimplementasikan pipeline pemrosesan FIS secara modular menggunakan Python.
4. Memvisualisasikan setiap tahap komputasi inferensi fuzzy dalam bentuk grafik proses.
5. Menganalisis pengaruh agregasi konklusi terhadap bentuk daerah solusi fuzzy sebelum proses defuzzifikasi.

---

## B. Konsep Dasar

### 1. Arsitektur Empat Pilar Fuzzy Inference System
Fuzzy Inference System (FIS) adalah kerangka kerja komputasi cerdas yang memetakan ruang input ke ruang output menggunakan penalaran berbasis aturan fuzzy. FIS terdiri dari empat komponen utama:

```text
┌──────────────────────────────────────────────────────────────────────────────────┐
│                          FUZZY INFERENCE SYSTEM (FIS)                            │
│                                                                                  │
│   INPUT CRISP                                                     OUTPUT CRISP   │
│       │                                                                ▲         │
│       ▼                                                                │         │
│ ┌───────────┐         ┌─────────────────────┐                    ┌───────────┐   │
│ │           │         │ INFERENCE ENGINE    │                    │           │   │
│ │  FUZZI-   │ ──────► │ (Penalaran Aturan   │ ─────────────────► │  DEFUZZI- │   │
│ │  FIKASI   │         │  dan Agregasi)      │                    │  FIKASI   │   │
│ └───────────┘         └─────────────────────┘                    └───────────┘   │
│                                  ▲                                               │
│                                  │                                               │
│                       ┌─────────────────────┐                                    │
│                       │   KNOWLEDGE BASE    │                                    │
│                       │ (Rule Base &        │                                    │
│                       │  Database MF)       │                                    │
│                       └─────────────────────┘                                    │
└──────────────────────────────────────────────────────────────────────────────────┘
```

1. **Basis Pengetahuan (*Knowledge Base*):** Berisi definisi fungsi keanggotaan seluruh variabel (*Database*) dan kumpulan aturan IF-THEN (*Rule Base*).
2. **Unit Fuzzifikasi (*Fuzzification Interface*):** Mengubah nilai input crisp menjadi derajat keanggotaan linguistik $\mu \in [0, 1]$.
3. **Mesin Inferensi (*Inference Engine*):** Menerapkan operator logika fuzzy pada premis aturan, menerapkan metode implikasi (misal: pemotongan kurva/Mamdani Min), dan menggabungkan hasil seluruh aturan aktif ke dalam satu fungsi keanggotaan gabungan (*Aggregation*).
4. **Unit Defuzzifikasi (*Defuzzification Interface*):** Mengubah daerah himpunan fuzzy hasil agregasi kembali menjadi satu nilai tegas (*crisp output*), misalnya melalui metode titik berat (*Centroid*).

---

## C. Alur Komputasi Step-by-Step

Misalkan terdapat sistem rekomendasi diskon layanan TI dengan:
- **Input 1:** Lama Langganan ($x_1 = 15$ bulan)
- **Input 2:** Frekuensi Transaksi ($x_2 = 8$ kali/bulan)
- **Output:** Besaran Diskon ($z$ dalam persen)

### Tahap 1: Fuzzifikasi
Setiap input dipetakan ke fungsi keanggotaan masing-masing:
- $x_1 = 15 \implies \mu_{\text{Baru}} = 0.0, \quad \mu_{\text{Lama}} = 0.75$
- $x_2 = 8 \implies \mu_{\text{Jarang}} = 0.20, \quad \mu_{\text{Sering}} = 0.80$

### Tahap 2: Evaluasi Aturan & Implikasi
Misalkan terdapat 2 aturan aktif:
- **Rule 1:** $\textbf{IF } \text{Lama is Lama AND Frekuensi is Jarang} \textbf{ THEN } \text{Diskon is Sedang}$
  $$\alpha_1 = \min(\mu_{\text{Lama}}, \mu_{\text{Jarang}}) = \min(0.75, 0.20) = \mathbf{0.20}$$
  *Implikasi:* Kurva output `Diskon Sedang` dipotong setinggi $\alpha_1 = 0.20$.
- **Rule 2:** $\textbf{IF } \text{Lama is Lama AND Frekuensi is Sering} \textbf{ THEN } \text{Diskon is Besar}$
  $$\alpha_2 = \min(\mu_{\text{Lama}}, \mu_{\text{Sering}}) = \min(0.75, 0.80) = \mathbf{0.75}$$
  *Implikasi:* Kurva output `Diskon Besar` dipotong setinggi $\alpha_2 = 0.75$.

### Tahap 3: Agregasi (Max Operator)
Menggabungkan seluruh kurva terpotong dari Rule 1 dan Rule 2 menggunakan operator maksimum:
$$\mu_{\text{Agg}}(z) = \max(\mu_{\text{Rule1}}(z), \mu_{\text{Rule2}}(z))$$

```text
       Implikasi Rule 1 (Sedang)       Implikasi Rule 2 (Besar)              Hasil Agregasi
μ(z)                            μ(z)                            μ(z)
1.0 ────                        1.0 ────                        1.0 ────
                                0.75───  ┌───┐                  0.75───  ┌───┐
0.20───  ┌───┐                                                  0.20─── ┌┴───┤
0.0 ────┴─────┴───              0.0 ────┴─────┴───              0.0 ───┴──────┴───
```

### Tahap 4: Defuzzifikasi (Centroid)
Menghitung titik pusat massa (*Center of Gravity*) dari kurva agregasi:
$$z^* = \frac{\int z \cdot \mu_{\text{Agg}}(z) \, dz}{\int \mu_{\text{Agg}}(z) \, dz} \approx \frac{\sum z_i \cdot \mu_{\text{Agg}}(z_i)}{\sum \mu_{\text{Agg}}(z_i)}$$

---

## D. Implementasi Pipeline FIS dalam Python

Simpan kode modular berikut sebagai `pertemuan7_pipeline_fis.py`:

```python
import numpy as np
import matplotlib.pyplot as plt

# ==========================================================
# 1. DEFINISI FUNGSI KEANGGOTAAN SEGI TIGA & TRAPESIUM
# ==========================================================
def trimf(x, params):
    """Fungsi keanggotaan segitiga [a, b, c]"""
    a, b, c = params
    y = np.zeros_like(x)
    idx1 = (x > a) & (x <= b)
    if np.any(idx1) and b != a:
        y[idx1] = (x[idx1] - a) / (b - a)
    idx2 = (x > b) & (x < c)
    if np.any(idx2) and c != b:
        y[idx2] = (c - x[idx2]) / (c - b)
    return np.clip(y, 0.0, 1.0)


# ==========================================================
# 2. DEFINISI DOMAIN DAN SEMESTA
# ==========================================================
# Domain Output: Besaran Diskon [0 - 30%]
z = np.linspace(0, 30, 300)

mf_diskon_kecil = trimf(z, [0, 5, 12])
mf_diskon_sedang = trimf(z, [8, 15, 22])
mf_diskon_besar = trimf(z, [18, 25, 30])


# ==========================================================
# 3. SIMULASI NILAI FIRING STRENGTH DARI ATURAN
# ==========================================================
# Misal hasil evaluasi aturan menghasilkan:
alpha_kecil = 0.00
alpha_sedang = 0.20
alpha_besar = 0.75

# Implikasi (Mamdani Min)
imp_kecil = np.minimum(alpha_kecil, mf_diskon_kecil)
imp_sedang = np.minimum(alpha_sedang, mf_diskon_sedang)
imp_besar = np.minimum(alpha_besar, mf_diskon_besar)

# Agregasi (Max)
agregasi = np.maximum(imp_kecil, np.maximum(imp_sedang, imp_besar))


# ==========================================================
# 4. DEFUZZIFIKASI CENTROID (DISKRIT)
# ==========================================================
def defuzzifikasi_centroid(x_vals, mu_vals):
    total_mu = np.sum(mu_vals)
    if total_mu == 0:
        return 0.0
    return np.sum(x_vals * mu_vals) / total_mu

z_crisp = defuzzifikasi_centroid(z, agregasi)


# ==========================================================
# 5. VISUALISASI PIPELINE FIS
# ==========================================================
plt.figure(figsize=(12, 6))

plt.plot(z, mf_diskon_kecil, 'g--', label='MF Kecil', alpha=0.5)
plt.plot(z, mf_diskon_sedang, 'b--', label='MF Sedang', alpha=0.5)
plt.plot(z, mf_diskon_besar, 'r--', label='MF Besar', alpha=0.5)

# Gambar kurva terpotong & area agregasi
plt.fill_between(z, 0, agregasi, color='purple', alpha=0.35, label='Daerah Agregasi Fuzzy')
plt.plot(z, agregasi, color='purple', linewidth=2.5)

# Garis titik berat hasil defuzzifikasi
plt.axvline(x=z_crisp, color='black', linewidth=2.5, linestyle='-', 
            label=f'Crisp Output (Centroid = {z_crisp:.2f}%)')
plt.scatter([z_crisp], [0], color='black', s=80, zorder=6)

plt.title('Arsitektur FIS: Hasil Implikasi, Agregasi, dan Defuzzifikasi Centroid', fontsize=13, fontweight='bold')
plt.xlabel('Besaran Diskon (%)', fontsize=11)
plt.ylabel('Derajat Keanggotaan μ(z)', fontsize=11)
plt.ylim(-0.05, 1.05)
plt.grid(True, linestyle=':', alpha=0.6)
plt.legend(loc='upper left', fontsize=10)
plt.tight_layout()

plt.savefig('pipeline_fis_agregasi_defuzzifikasi.png', dpi=300)
plt.show()

print(f"Keputusan Akhir Sistem FIS:")
print(f" - Rekomendasi Diskon: {z_crisp:.2f}%")
```

---

## E. Tugas Praktikum 7

### Menggabungkan Fuzzifikasi, Evaluasi Aturan, dan Defuzzifikasi Menjadi Satu Fungsi Utuh
1. Bangun kelas `FuzzyInferenceSystem` yang memiliki metode:
   - `add_input_variable(name, universe, mf_dict)`
   - `set_output_variable(name, universe, mf_dict)`
   - `add_rule(rule_tuple)`
   - `compute(input_values_dict)` $\to$ mengembalikan nilai crisp output.
2. Ujilah sistem dengan 3 kombinasi input lama langganan dan frekuensi transaksi:
   - Kasus 1: Lama $= 3$ bulan, Frekuensi $= 2$ kali
   - Kasus 2: Lama $= 12$ bulan, Frekuensi $= 6$ kali
   - Kasus 3: Lama $= 24$ bulan, Frekuensi $= 15$ kali
3. Catat nilai output diskon persen untuk setiap kasus.

---

## F. Pertanyaan Analisis

1. Mengapa FIS memerlukan tahap defuzzifikasi? Mengapa sistem kontrol atau pengambil keputusan tidak dapat langsung menggunakan fungsi keanggotaan agregasi fuzzy?
2. Apa perbedaan utama antara metode implikasi **Clipping (Min)** dan **Scaling (Product)**? Bagaimana pengaruh masing-masing terhadap bentuk kurva agregasi?
3. Jika pada tahap agregasi seluruh nilai $\alpha = 0$, apa yang terjadi pada rumus Centroid $\frac{\sum z \mu}{\sum \mu}$? Bagaimana strategi penanganan kesalahan (*fallback mechanism*) yang tepat?

---

## G. Ketentuan & Pengumpulan
1. File yang dikumpulkan: `Modul-2/Praktikum7_<NIM>.py` beserta screenshot grafik agregasi.
2. Pesan commit: `feat(modul2): selesaikan arsitektur dan pipeline FIS praktikum 7`.

---

## H. Kesimpulan
Fuzzy Inference System mengintegrasikan fuzzifikasi, rule base, implikasi, agregasi, dan defuzzifikasi menjadi satu kesatuan mesin inferensi yang utuh. Melalui arsitektur ini, input dunia nyata yang bersifat ambigu dapat diolah secara deterministik menjadi keputusan konkret yang dapat diimplementasikan pada aktuator, antarmuka pengguna, maupun modul sistem informasi.
