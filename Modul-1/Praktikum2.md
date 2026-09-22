# Praktikum 2 — Himpunan Fuzzy dan Variabel Linguistik
## Semesta Pembicaraan, Domain Nilai, Variabel Linguistik, dan Fuzzifikasi Sederhana

---

## A. Tujuan Praktikum
Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:
1. Memahami konsep semesta pembicaraan (*universe of discourse*), domain nilai, dan batas himpunan fuzzy.
2. Mendefinisikan variabel linguistik beserta term/label linguistik yang merepresentasikan permasalahan nyata.
3. Merancang struktur data variabel linguistik dalam Python menggunakan kamus (*dictionary*) dan fungsi.
4. Memvisualisasikan multi-label himpunan fuzzy dalam satu semesta pembicaraan menggunakan `Matplotlib`.
5. Melakukan proses fuzzifikasi sederhana terhadap data input crisp untuk menentukan derajat keanggotaan pada setiap label linguistik.
6. Menganalisis fenomena tumpang tindih (*overlapping*) antar-label linguistik dan interpretasi label dominan.

---

## B. Konsep Dasar

### 1. Komponen Variabel Linguistik
Dalam logika fuzzy, variabel yang digunakan dalam pemodelan disebut **Variabel Linguistik** (*Linguistic Variable*). Berbeda dengan variabel komputasi konvensional yang bernilai angka riil, variabel linguistik memiliki nilai berupa kata-kata atau kalimat dalam bahasa alami.

Variabel linguistik secara formal didefinisikan oleh kuintupel $(x, T(x), U, G, M)$:
1. **Nama Variabel ($x$):** Nama konsep yang diamati, misalnya `Waktu Respons`.
2. **Kumpulan Term / Label Linguistik ($T(x)$):** Himpunan kata sifat yang merepresentasikan keadaan variabel, misalnya $\{\text{Cepat}, \text{Sedang}, \text{Lambat}\}$.
3. **Semesta Pembicaraan ($U$):** Rentang nilai numerik riil total yang mungkin dimiliki variabel, misalnya $U = [0, 10]$ detik.
4. **Aturan Sintaktis ($G$):** Tata bahasa untuk membentuk nama label baru (misal: *sangat cepat*, *agak lambat*).
5. **Aturan Semantis ($M$):** Pemetaan matematis dari setiap label ke fungsi keanggotaannya pada semesta $U$.

```text
Variabel Linguistik: WAKTU RESPONS (Semesta U: [0, 10] detik)

μ(x)
1.0 ──────┐               ▲               ┌──────
          │\             / \             /│
          │ \           /   \           / │
          │  \         /     \         /  │
          │   \       /       \       /   │
0.0 ──────┴────\─────/─────────\─────/────┴──────
          0     2   3     5     7   8     10    Detik
          
       [ CEPAT ]       [ SEDANG ]     [ LAMBAT ]
```

### 2. Domain Nilai Himpunan Fuzzy
- **Domain** adalah rentang nilai pada semesta pembicaraan yang memiliki derajat keanggotaan lebih besar dari 0 ($\mu(x) > 0$).
- Daerah tumpang tindih (*overlap*) antara dua kurva yang bersebelahan sangat penting dalam fuzzy untuk menjamin bahwa tidak ada nilai input yang kehilangan representasi linguistiknya.

---

## C. Perhitungan Fuzzifikasi Manual

Misalkan variabel `Waktu Respons` memiliki semesta $U = [0, 10]$ detik dengan tiga label yang didefinisikan sebagai berikut:

1. **Label `Cepat` (Bahu Kiri / Trapesium Turun):**
   $$\mu_{\text{Cepat}}(x) = \begin{cases} 
   1, & x \le 2 \\ 
   \dfrac{4 - x}{4 - 2} = \dfrac{4 - x}{2}, & 2 < x < 4 \\ 
   0, & x \ge 4 
   \end{cases}$$

2. **Label `Sedang` (Segitiga):**
   Titik acuan: $(a=3, b=5, c=7)$
   $$\mu_{\text{Sedang}}(x) = \begin{cases} 
   0, & x \le 3 \text{ atau } x \ge 7 \\ 
   \dfrac{x - 3}{5 - 3} = \dfrac{x - 3}{2}, & 3 < x \le 5 \\ 
   \dfrac{7 - x}{7 - 5} = \dfrac{7 - x}{2}, & 5 < x < 7 
   \end{cases}$$

3. **Label `Lambat` (Bahu Kanan / Trapesium Naik):**
   $$\mu_{\text{Lambat}}(x) = \begin{cases} 
   0, & x \le 6 \\ 
   \dfrac{x - 6}{8 - 6} = \dfrac{x - 6}{2}, & 6 < x < 8 \\ 
   1, & x \ge 8 
   \end{cases}$$

