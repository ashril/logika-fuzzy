# Pertemuan 5 — Asesmen Modul 1

## Final Practical Assignment 1: Fuzzy Modeling

### Tujuan
Mahasiswa mampu mengubah satu permasalahan nyata menjadi model fuzzy sederhana, melakukan fuzzifikasi, dan menjelaskan hasilnya secara terukur.

## Instruksi

Pilih satu masalah sederhana, misalnya prioritas tiket helpdesk, kualitas jaringan, rekomendasi film, kelayakan layanan, atau risiko transaksi. Kerjakan delapan langkah berikut.

1. **Tentukan permasalahan.** Jelaskan konteks, pengguna, dan alasan fuzzy diperlukan.
2. **Tentukan variabel input dan output.** Minimal satu input dan satu output; tuliskan satuan setiap variabel.
3. **Tentukan domain.** Tuliskan semesta pembicaraan dan rentang nilai tiap variabel.
4. **Tentukan himpunan linguistik.** Gunakan label yang bermakna, misalnya `rendah`, `sedang`, dan `tinggi`.
5. **Tentukan fungsi keanggotaan.** Pilih segitiga, trapesium, Gaussian, atau sigmoid dan jelaskan alasan serta parameternya.
6. **Implementasikan dengan Python.** Gunakan NumPy atau scikit-fuzzy.
7. **Buat visualisasi.** Setiap grafik harus memiliki judul, label sumbu, legenda, dan rentang derajat 0–1.
8. **Lakukan fuzzifikasi.** Uji minimal lima kombinasi/data input dan interpretasikan setiap hasil.

## Template implementasi

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0, 120, 601)
cepat = np.clip((60 - x) / 60, 0, 1)
sedang = triangular(x, 30, 60, 90)
lambat = np.clip((x - 60) / 60, 0, 1)

samples = np.array([10, 35, 55, 75, 110])
hasil = {
    'cepat': np.interp(samples, x, cepat),
    'sedang': np.interp(samples, x, sedang),
    'lambat': np.interp(samples, x, lambat),
}
```

Modifikasi nama variabel, domain, parameter, dan label agar sesuai dengan masalah pilihan Anda.

## Format laporan

1. Judul dan identitas.
2. Deskripsi masalah.
3. Tabel variabel, satuan, domain, dan label.
4. Alasan pemilihan fungsi keanggotaan.
5. Kode Python yang dapat dijalankan.
6. Grafik fungsi keanggotaan.
7. Tabel hasil fuzzifikasi lima data input.
8. Analisis dan kesimpulan.

## Rubrik penilaian

| Komponen | Bobot |
|---|---:|
| Perumusan masalah dan variabel | 20% |
| Domain, label, dan fungsi keanggotaan | 25% |
| Implementasi Python | 25% |
| Visualisasi | 15% |
| Analisis dan kerapian laporan | 15% |

## Refleksi

1. Apa perbedaan nilai fuzzy dan probabilitas?
2. Bagaimana perubahan parameter memengaruhi hasil fuzzifikasi?
3. Apa risiko memilih domain atau label yang terlalu sempit?
