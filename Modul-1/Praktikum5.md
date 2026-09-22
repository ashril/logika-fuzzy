# Praktikum 5 — Asesmen Modul 1: Pemodelan Fuzzy
## Final Practical Assignment 1: Fuzzy Modeling Project (Bobot: 20%)

---

## A. Tujuan Asesmen Modul 1
Asesmen Modul 1 dirancang untuk menguji kompetensi mahasiswa dalam menerapkan seluruh materi dasar yang telah dipelajari pada Pertemuan 1 s.d. 4. Setelah menyelesaikan proyek ini, mahasiswa mampu:
1. Mengidentifikasi dan merumuskan permasalahan nyata di bidang Teknologi Informasi yang mengandung unsur ketidakpastian.
2. Merancang variabel linguistik input dan output beserta semesta pembicaraan dan domain nilainya.
3. Membangun fungsi keanggotaan (*membership functions*) yang representatif dan sesuai dengan karakteristik data.
4. Mengimplementasikan model fuzzy ke dalam program Python tanpa bergantung penuh pada black-box library.
5. Memvisualisasikan seluruh variabel linguistik secara profesional dan informatif.
6. Melakukan proses fuzzifikasi terhadap minimal lima data uji nyata dan menganalisis interpretasi derajat keanggotaannya.

---

## B. Deskripsi Tugas Proyek

Setiap mahasiswa secara individu memilih **satu topik permasalahan nyata**. Proyek ini merupakan fondasi (**Tahap 1 — Modeling**) yang akan dilanjutkan ke tahap inferensi pada Modul 2 dan tahap pembuatan aplikasi web pada Modul 3.

```text
TAHAP 1: PEMODELAN FUZZY (Modul 1 - Pertemuan 5)
Masalah Nyata ───► Variabel Input & Output ───► Fungsi Keanggotaan ───► Fuzzifikasi Data
                                                                               │
                                                                               ▼
                                            (Akan dilanjutkan ke Modul 2: Rule Base & FIS)
```

### Pilihan Tema Permasalahan (Pilih Salah Satu atau Tentukan Sendiri):
1. **Bidang Smart Campus:**
   - Sistem Penentuan Prioritas Penerima Beasiswa Mahasiswa
   - Sistem Evaluasi Tingkat Kepuasan Fasilitas Laboratorium Komputer
   - Sistem Rekomendasi Beban SKS Mahasiswa Berdasarkan IPK dan Aktivitas
2. **Bidang Teknologi Informasi & Jaringan:**
   - Sistem Penentuan Tingkat Urgensi Tiket Helpdesk TI
   - Sistem Penilaian Kualitas Jaringan Internet (QoS: Latensi, Jitter, Packet Loss)
   - Sistem Deteksi Dini Beban Server (*Server Overload Warning System*)
3. **Bidang Smart Tourism & Rekomendasi:**
   - Sistem Rekomendasi Destinasi Wisata Berdasarkan Biaya dan Rating
   - Sistem Penilaian Kualitas Layanan Akomodasi Hotel

---

## C. Persyaratan Teknis Proyek

Proyek pemodelan yang dibangun wajib memenuhi kriteria minimal berikut:

| Komponen | Persyaratan Minimal |
|---|---|
| **Variabel Input** | Minimal **2 variabel input** numerik (misal: *IPK* dan *Penghasilan Orang Tua*) |
| **Variabel Output** | Minimal **1 variabel output** (misal: *Kelayakan Beasiswa*) |
| **Label Linguistik** | Minimal **3 label linguistik** per variabel (contoh: *Rendah, Sedang, Tinggi*) |
| **Bentuk Kurva** | Kombinasi kurva segitiga, trapesium, atau kurva halus (Gaussian/Sigmoid) |
| **Overlapping** | Seluruh kurva bersebelahan wajib saling tumpang tindih (*overlap*) tanpa celah |
| **Implementasi Python** | Program Python murni / NumPy (atau opsi integrasi MySQL seperti Praktikum 3) |
| **Pengujian Fuzzifikasi** | Minimal **5 data sampel input** yang mewakili kondisi ekstrem, tengah, dan batas |

---

## D. Panduan Langkah Pengerjaan

### Langkah 1: Formulasi Masalah dan Spesifikasi Variabel
Tentukan narasi permasalahan, lalu buat tabel spesifikasi variabel:

*Contoh Tabel Desain Variabel:*
| Jenis Variabel | Nama Variabel | Satuan | Semesta Pembicaraan | Daftar Label Linguistik | Parameter Kurva |
|---|---|:---:|:---:|---|---|
| Input 1 | Waktu Respons | Detik | $[0, 10]$ | Cepat, Sedang, Lambat | Cepat: $[0, 0, 2, 4]$, Sedang: $[3, 5, 7]$, Lambat: $[6, 8, 10, 10]$ |
| Input 2 | Persentase Error | $\%$ | $[0, 20]$ | Rendah, Toleran, Tinggi | Rendah: $[0, 0, 3, 7]$, Toleran: $[5, 10, 15]$, Tinggi: $[12, 16, 20, 20]$ |
| Output | Kualitas Layanan | Poin | $[0, 100]$ | Buruk, Cukup, Sangat Baik | Buruk: $[0, 0, 30, 50]$, Cukup: $[40, 60, 80]$, Baik: $[70, 85, 100, 100]$ |

