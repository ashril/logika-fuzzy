# Praktikum 4 — Operasi Himpunan Fuzzy
## Operasi Union, Intersection, Complement, T-Norm, dan T-Conorm Menggunakan Python

---

## A. Tujuan Praktikum
Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:
1. Memahami konsep matematis operasi dasar himpunan fuzzy: Union (Gabungan/OR), Intersection (Irisan/AND), dan Complement (Komplemen/NOT).
2. Membedakan operator standar Zadeh (*Min-Max*) dengan keluarga operator **T-norm** (*Triangular Norm*) dan **T-conorm** (*Triangular Co-norm*).
3. Mengimplementasikan operasi logika fuzzy menggunakan pustaka `NumPy`.
4. Memvisualisasikan hasil operasi multi-himpunan fuzzy menggunakan `Matplotlib`.
5. Menganalisis dampak pemilihan operator terhadap sensitivitas keputusan dalam skenario multikriteria bidang Teknologi Informasi.

---

## B. Konsep Dasar

### 1. Operasi Standar Zadeh
Pada teori himpunan klasik, operasi gabungan dan irisan didasarkan pada aljabar Boolean. Pada himpunan fuzzy, **Lotfi A. Zadeh (1965)** merumuskan operasi dasar derajat keanggotaan untuk dua himpunan fuzzy $A$ dan $B$ pada semesta $X$:

1. **Intersection (Irisan / AND):** Mengambil nilai derajat minimum.
   $$\mu_{A \cap B}(x) = \min(\mu_A(x), \mu_B(x))$$

2. **Union (Gabungan / OR):** Mengambil nilai derajat maksimum.
   $$\mu_{A \cup B}(x) = \max(\mu_A(x), \mu_B(x))$$

3. **Complement (Komplemen / NOT):** Mengurangkan nilai keanggotaan dari 1.
   $$\mu_{\neg A}(x) = 1 - \mu_A(x)$$

```text
       INTERSECTION (AND / MIN)                      UNION (OR / MAX)
μ(x)                                        μ(x)
1.0 ───┐             ┌───                   1.0 ───┐  ▲▲▲▲▲▲▲▲▲  ┌───
       │\           /│                             │\/         \/│
       │ \   ▲▲▲   / │                             │/           \│
       │  \ /   \ /  │                             /             \
0.0 ───┴───X─────X───┴───                   0.0 ──┴───────────────┴───
           Daerah Min                                Daerah Max
```

### 2. Keluarga Operator T-Norm dan T-Conorm
Selain operator Zadeh standar, terdapat variasi operator t-norm (untuk irisan/AND) dan t-conorm (untuk gabungan/OR) yang sering digunakan dalam sistem inferensi:

| Operasi | Jenis Operator | Rumus Matematis | Karakteristik |
|---|---|---|---|
| **AND** | **Standard Zadeh (Min)** | $\min(\mu_A, \mu_B)$ | Paling konservatif, tidak terpengaruh selisih kecil |
| **AND** | **Algebraic Product** | $\mu_A \cdot \mu_B$ | Menghasilkan nilai lebih ketat/rendah saat kedua operand $< 1$ |
| **AND** | **Bounded Difference (Lukasiewicz)** | $\max(0, \mu_A + \mu_B - 1)$ | Paling drastis, bernilai 0 jika jumlah derajat $\le 1$ |
| **OR** | **Standard Zadeh (Max)** | $\max(\mu_A, \mu_B)$ | Memilih derajat tertinggi dari salah satu kriteria |
| **OR** | **Algebraic Sum (Probabilistic Sum)** | $\mu_A + \mu_B - (\mu_A \cdot \mu_B)$ | Memperhitungkan kontribusi kedua operand |
| **OR** | **Bounded Sum (Lukasiewicz)** | $\min(1, \mu_A + \mu_B)$ | Meningkat secara linear hingga mencapai saturasi 1 |

---

## C. Contoh Perhitungan Manual

Misalkan terdapat evaluasi kualitas server dengan dua parameter:
- $\mu_{\text{Koneksi Stabil}} = 0.80$
- $\mu_{\text{Latensi Rendah}} = 0.60$

Mari hitung nilai keanggotaan gabungan kedua parameter:

1. **Intersection (Server Prima = Stabil AND Latensi Rendah):**
   - **Zadeh Min:** $\min(0.80, 0.60) = \mathbf{0.60}$
   - **Algebraic Product:** $0.80 \times 0.60 = \mathbf{0.48}$
   - **Bounded Difference:** $\max(0, 0.80 + 0.60 - 1) = \max(0, 0.40) = \mathbf{0.40}$

2. **Union (Server Layak Pakai = Stabil OR Latensi Rendah):**
   - **Zadeh Max:** $\max(0.80, 0.60) = \mathbf{0.80}$
   - **Algebraic Sum:** $0.80 + 0.60 - (0.80 \times 0.60) = 1.40 - 0.48 = \mathbf{0.92}$
   - **Bounded Sum:** $\min(1, 0.80 + 0.60) = \min(1, 1.40) = \mathbf{1.00}$