### Contoh Perhitungan Manual Input Crisp $x = 3.5$ detik:
- $\mu_{\text{Cepat}}(3.5) = \dfrac{4 - 3.5}{2} = \dfrac{0.5}{2} = 0.25$
- $\mu_{\text{Sedang}}(3.5) = \dfrac{3.5 - 3}{2} = \dfrac{0.5}{2} = 0.25$
- $\mu_{\text{Lambat}}(3.5) = 0.0$

**Hasil Fuzzifikasi:** Pada waktu respons $3.5$ detik, sistem mengenali kondisi tersebut sebagai **Cepat dengan derajat 0.25** dan **Sedang dengan derajat 0.25**.

---

## D. Implementasi dalam Python

### 1. Struktur Kode Lengkap
Simpan kode berikut sebagai `pertemuan2_variabel_linguistik.py`:

```python
import numpy as np
import matplotlib.pyplot as plt

# ==========================================================
# 1. DEFINISI FUNGSI KEANGGOTAAN LINGUISTIK
# ==========================================================
def mf_cepat(x):
    """Fungsi bahu kiri untuk label Cepat"""
    kondisi = [
        x <= 2.0,
        (x > 2.0) & (x < 4.0),
        x >= 4.0
    ]
    pilihan = [
        1.0,
        (4.0 - x) / (4.0 - 2.0),
        0.0
    ]
    return np.select(kondisi, pilihan)


def mf_sedang(x):
    """Fungsi segitiga untuk label Sedang"""
    kondisi = [
        (x <= 3.0) | (x >= 7.0),
        (x > 3.0) & (x <= 5.0),
        (x > 5.0) & (x < 7.0)
    ]
    pilihan = [
        0.0,
        (x - 3.0) / (5.0 - 3.0),
        (7.0 - x) / (7.0 - 5.0)
    ]
    return np.select(kondisi, pilihan)


def mf_lambat(x):
    """Fungsi bahu kanan untuk label Lambat"""
    kondisi = [
        x <= 6.0,
        (x > 6.0) & (x < 8.0),
        x >= 8.0
    ]
    pilihan = [
        0.0,
        (x - 6.0) / (8.0 - 6.0),
        1.0
    ]
    return np.select(kondisi, pilihan)


# ==========================================================
# 2. DEFINISI STRUKTUR VARIABEL LINGUISTIK
# ==========================================================
variabel_waktu_respons = {
    "nama": "Waktu Respons Server",
    "satuan": "detik",
    "semesta": (0.0, 10.0),
    "label": {
        "Cepat": mf_cepat,
        "Sedang": mf_sedang,
        "Lambat": mf_lambat
    }
}


# ==========================================================
# 3. FUNGSI FUZZIFIKASI INPUT TUNGGAL
# ==========================================================
def fuzzifikasi(nilai_crisp, variabel):
    """
    Melakukan pemetaan nilai crisp ke semua derajat label linguistik.
    """
    hasil = {}
    u_min, u_max = variabel["semesta"]
    
    if not (u_min <= nilai_crisp <= u_max):
        raise ValueError(f"Input {nilai_crisp} di luar semesta [{u_min}, {u_max}]")
        
    for nama_label, fungsi_mf in variabel["label"].items():
        derajat = float(fungsi_mf(np.array([nilai_crisp]))[0])
        hasil[nama_label] = round(derajat, 4)
        
    return hasil


# ==========================================================
# 4. PENGUJIAN DAN VISUALISASI
# ==========================================================
x_semesta = np.linspace(0.0, 10.0, 500)

y_cepat = mf_cepat(x_semesta)
y_sedang = mf_sedang(x_semesta)
y_lambat = mf_lambat(x_semesta)

plt.figure(figsize=(10, 5.5))
plt.plot(x_semesta, y_cepat, label='Cepat', color='#2ca02c', linewidth=2.5)
plt.plot(x_semesta, y_sedang, label='Sedang', color='#ff7f0e', linewidth=2.5)
plt.plot(x_semesta, y_lambat, label='Lambat', color='#d62728', linewidth=2.5)

# Simulasi input x = 3.5 detik
x_uji = 3.5
derajat_uji = fuzzifikasi(x_uji, variabel_waktu_respons)

plt.axvline(x=x_uji, color='purple', linestyle='--', linewidth=1.8, label=f'Input x = {x_uji}s')
plt.scatter([x_uji, x_uji], [derajat_uji['Cepat'], derajat_uji['Sedang']], 
            color='purple', s=70, zorder=5)

plt.title(f'Variabel Linguistik: {variabel_waktu_respons["nama"]}', fontsize=13, fontweight='bold')
plt.xlabel(f'Waktu Respons ({variabel_waktu_respons["satuan"]})', fontsize=11)
plt.ylabel('Derajat Keanggotaan μ(x)', fontsize=11)
plt.ylim(-0.05, 1.1)
plt.grid(True, linestyle=':', alpha=0.6)
plt.legend(loc='center right', fontsize=10)
plt.tight_layout()

plt.savefig('variabel_linguistik_waktu_respons.png', dpi=300)
plt.show()

# Tampilkan hasil terminal
print(f"Hasil Fuzzifikasi untuk x = {x_uji} {variabel_waktu_respons['satuan']}:")
for label, deg in derajat_uji.items():
    print(f" - {label:<8}: {deg}")
```

