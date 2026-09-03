# Pertemuan 3 — Fungsi Keanggotaan

## Tujuan
Mahasiswa mampu menjelaskan, mengimplementasikan, dan memilih fungsi keanggotaan segitiga, trapesium, Gaussian, serta sigmoid.

## Materi Inti

Fungsi keanggotaan memetakan nilai input ke derajat keanggotaan `[0, 1]`. Parameter fungsi harus ditentukan berdasarkan karakteristik data dan arti linguistiknya.

### Jenis fungsi

1. **Segitiga**: memiliki satu titik puncak; sederhana dan mudah diinterpretasikan.
2. **Trapesium**: memiliki rentang dengan keanggotaan penuh; sesuai untuk kategori yang stabil pada suatu interval.
3. **Gaussian**: transisi halus di sekitar pusat; sesuai untuk data dengan variasi kontinu.
4. **Sigmoid**: naik atau turun bertahap; sesuai untuk konsep ambang yang tidak tegas.

## Praktikum NumPy

1. Buat fungsi Python `triangular(x, left, center, right)`.
2. Buat fungsi `trapezoidal(x, a, b, c, d)`.
3. Buat fungsi Gaussian `exp(-0.5 * ((x-center)/sigma)**2)`.
4. Buat fungsi sigmoid `1 / (1 + exp(-slope * (x-center)))`.
5. Evaluasi semua fungsi pada `x = np.linspace(0, 10, 501)`.
6. Buat subplot 2×2 dengan judul dan label sumbu.

Contoh fungsi segitiga:

```python
def triangular(x, left, center, right):
    rising = (x - left) / (center - left)
    falling = (right - x) / (right - center)
    return np.maximum(0, np.minimum(rising, falling))
```

## Praktikum scikit-fuzzy

Jika pustaka tersedia, gunakan:

```python
import skfuzzy as fuzz
triangle = fuzz.trimf(x, [2, 5, 8])
trapezoid = fuzz.trapmf(x, [2, 4, 6, 8])
```

Jika belum tersedia, jalankan `%pip install scikit-fuzzy` pada notebook.

## Latihan

1. Bandingkan segitiga dan Gaussian untuk label `kepuasan sedang`.
2. Ubah parameter pusat dan lebar Gaussian. Amati perubahan grafik.
3. Tentukan fungsi yang paling tepat untuk konsep `waktu respons lambat` dan jelaskan alasannya.

## Keluaran

- implementasi empat fungsi keanggotaan;
- grafik perbandingan;
- analisis dampak perubahan parameter;
- contoh implementasi menggunakan scikit-fuzzy.
