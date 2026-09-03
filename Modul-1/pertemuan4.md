# Pertemuan 4 — Operasi Himpunan Fuzzy

## Tujuan
Mahasiswa mampu menerapkan union, intersection, complement, AND, OR, T-norm, dan T-conorm serta menginterpretasikan hasilnya.

## Materi Inti

Untuk dua himpunan fuzzy `A` dan `B` pada nilai `x`:

- **Union/OR standar**: `μ(A ∪ B) = max(μA, μB)`;
- **Intersection/AND standar**: `μ(A ∩ B) = min(μA, μB)`;
- **Complement**: `μ(not A) = 1 - μA`.

Minimum adalah contoh **T-norm**, sedangkan maksimum adalah contoh **T-conorm**. Alternatif yang sering digunakan:

- product T-norm: `μA · μB`;
- probabilistic sum T-conorm: `μA + μB - μA · μB`.

## Praktikum

1. Definisikan dua array derajat keanggotaan, misalnya `quality` dan `speed`.
2. Hitung `np.maximum(quality, speed)` untuk union.
3. Hitung `np.minimum(quality, speed)` untuk intersection.
4. Hitung `1 - quality` untuk complement.
5. Bandingkan hasil minimum dengan product T-norm.
6. Bandingkan hasil maksimum dengan probabilistic sum T-conorm.
7. Buat grafik yang membandingkan input, AND, dan OR.

Contoh:

```python
union = np.maximum(quality, speed)
intersection = np.minimum(quality, speed)
complement = 1 - quality
product = quality * speed
probabilistic_sum = quality + speed - quality * speed
```

## Analisis

Intersection tidak akan lebih besar daripada salah satu operand karena AND mensyaratkan kedua kondisi terpenuhi. Product T-norm biasanya lebih ketat daripada minimum ketika kedua derajat kurang dari 1. Union memilih derajat tertinggi, sedangkan probabilistic sum memperhitungkan kontribusi kedua operand.

## Latihan

1. Ubah nilai anggota kedua himpunan dan hitung ulang semua operasi.
2. Temukan satu pasangan input yang menghasilkan perbedaan besar antara `min` dan product.
3. Jelaskan operator yang tepat untuk kondisi “kualitas baik DAN respons cepat”.
4. Jelaskan operator yang tepat untuk kondisi “kualitas baik ATAU respons cepat”.

## Keluaran

- tabel seluruh hasil operasi;
- grafik perbandingan operator;
- analisis perubahan nilai dan alasan pemilihan operator.