---

## D. Implementasi dalam Python

Simpan kode program berikut sebagai `pertemuan4_operasi_fuzzy.py`:

```python
import numpy as np
import matplotlib.pyplot as plt

# ==========================================================
# 1. IMPLEMENTASI OPERATOR T-NORM (AND)
# ==========================================================
def tnorm_min(mu_a, mu_b):
    """Zadeh Min: min(A, B)"""
    return np.minimum(mu_a, mu_b)


def tnorm_product(mu_a, mu_b):
    """Algebraic Product: A * B"""
    return mu_a * mu_b


def tnorm_bounded_diff(mu_a, mu_b):
    """Bounded Difference: max(0, A + B - 1)"""
    return np.maximum(0.0, mu_a + mu_b - 1.0)


# ==========================================================
# 2. IMPLEMENTASI OPERATOR T-CONORM (OR)
# ==========================================================
def tconorm_max(mu_a, mu_b):
    """Zadeh Max: max(A, B)"""
    return np.maximum(mu_a, mu_b)


def tconorm_algebraic_sum(mu_a, mu_b):
    """Algebraic Sum: A + B - (A * B)"""
    return mu_a + mu_b - (mu_a * mu_b)


def tconorm_bounded_sum(mu_a, mu_b):
    """Bounded Sum: min(1, A + B)"""
    return np.minimum(1.0, mu_a + mu_b)


# ==========================================================
# 3. IMPLEMENTASI KOMPLEMEN (NOT)
# ==========================================================
def fuzzy_not(mu):
    """Zadeh Complement: 1 - mu"""
    return 1.0 - mu


# ==========================================================
# 4. SIMULASI DUA FUNGSI KEANGGOTAAN
# ==========================================================
x = np.linspace(0, 10, 500)

# Himpunan A: Segitiga di kiri [1, 3, 6]
mu_a = np.maximum(0.0, np.minimum((x - 1.0) / (3.0 - 1.0), (6.0 - x) / (6.0 - 3.0)))

# Himpunan B: Segitiga di kanan [4, 7, 9]
mu_b = np.maximum(0.0, np.minimum((x - 4.0) / (7.0 - 4.0), (9.0 - x) / (9.0 - 7.0)))


# ==========================================================
# 5. VISUALISASI KOMPARASI OPERASI
# ==========================================================
fig, axes = plt.subplots(2, 2, figsize=(14, 9))

# Panel 1: Himpunan Dasar A, B dan Not A
axes[0, 0].plot(x, mu_a, label='Himpunan A', color='#1f77b4', linewidth=2.5)
axes[0, 0].plot(x, mu_b, label='Himpunan B', color='#ff7f0e', linewidth=2.5)
axes[0, 0].plot(x, fuzzy_not(mu_a), label='NOT A (Komplemen)', color='gray', linestyle='--', linewidth=1.8)
axes[0, 0].set_title('1. Himpunan A, B, dan Komplemen NOT A', fontweight='bold')
axes[0, 0].set_ylim(-0.05, 1.1)
axes[0, 0].grid(True, linestyle=':', alpha=0.6)
axes[0, 0].legend()

# Panel 2: Komparasi Operator Intersection (T-Norm)
axes[0, 1].plot(x, tnorm_min(mu_a, mu_b), label='Zadeh Min (Standar)', color='#2ca02c', linewidth=2.5)
axes[0, 1].plot(x, tnorm_product(mu_a, mu_b), label='Algebraic Product', color='#d62728', linestyle='-.', linewidth=2)
axes[0, 1].plot(x, tnorm_bounded_diff(mu_a, mu_b), label='Bounded Diff', color='#9467bd', linestyle=':', linewidth=2)
axes[0, 1].set_title('2. Operasi Intersection (AND / T-Norm)', fontweight='bold')
axes[0, 1].set_ylim(-0.05, 1.1)
axes[0, 1].grid(True, linestyle=':', alpha=0.6)
axes[0, 1].legend()

# Panel 3: Komparasi Operator Union (T-Conorm)
axes[1, 0].plot(x, tconorm_max(mu_a, mu_b), label='Zadeh Max (Standar)', color='#2ca02c', linewidth=2.5)
axes[1, 0].plot(x, tconorm_algebraic_sum(mu_a, mu_b), label='Algebraic Sum', color='#d62728', linestyle='-.', linewidth=2)
axes[1, 0].plot(x, tconorm_bounded_sum(mu_a, mu_b), label='Bounded Sum', color='#9467bd', linestyle=':', linewidth=2)
axes[1, 0].set_title('3. Operasi Union (OR / T-Conorm)', fontweight='bold')
axes[1, 0].set_ylim(-0.05, 1.1)
axes[1, 0].grid(True, linestyle=':', alpha=0.6)
axes[1, 0].legend()

# Panel 4: Perbandingan Daerah Area Min vs Max
axes[1, 1].fill_between(x, tnorm_min(mu_a, mu_b), color='#2ca02c', alpha=0.4, label='Area Min (A ∩ B)')
axes[1, 1].plot(x, tconorm_max(mu_a, mu_b), color='#d62728', linewidth=2, label='Batas Max (A ∪ B)')
axes[1, 1].plot(x, mu_a, color='#1f77b4', linestyle=':', alpha=0.7)
axes[1, 1].plot(x, mu_b, color='#ff7f0e', linestyle=':', alpha=0.7)
axes[1, 1].set_title('4. Hubungan Area Irisan vs Gabungan Standar', fontweight='bold')
axes[1, 1].set_ylim(-0.05, 1.1)
axes[1, 1].grid(True, linestyle=':', alpha=0.6)
axes[1, 1].legend()

plt.tight_layout()
plt.savefig('operasi_himpunan_fuzzy_komparasi.png', dpi=300)
plt.show()
```

