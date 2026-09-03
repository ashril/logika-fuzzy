# Pertemuan 2 — Himpunan Fuzzy dan Variabel Linguistik

## Tujuan
Mahasiswa mampu membangun himpunan crisp dan fuzzy, menentukan semesta pembicaraan serta domain, dan merepresentasikan variabel linguistik dengan label yang sesuai.

## Materi Inti

### 1. Himpunan dan derajat keanggotaan

Himpunan crisp menetapkan anggota atau bukan anggota. Himpunan fuzzy memberikan derajat keanggotaan `μA(x) ∈ [0, 1]` untuk setiap nilai `x`.

- `0`: tidak menjadi anggota;
- `1`: menjadi anggota penuh;
- nilai di antara 0 dan 1: menjadi anggota sebagian.

### 2. Semesta pembicaraan dan domain

Semesta pembicaraan adalah seluruh nilai yang mungkin. Contoh: waktu respons memiliki semesta 0–10 detik. Domain label tertentu adalah rentang nilai yang relevan untuk label tersebut, misalnya `cepat` pada 0–5 detik.

### 3. Variabel linguistik

Variabel linguistik memiliki nama, semesta pembicaraan, unit, dan label bahasa. Contoh:

- nama: `Waktu Respons`;
- unit: detik;
- semesta: 0–10;
- label: `cepat`, `sedang`, `lambat`.

Label dapat saling tumpang tindih sehingga satu input dapat memiliki beberapa derajat keanggotaan.

## Praktikum

1. Buat array waktu respons menggunakan `np.linspace(0, 10, 501)`.
2. Definisikan label `cepat`, `sedang`, dan `lambat`.
3. Simpan label dalam dictionary variabel linguistik.
4. Plot semua label pada satu grafik.
5. Lakukan fuzzifikasi untuk input 6 detik dengan interpolasi atau fungsi keanggotaan.
6. Catat label dengan derajat keanggotaan terbesar.

## Latihan

1. Ubah semesta menjadi 0–20 detik.
2. Tentukan domain baru untuk ketiga label.
3. Fuzzifikasikan input 7 detik.
4. Jelaskan apakah satu input boleh memiliki keanggotaan pada dua label sekaligus.

## Keluaran

- dictionary variabel linguistik;
- grafik tiga label fuzzy;
- tabel derajat keanggotaan minimal tiga data input;
- interpretasi label dominan.
