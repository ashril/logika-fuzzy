# Logika Fuzzy

Repositori ini berisi bahan ajar dan praktikum **Modul 1: Dasar-Dasar Logika Fuzzy dan Fuzzifikasi**. Materi disusun untuk membantu mahasiswa memahami cara merepresentasikan permasalahan nyata yang memiliki batas tidak tegas menggunakan himpunan fuzzy, variabel linguistik, dan fungsi keanggotaan.

Praktikum menggunakan Python dan Jupyter Notebook. Contoh-contoh di dalam modul menggunakan konteks penilaian kualitas layanan, tetapi dapat dikembangkan untuk masalah Teknologi Informasi seperti sistem rekomendasi, sistem pendukung keputusan, klasifikasi, dan prioritas tiket helpdesk.

## Capaian Pembelajaran

Setelah menyelesaikan Modul 1, mahasiswa diharapkan mampu:

1. Menjelaskan konsep ketidakpastian, logika crisp, logika Boolean, dan logika fuzzy.
2. Menjelaskan arti derajat keanggotaan dan membedakannya dari probabilitas.
3. Membentuk himpunan fuzzy berdasarkan semesta pembicaraan dan domain.
4. Menentukan variabel linguistik beserta label linguistik yang sesuai.
5. Mengimplementasikan fungsi keanggotaan segitiga, trapesium, Gaussian, dan sigmoid.
6. Memvisualisasikan fungsi keanggotaan menggunakan NumPy dan Matplotlib.
7. Menerapkan operasi union, intersection, complement, AND, OR, T-norm, dan T-conorm.
8. Melakukan fuzzifikasi terhadap data input dan menginterpretasikan hasilnya.
9. Membuat model fuzzy sederhana untuk permasalahan nyata.

## Daftar Pertemuan

| Pertemuan | Topik | Praktik utama |
|---|---|---|
| 1 | Pengantar Logika Fuzzy | Representasi crisp dan fuzzy serta visualisasi derajat keanggotaan |
| 2 | Himpunan Fuzzy dan Variabel Linguistik | Membuat dan memvisualisasikan himpunan fuzzy |
| 3 | Fungsi Keanggotaan | Implementasi fungsi segitiga, trapesium, Gaussian, sigmoid, dan scikit-fuzzy |
| 4 | Operasi Himpunan Fuzzy | Union, intersection, complement, AND, OR, T-norm, dan T-conorm |
| 5 | Asesmen Modul 1 | Final Practical Assignment 1: Fuzzy Modeling |

## Struktur Modul

```text
Modul-1/
├── pertemuan1.md
├── pertemuan2.md
├── pertemuan3.md
├── pertemuan4.md
├── pertemuan5.md
└── Modul_1_Dasar_Logika_Fuzzy_dan_Fuzzifikasi.ipynb
```

Dokumen pertemuan berisi tujuan, materi inti, langkah praktikum, latihan, dan keluaran yang diharapkan. Notebook berisi contoh kode Python dan visualisasi yang digunakan sepanjang Modul 1.

## Prasyarat

- Python 3 dan Jupyter Notebook atau JupyterLab.
- Pemahaman dasar variabel, fungsi, array, dan grafik pada Python.
- Pustaka `numpy` dan `matplotlib`.
- Pustaka `scikit-fuzzy` untuk bagian integrasi pada Pertemuan 3.

Instalasi pustaka dapat dilakukan melalui terminal:

```bash
python -m pip install numpy matplotlib scikit-fuzzy jupyter
```

## Cara Menjalankan Praktikum

1. Clone repositori dan masuk ke direktorinya.
2. Buka notebook berikut menggunakan Jupyter atau VS Code:
	`Modul-1/Modul_1_Dasar_Logika_Fuzzy_dan_Fuzzifikasi.ipynb`
3. Baca dokumen pertemuan sesuai urutan.
4. Jalankan sel notebook secara berurutan.
5. Lengkapi latihan dan interpretasi hasil pada setiap pertemuan.
6. Untuk Pertemuan 5, pilih permasalahan, tentukan variabel dan domain, bangun fungsi keanggotaan, lakukan fuzzifikasi minimal lima data, lalu kumpulkan notebook beserta analisisnya.

Untuk menjalankan Jupyter Notebook dari terminal:

```bash
jupyter notebook
```

## Cara Commit Perubahan

Pastikan perubahan sudah diperiksa sebelum commit:

```bash
git status
git diff --check
```

Tambahkan file yang ingin disimpan, kemudian buat commit dengan pesan yang jelas:

```bash
git add README.md Modul-1/
git commit -m "docs: susun modul praktikum logika fuzzy"
```

Periksa commit terakhir:

```bash
git log -1 --oneline
```

Jika repositori terhubung ke remote dan perubahan perlu dikirim ke GitHub:

```bash
git push origin main
```

Gunakan pesan commit yang singkat dan menjelaskan perubahan, misalnya `docs: perbarui materi pertemuan 3` atau `feat: tambah contoh fuzzifikasi`.