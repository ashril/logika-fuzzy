# Praktikum 12 — Evaluasi Sistem Fuzzy Menggunakan Dataset
## Pengujian Batch Dataset, Preprocessing Sederhana, Pengukuran Error (MAE, RMSE), dan Analisis Sensitivitas

---

## A. Tujuan Praktikum
Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:
1. Menghubungkan dataset eksternal (file CSV) sebagai sumber input sistem fuzzy menggunakan pustaka `Pandas`.
2. Melakukan proses *preprocessing* data sederhana (penanganan nilai hilang dan validasi rentang semesta).
3. Melakukan eksekusi inferensi fuzzy secara batch (*batch testing*) terhadap puluhan baris data.
4. Menghitung metrik evaluasi kesalahan kuantitatif: **Mean Absolute Error (MAE)** dan **Root Mean Squared Error (RMSE)**.
5. Membandingkan keputusan sistem fuzzy dengan nilai aktual (*ground truth*) atau keputusan aturan pembanding pakar.
6. Menganalisis sensitivitas sistem fuzzy terhadap perubahan nilai variabel masukan (*sensitivity analysis*).

---

## B. Konsep Dasar

### 1. Kebutuhan Validasi Berbasis Data
Sistem fuzzy yang telah dirancang tidak boleh hanya diuji pada 1–2 kasus rekaan (*toy example*). Di lingkungan industri, performa sistem harus divalidasi terhadap dataset nyata atau skenario pengujian komprehensif untuk memastikan:
- Tidak terjadi ketidakstabilan numerik (*numerical instability*) pada data riil.
- Keputusan sistem sejalan dengan keputusan para pakar manusia (*expert ground truth*).
- Tingkat kesalahan (*error rate*) berada dalam batas toleransi yang dapat diterima.

### 2. Metrik Pengukuran Kesalahan (Error Metrics)
Jika terdapat $N$ data uji, di mana $y_i$ adalah nilai aktual / target keputusan pakar, dan $\hat{y}_i$ adalah output inferensi sistem fuzzy:

#### A. Mean Absolute Error (MAE)
Mengukur rata-rata magnitudo kesalahan absolut:
$$\text{MAE} = \frac{1}{N} \sum_{i=1}^{N} |y_i - \hat{y}_i|$$

#### B. Root Mean Squared Error (RMSE)
Memberikan penalti yang lebih besar terhadap kesalahan bernilai ekstrem/besar:
$$\text{RMSE} = \sqrt{\frac{1}{N} \sum_{i=1}^{N} (y_i - \hat{y}_i)^2}$$

---

## C. Implementasi dalam Python

### 1. Pembuatan Dataset Pengujian (`dataset_tiket_it.csv`)
Buat file data sampel di folder `Modul-3/data/dataset_tiket_it.csv`:

```csv
id,waktu_tunggu_jam,tingkat_urgensi,prioritas_aktual
1,1.5,20,15.0
2,3.0,40,30.0
3,5.5,50,52.0
4,7.0,80,78.0
5,9.5,85,88.0
6,12.0,90,95.0
7,4.0,25,25.0
8,8.0,45,60.0
9,15.0,95,98.0
10,2.0,80,65.0
```

### 2. Kode Program Evaluasi Batch dan Pengukuran Error
Simpan sebagai `pertemuan12_evaluasi_data.py`:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# ==========================================================
# 1. FUNGSI DUMMY INFERENSI FUZZY (MAMDANI / SUGENO)
# ==========================================================
def inferensi_fuzzy_prioritas(waktu_jam, urgensi):
    """
    Simulasi fungsi fuzzy engine yang menerima input numerik
    dan mengembalikan nilai output crisp prioritas (0 - 100).
    """
    # Normalisasi bobot simulasi (dapat diganti dengan FIS utuh Anda)
    w1 = np.clip(waktu_jam / 16.0, 0.0, 1.0)
    w2 = np.clip(urgensi / 100.0, 0.0, 1.0)
    
    # Penalaran non-linear halus representasi fuzzy
    skor = (0.45 * w1 + 0.55 * w2) * 100.0
    return round(float(skor), 2)


# ==========================================================
# 2. MEMBACA DAN MEMVALIDASI DATASET DENGAN PANDAS
# ==========================================================
df = pd.read_csv('data/dataset_tiket_it.csv')

print("=" * 65)
print("5 DATA TERATAS PENGUJIAN TIKET IT:")
print("=" * 65)
print(df.head())


# ==========================================================
# 3. EKSEKUSI BATCH TESTING
# ==========================================================
prediksi_fuzzy = []
for index, row in df.iterrows():
    hasil = inferensi_fuzzy_prioritas(row['waktu_tunggu_jam'], row['tingkat_urgensi'])
    prediksi_fuzzy.append(hasil)