---

## E. Skenario Pengujian Operasi Numerik

Tabel berikut menunjukkan hasil evaluasi beberapa pasangan derajat keanggotaan $(\mu_A, \mu_B)$:

| Kasus | $\mu_A$ | $\mu_B$ | Min | Product | Bounded Diff | Max | Alg. Sum | Bounded Sum |
|:--:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 1 | 0.90 | 0.90 | 0.90 | 0.81 | 0.80 | 0.90 | 0.99 | 1.00 |
| 2 | 0.70 | 0.40 | 0.40 | 0.28 | 0.10 | 0.70 | 0.82 | 1.00 |
| 3 | 0.50 | 0.50 | 0.50 | 0.25 | 0.00 | 0.50 | 0.75 | 1.00 |
| 4 | 0.30 | 0.20 | 0.20 | 0.06 | 0.00 | 0.30 | 0.44 | 0.50 |
| 5 | 0.00 | 0.85 | 0.00 | 0.00 | 0.00 | 0.85 | 0.85 | 0.85 |

---

## F. Tugas Praktikum 4

### Kasus: Evaluasi Kelayakan Bandwidth Jaringan Kampus
Dua kriteria fuzzy dievaluasi untuk menentukan kualitas bandwidth:
- Himpunan $A$ (*Ketersediaan Bandwidth Cukup*): semesta $[0, 100]$ Mbps.
  - Model segitiga: $[30, 60, 90]$.
- Himpunan $B$ (*Packet Loss Rendah*): semesta $[0, 100]$ Mbps throughput efektif.
  - Model trapesium: $[40, 55, 75, 95]$.

**Instruksi Pengerjaan:**
1. Bangun fungsi keanggotaan $A$ dan $B$ pada semesta $X = [0, 100]$.
2. Hitung dan plot:
   - Operasi Irisan menggunakan **Zadeh Min** dan **Algebraic Product**.
   - Operasi Gabungan menggunakan **Zadeh Max** dan **Algebraic Sum**.
   - Operasi Komplemen $\neg A$.
3. Uji pada 4 nilai throughput: $35, 50, 65, 80$ Mbps. Catat derajat keanggotaannya ke dalam tabel perbandingan.
4. Buat kesimpulan tentang operator mana yang paling tepat jika kebijakan kampus menginginkan kriteria seleksi yang ketat.

---

## G. Pertanyaan Analisis

1. Mengapa nilai hasil operasi *Intersection* tidak pernah lebih besar daripada nilai terkecil operand-nya? Buktikan secara matematis!
2. Dalam sistem rekomendasi produk e-commerce, kapankah sebaiknya kita menggunakan operator **Algebraic Product** alih-alih **Zadeh Min** pada aturan: *"IF harga murah AND rating tinggi"*?
3. Pada tabel pengujian kasus 3 ($\mu_A = 0.5, \mu_B = 0.5$), nilai *Bounded Difference* menghasilkan 0.00, sedangkan *Min* menghasilkan 0.50. Mengapa perbedaan ini bisa begitu signifikan?
4. Apakah hukum De Morgan berlaku pada himpunan fuzzy? Jelaskan:
   $$\neg(A \cup B) = \neg A \cap \neg B$$

---

## H. Ketentuan & Pengumpulan
1. Mahasiswa membuat script Python dan laporan praktikum.
2. Simpan di folder repositori masing-masing: `Modul-1/Praktikum4_<NIM>.py` atau `.ipynb`.
3. Commit git: `feat(modul1): selesaikan tugas praktikum 4 operasi himpunan fuzzy`.

---

## I. Kesimpulan
Operasi himpunan fuzzy memungkinkan penggabungan berbagai kondisi kebenaran parsial menjadi satu kesimpulan logis. Pemilihan antara standar Zadeh, aljabar, atau bounded norm memberikan fleksibilitas kepada perancang sistem untuk menyesuaikan derajat toleransi dan keketatan (*strictness*) dalam penalaran sistem fuzzy.
