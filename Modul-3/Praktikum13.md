# Praktikum 13 — Pengembangan Web App Fuzzy dengan Streamlit
## Membangun Antarmuka Pengguna Interaktif, Integrasi Logika Inferensi, dan Visualisasi Keputusan Real-Time

---

## A. Tujuan Praktikum
Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:
1. Memahami arsitektur aplikasi berbasis logika fuzzy dengan pemisahan tegas antara logika bisnis (*Fuzzy Engine*) dan antarmuka pengguna (*User Interface*).
2. Membangun antarmuka web interaktif menggunakan framework **Streamlit**.
3. Merancang komponen masukan pengguna yang ergonomis menggunakan *Slider*, *Number Input*, dan *Select Box*.
4. Menampilkan hasil inferensi secara real-time disertai indikator visual (*Metric Badge*, *Progress Bar*, dan *Warning Alert*).
5. Mengintegrasikan visualisasi grafik `Matplotlib` langsung ke dalam halaman aplikasi web.
6. Menjalankan dan menguji aplikasi web secara lokal di lingkungan komputer laboratorium.

---

## B. Konsep Dasar

### 1. Mengapa Streamlit untuk Aplikasi Fuzzy?
Streamlit adalah framework Python open-source yang memungkinkan pengembang mengubah skrip data dan model machine learning/fuzzy menjadi aplikasi web interaktif tanpa memerlukan keahlian frontend HTML/CSS/JavaScript yang rumit:
- **Reaktif (*Reactive Execution*):** Setiap kali pengguna menggeser slider atau mengubah nilai, Streamlit secara otomatis menjalankan ulang inferensi dan memperbarui layar seketika.
- **Dukungan Visualisasi Penuh:** Grafik `Matplotlib`, kurva keanggotaan, dan plot 3D dapat langsung dirender menggunakan `st.pyplot()`.
- **Pengembangan Cepat (*Rapid Prototyping*):** Sangat ideal untuk mendemonstrasikan sistem pendukung keputusan fuzzy kepada pengguna non-teknis.

### 2. Pola Arsitektur Pemisahan Kode

```text
proyek-fuzzy/
├── engine/
│   └── fuzzy_engine.py      # Murni logika inferensi (Python murni/scikit-fuzzy)
└── app.py                   # Murni antarmuka pengguna (Streamlit)
```

Dengan struktur ini:
- `fuzzy_engine.py` dapat diuji secara mandiri tanpa menjalankan web server.
- Antarmuka `app.py` hanya bertugas menangkap input, memanggil fungsi inferensi, dan merender hasilnya.

---

## C. Implementasi dalam Python

### 1. Instalasi Streamlit
Buka terminal dan jalankan instalasi:
```bash
pip install streamlit
```

### 2. Modul Mesin Inferensi (`fuzzy_engine.py`)
Buat file di `Modul-3/src/fuzzy_engine.py`:

```python
import numpy as np

def hitung_prioritas_tiket(waktu_jam, urgensi_skor):
    """
    Fungsi logika inferensi fuzzy (Sugeno sederhana).
    Input:
      - waktu_jam (float): 0 - 24 jam
      - urgensi_skor (float): 0 - 100 poin
    Output:
      - skor_prioritas (float): 0 - 100
      - kategori (str): 'Rendah', 'Sedang', 'Tinggi', atau 'Kritis'
      - detail_derajat (dict)
    """
    # Fuzzifikasi Waktu
    mu_waktu_cepat = max(0.0, min(1.0, (8.0 - waktu_jam) / 8.0)) if waktu_jam <= 8.0 else 0.0
    mu_waktu_lama = max(0.0, min(1.0, (waktu_jam - 4.0) / 12.0)) if waktu_jam >= 4.0 else 0.0
    
    # Fuzzifikasi Urgensi
    mu_urgensi_rendah = max(0.0, min(1.0, (50.0 - urgensi_skor) / 50.0)) if urgensi_skor <= 50.0 else 0.0
    mu_urgensi_tinggi = max(0.0, min(1.0, (urgensi_skor - 30.0) / 70.0)) if urgensi_skor >= 30.0 else 0.0
    
    # Evaluasi Aturan (Sugeno Orde 0)
    # R1: IF Waktu Cepat AND Urgensi Rendah THEN Prioritas = 20
    a1 = min(mu_waktu_cepat, mu_urgensi_rendah)
    z1 = 20.0
    
    # R2: IF Waktu Cepat AND Urgensi Tinggi THEN Prioritas = 60
    a2 = min(mu_waktu_cepat, mu_urgensi_tinggi)
    z2 = 60.0
    
    # R3: IF Waktu Lama AND Urgensi Rendah THEN Prioritas = 50
    a3 = min(mu_waktu_lama, mu_urgensi_rendah)
    z3 = 50.0
    
    # R4: IF Waktu Lama AND Urgensi Tinggi THEN Prioritas = 95
    a4 = min(mu_waktu_lama, mu_urgensi_tinggi)
    z4 = 95.0
    
    # Defuzzifikasi Weighted Average
    total_alpha = a1 + a2 + a3 + a4
    if total_alpha == 0:
        skor = 20.0
    else:
        skor = (a1*z1 + a2*z2 + a3*z3 + a4*z4) / total_alpha
        
    skor = round(float(skor), 2)
    
    # Penentuan Kategori Linguistik
    if skor < 35.0:
        kategori = "Rendah"
    elif skor < 65.0:
        kategori = "Sedang"
    elif skor < 85.0:
        kategori = "Tinggi"
    else:
        kategori = "Kritis (Eskalasi Segera)"
        
    return skor, kategori, {
        "alpha": [a1, a2, a3, a4],
        "mu_input": {
            "Waktu Cepat": mu_waktu_cepat, "Waktu Lama": mu_waktu_lama,
            "Urgensi Rendah": mu_urgensi_rendah, "Urgensi Tinggi": mu_urgensi_tinggi
        }
    }
```

