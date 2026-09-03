# Pertemuan 1 — Pengantar Logika Fuzzy

## Tujuan
Setelah praktikum, mahasiswa mampu:

- menjelaskan pengambilan keputusan dalam kondisi ketidakpastian;
- membedakan logika Boolean/crisp dan logika fuzzy;
- menjelaskan arti derajat keanggotaan;
- mengenali penerapan fuzzy pada Teknologi Informasi.

## Materi Inti

### 1. Ketidakpastian dalam pengambilan keputusan

Banyak konsep nyata tidak memiliki batas tegas. Waktu respons 3,9 detik dapat dianggap cepat oleh satu pengguna dan lambat oleh pengguna lain. Logika fuzzy membantu merepresentasikan konsep seperti *cepat*, *baik*, atau *tinggi* secara bertahap.

### 2. Crisp versus fuzzy

Pada himpunan crisp, keanggotaan hanya bernilai 0 atau 1. Pada himpunan fuzzy, fungsi keanggotaan `μA(x)` bernilai pada interval `[0, 1]`. Nilai 0,8 menunjukkan tingkat pemenuhan konsep sebesar 0,8, bukan probabilitas.

| Aspek | Crisp/Boolean | Fuzzy |
|---|---|---|
| Nilai keanggotaan | 0 atau 1 | 0 sampai 1 |
| Batas kategori | Tegas | Bertahap |
| Contoh | rating >= 4 | derajat “rating baik” |

### 3. Sejarah dan penerapan

Teori himpunan fuzzy diperkenalkan Lotfi A. Zadeh pada 1965. Saat ini fuzzy digunakan dalam sistem rekomendasi, sistem pendukung keputusan, klasifikasi, diagnosis, pengaturan jaringan, prioritas tiket helpdesk, dan penilaian kualitas layanan.

## Praktikum

1. Buka notebook `Modul_1_Dasar_Logika_Fuzzy_dan_Fuzzifikasi.ipynb`.
2. Jalankan sel import NumPy dan Matplotlib.
3. Buat data rating crisp dengan aturan `rating >= 4`.
4. Buat derajat fuzzy untuk rating yang sama, misalnya `[0.0, 0.25, 0.75, 1.0]`.
5. Visualisasikan kedua representasi pada grafik yang sama.
6. Jelaskan perbedaan hasil keputusan pada nilai batas.

Contoh pertanyaan sistem rekomendasi: bagaimana menggabungkan tingkat kepuasan pengguna dan waktu respons untuk menentukan rekomendasi layanan?

## Latihan

1. Berikan dua contoh masalah TI yang memiliki batas kategori tidak tegas.
2. Jelaskan mengapa nilai fuzzy tidak sama dengan probabilitas.
3. Buat visualisasi derajat keanggotaan untuk konsep “kualitas layanan baik”.

## Keluaran

- satu grafik crisp versus fuzzy;
- jawaban latihan;
- kesimpulan singkat tentang manfaat fuzzy dalam keputusan yang tidak pasti.