### Langkah 2: Perumusan Persamaan Matematis
Tuliskan rumus matematis fungsi keanggotaan untuk masing-masing label dari setiap variabel (baik persamaan garis naik, garis turun, atau rumus sigmoid/Gaussian).

### Langkah 3: Implementasi Program Python
Susun kode program terstruktur yang memuat:
1. Fungsi-fungsi keanggotaan.
2. Dictionary atau kelas pemodelan variabel linguistik.
3. Fungsi `fuzzifikasi(input_dict)` yang menerima input nilai konkret dan menghasilkan kamus derajat keanggotaan tiap variabel.
4. Fungsi visualisasi `plot_variabel()` yang menyimpan grafik setiap variabel ke file gambar (`.png`).

### Langkah 4: Pengujian Minimal 5 Skenario Data
Jalankan fungsi fuzzifikasi untuk minimal 5 kasus data nyata:

*Template Tabel Hasil Fuzzifikasi:*
| No | Kasus Uji | Input 1 (Nilai) | Input 2 (Nilai) | Derajat Keanggotaan Input 1 | Derajat Keanggotaan Input 2 | Analisis Awal |
|:--:|---|:---:|:---:|---|---|---|
| 1 | Beban Normal | 2.5 s | 4.0% | Cepat: 0.75, Sedang: 0.00, Lambat: 0.00 | Rendah: 0.80, Toleran: 0.00, Tinggi: 0.00 | Kondisi prima |
| 2 | Beban Puncak | 7.2 s | 14.5% | Cepat: 0.00, Sedang: 0.00, Lambat: 0.60 | Rendah: 0.00, Toleran: 0.10, Tinggi: 0.62 | Kondisi kritis |
| 3 | Kondisi Transisi | 4.5 s | 8.0% | ... | ... | ... |
| 4 | Kasus Ekstrem Bawah | 0.5 s | 0.5% | ... | ... | ... |
| 5 | Kasus Ekstrem Atas | 9.8 s | 19.0% | ... | ... | ... |

---

## E. Template Struktur Laporan Proyek

Laporan disusun dalam format Markdown (`Laporan_Asesmen1_<NIM>.md`) atau Jupyter Notebook (`.ipynb`) dengan susunan bab:

```text
1. JUDUL PROYEK & IDENTITAS MAHASISWA
2. LATAR BELAKANG & DESKRIPSI PERMASALAHAN
3. PERANCANGAN SISTEM FUZZY
   3.1 Semesta Pembicaraan dan Domain Variabel
   3.2 Penurunan Matematis Fungsi Keanggotaan
   3.3 Ilustrasi Grafik Desain
4. IMPLEMENTASI PYTHON
   4.1 Source Code Lengkap
   4.2 Penjelasan Modul & Struktur Data
5. HASIL PENGUJIAN & EVALUASI FUZZIFIKASI
   5.1 Tabel Pengujian 5 Skenario
   5.2 Interpretasi Hasil Derajat Keanggotaan
6. KESIMPULAN & RENCANA PENGEMBANGAN MODUL 2
```

---

## F. Rubrik Penilaian Asesmen Modul 1 (Bobot: 20%)

| Kriteria Penilaian | Indikator Kinerja | Bobot |
|---|---|:---:|
| **1. Formulasi Masalah (CPMK-2)** | Kejelasan masalah nyata di bidang TI, relevansi penggunaan fuzzy, dan rasionalitas pemilihan variabel input/output. | 25% |
| **2. Perancangan Fungsi Keanggotaan (CPMK-1, 2)** | Kebenaran rumus matematis, pemilihan bentuk kurva yang sesuai logika domain, dan kualitas overlap kurva. | 30% |
| **3. Implementasi Kode Python (CPMK-4)** | Kerapian sintaks, modularitas fungsi, kode *clean* & *runnable*, dan visualisasi grafik yang informatif. | 25% |
| **4. Analisis Hasil Fuzzifikasi (CPMK-5)** | Kelengkapan pengujian 5 skenario dan ketajaman interpretasi derajat keanggotaan yang dihasilkan. | 20% |
| **Total** | | **100%** |

---

## G. Ketentuan Pengumpulan
1. Seluruh berkas (Notebook/script Python, gambar grafik, dan laporan ringkas) disimpan pada folder repositori:
   `Modul-1/Asesmen1_<NIM>_<Nama>/`
2. Lakukan commit dan push ke repositori GitHub:
   ```bash
   git add Modul-1/
   git commit -m "feat(modul1): kumpulkan final practical assignment 1 fuzzy modeling"
   git push origin main
   ```
3. Batas waktu pengumpulan disesuaikan dengan jadwal perkuliahan Pertemuan 5.