### 3. Aplikasi Web Streamlit (`app.py`)
Buat file di `Modul-3/src/app.py`:

```python
import streamlit as st
import matplotlib.pyplot as plt
import numpy as np
from fuzzy_engine import hitung_prioritas_tiket

# ==========================================================
# 1. KONFIGURASI HALAMAN
# ==========================================================
st.set_page_config(
    page_title="Sistem Rekomendasi Tiket TI",
    page_icon="🎫",
    layout="wide"
)

st.title("🎫 Sistem Pendukung Keputusan Prioritas Tiket Dukungan TI")
st.markdown("""
Aplikasi ini menggunakan **Logika Fuzzy (Sistem Inferensi Sugeno)** untuk menentukan tingkat prioritas 
penanganan tiket berdasarkan waktu tunggu dan tingkat urgensi masalah.
""")

st.divider()

# ==========================================================
# 2. SIDEBAR KONTROL INPUT PENGGUNA
# ==========================================================
st.sidebar.header("⚙️ Parameter Masukan")

input_waktu = st.sidebar.slider(
    "⏱️ Waktu Tunggu Tiket (Jam):",
    min_value=0.0,
    max_value=24.0,
    value=6.5,
    step=0.5,
    help="Berapa lama tiket telah berada di antrean sistem."
)

input_urgensi = st.sidebar.slider(
    "🚨 Skor Dampak / Urgensi Masalah (0 - 100):",
    min_value=0.0,
    max_value=100.0,
    value=60.0,
    step=1.0,
    help="Tingkat keparahan dampak terhadap operasional perusahaan."
)

# ==========================================================
# 3. PROSES INFERENSI
# ==========================================================
skor, kategori, detail = hitung_prioritas_tiket(input_waktu, input_urgensi)

# ==========================================================
# 4. TAMPILAN HASIL KEPUTUSAN DI PANEL UTAMA
# ==========================================================
col1, col2 = st.columns([1, 1])

with col1:
    st.subheader("📊 Hasil Rekomendasi Sistem")
    
    # Warna badge berdasarkan kategori
    if "Kritis" in kategori:
        st.error(f"### Kategori: {kategori}")
    elif "Tinggi" in kategori:
        st.warning(f"### Kategori: {kategori}")
    elif "Sedang" in kategori:
        st.info(f"### Kategori: {kategori}")
    else:
        st.success(f"### Kategori: {kategori}")
        
    st.metric(label="Skor Prioritas Penanganan", value=f"{skor} / 100")
    st.progress(int(skor))
    
    st.markdown("#### Detail Derajat Masukan:")
    for nama_lbl, val in detail["mu_input"].items():
        st.write(f"- **{nama_lbl}**: `{val:.3f}`")

with col2:
    st.subheader("📈 Visualisasi Nilai Firing Rules")
    
    fig, ax = plt.subplots(figsize=(6, 4))
    rules = ['R1 (Cepat-Rendah)', 'R2 (Cepat-Tinggi)', 'R3 (Lama-Rendah)', 'R4 (Lama-Tinggi)']
    alphas = detail["alpha"]
    
    ax.barh(rules, alphas, color='#1f77b4')
    ax.set_xlim(0, 1.05)
    ax.set_xlabel('Firing Strength (α)')
    ax.set_title('Tingkat Aktivasi Aturan (Firing Rules)')
    plt.tight_layout()
    
    st.pyplot(fig)

st.divider()
st.caption("Dikembangkan untuk Praktikum Modul 3 Logika Fuzzy — S1 Teknologi Informasi.")
```

---

## D. Menjalankan Aplikasi Web

Buka terminal di folder `Modul-3/src/`, lalu ketikkan perintah:
```bash
streamlit run app.py
```

Aplikasi web secara otomatis akan terbuka pada browser default Anda di alamat:
`http://localhost:8501`

---

## E. Tugas Praktikum 13

1. Rancang file `fuzzy_engine.py` khusus untuk topik proyek mandiri Anda (sesuai proposal Pertemuan 11).
2. Buat antarmuka `app.py` menggunakan Streamlit dengan:
   - Minimal 2 komponen masukan slider yang informatif.
   - Panel hasil metrik dan status rekomendasi.
   - Grafik visualisasi kurva inferensi / aktivasi aturan.
3. Ambil tangkapan layar (*screenshot*) antarmuka aplikasi web Anda pada 3 skenario input yang berbeda.

---

## F. Pertanyaan Analisis

1. Bagaimana cara kerja siklus reaktivitas pada Streamlit ketika pengguna menggeser widget slider?
2. Mengapa pengguna awam (*end-user*) lebih mudah memahami visualisasi progress bar dan badge kategori dibandingkan angka derajat keanggotaan desimal?
3. Sebutkan langkah-langkah yang diperlukan jika aplikasi Streamlit ini ingin dideploy secara publik agar dapat diakses oleh dosen dan rekan kelas melalui internet!

---

## G. Ketentuan & Pengumpulan
1. File yang dikumpulkan: Folder `Modul-3/src/` berisi `app.py`, `fuzzy_engine.py`, serta gambar screenshot aplikasi.
2. Commit git: `feat(modul3): bangun aplikasi web interaktif streamlit praktikum 13`.

---

## H. Kesimpulan
Streamlit menjembatani keahlian algoritma fuzzy dengan kebutuhan antarmuka pengguna modern. Melalui pemisahan logika backend dan frontend reaktif, sistem pendukung keputusan fuzzy menjadi sebuah produk perangkat lunak interaktif yang siap disimulasikan dan diuji secara nyata.