df['prediksi_fuzzy'] = prediksi_fuzzy
df['error_absolut'] = np.abs(df['prioritas_aktual'] - df['prediksi_fuzzy'])
df['error_kuadrat'] = (df['prioritas_aktual'] - df['prediksi_fuzzy']) ** 2


# ==========================================================
# 4. PERHITUNGAN METRIK EVALUASI (MAE & RMSE)
# ==========================================================
mae = df['error_absolut'].mean()
rmse = np.sqrt(df['error_kuadrat'].mean())

print("\n" + "=" * 65)
print("HASIL PENGUKURAN KINERJA SISTEM FUZZY:")
print("=" * 65)
print(f"Total Sampel Uji (N) : {len(df)}")
print(f"Mean Absolute Error (MAE)  : {mae:.3f} poin")
print(f"Root Mean Squared Error (RMSE): {rmse:.3f} poin")
print("=" * 65)


# ==========================================================
# 5. VISUALISASI PERBANDINGAN AKTUAL VS PREDIKSI
# ==========================================================
plt.figure(figsize=(10, 5.5))
x_idx = np.arange(1, len(df) + 1)

plt.plot(x_idx, df['prioritas_aktual'], 'ro-', label='Target Aktual (Pakar)', linewidth=2)
plt.plot(x_idx, df['prediksi_fuzzy'], 'bs--', label='Output Sistem Fuzzy', linewidth=2)

plt.title(f'Evaluasi Sistem Fuzzy: Target Aktual vs Prediksi Fuzzy (MAE: {mae:.2f})', 
          fontsize=13, fontweight='bold')
plt.xlabel('Nomor Kasus Tiket Uji', fontsize=11)
plt.ylabel('Skor Prioritas Penanganan', fontsize=11)
plt.xticks(x_idx)
plt.grid(True, linestyle=':', alpha=0.6)
plt.legend(loc='upper left', fontsize=10)
plt.tight_layout()

plt.savefig('evaluasi_prediksi_vs_aktual.png', dpi=300)
plt.show()
```

---

## D. Analisis Sensitivitas (*Sensitivity Analysis*)

Analisis sensitivitas dilakukan untuk mengetahui seberapa besar fluktuasi output jika salah satu variabel input divariasikan secara kontinu sementara variabel lain ditahan konstan.

```text
       ANALISIS SENSITIVITAS
Output
  ▲
  │                  Variabel 1 (Sangat Sensitif / Curam)
  │            /
  │           /      Variabel 2 (Kurang Sensitif / Landai)
  │          /  --------------------
  │         /
  └────────┴────────────────────────► Nilai Input
```

Jika kurva respon terlalu curam secara tiba-tiba, kemungkinan parameter membership function terlalu sempit atau perlu dilakukan penghalusan (*smoothing*).

---

## E. Tugas Praktikum 12

1. Siapkan sebuah file CSV berisi **minimal 15 baris data uji** untuk kasus proyek fuzzy Anda.
2. Terapkan mesin inferensi fuzzy lengkap Anda pada dataset tersebut.
3. Hitung metrik **MAE** dan **RMSE**.
4. Buat visualisasi grafik garis perbandingan antara nilai target vs nilai prediksi fuzzy.
5. Analisis 2 kasus dengan nilai kesalahan absolut terbesar: jelaskan mengapa sistem fuzzy menghasilkan selisih tersebut dan bagaimana cara memperbaiki rule basenya.

---

## F. Pertanyaan Analisis

1. Apakah nilai MAE yang rendah selalu menjamin bahwa seluruh aturan fuzzy telah teruji dengan baik? Bagaimana jika dataset pengujian hanya terpusat pada satu kelompok kondisi?
2. Mengapa metrik RMSE selalu bernilai lebih besar atau sama dengan MAE? Kapan kita lebih memprioritaskan meminimalkan RMSE dibandingkan MAE?
3. Bagaimana strategi *fine-tuning* yang dapat dilakukan jika sistem fuzzy Anda secara konsisten menghasilkan output yang lebih rendah (*under-estimation*) dibandingkan data aktual?

---

## G. Ketentuan & Pengumpulan
1. File yang dikumpulkan: Dataset CSV `data/test_cases.csv`, script Python `Modul-3/Praktikum12_<NIM>.py`, dan grafik visualisasi.
2. Commit git: `feat(modul3): implementasi pengujian batch data dan evaluasi error praktikum 12`.

---

## H. Kesimpulan
Evaluasi berbasis dataset memberikan bukti empiris atas keandalan sistem fuzzy yang dirancang. Dengan menganalisis metrik MAE, RMSE, dan sensitivitas variabel, pengembang dapat menyempurnakan parameter fungsi keanggotaan dan basis aturan secara objektif sebelum diintegrasikan ke dalam antarmuka aplikasi.