---

## E. Skenario Pengujian Fuzzifikasi

Lakukan fuzzifikasi terhadap beberapa nilai input representatif berikut:

| No | Input Crisp ($x$) | $\mu_{\text{Cepat}}(x)$ | $\mu_{\text{Sedang}}(x)$ | $\mu_{\text{Lambat}}(x)$ | Label Dominan |
|:--:|:---:|:---:|:---:|:---:|:---:|
| 1 | 1.0 s | 1.000 | 0.000 | 0.000 | Cepat |
| 2 | 2.5 s | 0.750 | 0.000 | 0.000 | Cepat |
| 3 | 3.5 s | 0.250 | 0.250 | 0.000 | Imbang (Cepat/Sedang) |
| 4 | 5.0 s | 0.000 | 1.000 | 0.000 | Sedang |
| 5 | 6.5 s | 0.000 | 0.250 | 0.250 | Imbang (Sedang/Lambat) |
| 6 | 7.5 s | 0.000 | 0.000 | 0.750 | Lambat |
| 7 | 9.0 s | 0.000 | 0.000 | 1.000 | Lambat |

---

## F. Tugas Praktikum 2

### Pemodelan Variabel: Penggunaan CPU Server (*CPU Utilization*)
Rancang sebuah variabel linguistik untuk **Penggunaan CPU Server**:
1. **Semesta Pembicaraan:** $U = [0, 100] \%$ beban CPU.
2. **Label Linguistik:**
   - `Rendah`: $0 \le x \le 40\%$, bahu kiri (penuh pada $\le 20\%$, turun ke $0$ pada $40\%$).
   - `Normal`: $30 \le x \le 70\%$, bentuk segitiga (puncak pada $50\%$).
   - `Tinggi`: $60 \le x \le 100\%$, bahu kanan (naik dari $60\%$, penuh pada $\ge 80\%$).
3. **Instruksi Tugas:**
   - Turunkan rumus matematika masing-masing label secara manual.
   - Buat fungsi Python untuk variabel linguistik tersebut.
   - Plot ketiga label dalam satu grafik berwarna jelas.
   - Lakukan pengujian fuzzifikasi untuk input beban CPU: $10\%, 35\%, 50\%, 65\%, 75\%, 95\%$.
   - Tampilkan tabel output derajat keanggotaan dan simpan hasil grafik.

---

## G. Pertanyaan Analisis

1. Mengapa kurva fungsi keanggotaan yang bersebelahan harus saling tumpang tindih (*overlap*)? Apa konsekuensinya pada sistem inferensi jika terdapat celah (*gap*) kosong di antara dua kurva?
2. Pada pengujian input $x = 3.5$, diperoleh $\mu_{\text{Cepat}} = 0.25$ dan $\mu_{\text{Sedang}} = 0.25$ (total = $0.5$). Apakah total derajat keanggotaan suatu variabel pada satu titik harus selalu berjumlah 1.0? Jelaskan konsep *fuzzy partition*!
3. Jika pengembang ingin menambahkan label `Sangat Cepat` dan `Sangat Lambat`, bagaimana pengaruhnya terhadap resolusi dan sensitivitas kendali sistem?

---

## H. Ketentuan & Pengumpulan
1. Mahasiswa menyusun laporan mandiri berisi penurunan rumus, source code Python, tabel pengujian, dan jawaban pertanyaan analisis.
2. Simpan file laporan di folder repositori masing-masing: `Modul-1/Praktikum2_<NIM>.ipynb` atau `.py`.
3. Lakukan git commit: `feat(modul1): selesaikan materi variabel linguistik praktikum 2`.

---

## I. Kesimpulan
Variabel linguistik menjembatani nilai data numerik (*crisp*) dengan penalaran intuitif manusia. Melalui penetapan semesta pembicaraan, domain, dan label linguistik yang tepat, sebuah sistem komputasi cerdas dapat merepresentasikan kondisi lingkungan secara alami dan siap diproses ke tahap inferensi aturan fuzzy (*fuzzy rules*).
