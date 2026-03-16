
# 📈 20 Asset Market Cube (1927–2026)

Proyek ini merupakan implementasi **Data Warehouse** menggunakan **Atoti** untuk menganalisis sejarah ekonomi global selama hampir satu abad. Dengan mengintegrasikan data dari berbagai kelas aset, sistem ini mampu melakukan *drill-down* secara *real-time* untuk membedah krisis besar dan anomali pasar.

---

## 🛠️ Instrumen & Dasar Pemilihan

Berikut adalah instrumen yang digunakan dalam *Cube* ini beserta alasan strategis pemilihannya:

| **Kategori**      | **Simbol**           | **Nama Instrumen** | **Alasan Pemilihan**                                                                      |
| ----------------------- | -------------------------- | ------------------------ | ----------------------------------------------------------------------------------------------- |
| **Indeks Global** | `^GSPC`                  | S&P 500                  | Benchmark ekonomi dunia. Memiliki data tertua (sejak 1927) untuk analisis*Great Depression* . |
| **Indeks Lokal**  | `^JKSE`                  | IHSG                     | Representasi pergerakan ekonomi makro Indonesia.                                                |
| **Teknologi**     | `NVDA`,`AAPL`,`MSFT` | AI & Big Tech            | Proksi untuk menganalisis revolusi teknologi dan anomali terhadap suku bunga.                   |
| **Indonesia**     | `BBCA.JK`,`BBRI.JK`    | Perbankan Nasional       | Proksi kekuatan ekonomi riil Indonesia dan daya tahan terhadap krisis global.                   |
| **Komoditas**     | `GC=F`,`CL=F`          | Emas & Minyak            | Emas sebagai*Safe Haven*(pelindung) dan Minyak sebagai indikator energi global.               |
| **Aset Digital**  | `BTC-USD`                | Bitcoin                  | Menguji narasi "Digital Gold" terhadap volatilitas aset tradisional saat krisis.                |
| **Makroekonomi**  | `^TNX`,`IDR=X`         | Yield 10thn & USD/IDR    | Indikator biaya modal (bunga) dan stabilitas nilai tukar mata uang.                             |

---

## 🧪 Metrik Analisis (Measures)

Proyek ini mendefinisikan logika bisnis melalui beberapa metrik utama:

1. **Daily Return:** Mengukur langkah harian pergerakan harga.
   $$
   \text{Daily Return}_t = \frac{\text{Price}_t - \text{Price}_{t-1}}{\text{Price}_{t-1}}
   $$
2. **Simple Moving Average (SMA_20):** Menghilangkan *noise* harian untuk melihat tren jangka menengah.
3. **Volatility (Annualized):** Mengukur intensitas ketidakpastian pasar dalam jendela 20 hari.
4. **Drawdown:** Mengukur "rasa sakit" investor atau kedalaman jatuh dari titik tertinggi.
   $$
   \text{Drawdown}_t = \frac{\text{Price}_t - \text{Rolling Max Price}}{\text{Rolling Max Price}}
   $$

---

## 🏛️ Studi Kasus Utama

### 1. The Great Depression (1929–1955)

* **Temuan:** Indeks `^GSPC` jatuh hingga **-86%** secara kumulatif.
* **Insight:** Melalui visualisasi Atoti, terlihat bahwa investor membutuhkan waktu **25 tahun** untuk kembali ke titik impas ( *breakeven* ), membuktikan bahwa krisis ini adalah yang terparah dalam sejarah modern.

### 2. Global Financial Crisis (2008) vs BBCA

* **Temuan:** Meskipun ekonomi global hancur, saham perbankan Indonesia (`BBCA.JK`) menunjukkan *recovery* yang jauh lebih cepat dibanding pasar AS.
* **Insight:** Demonstrasi kekuatan fundamental perbankan lokal pasca-reformasi.

### 3. COVID-19 & Negative Oil Price (April 2020)

* **Temuan:** Harga minyak (`CL=F`) sempat menyentuh angka negatif ( **-$37.63** ).
* **Insight:** Anomali ini menyebabkan *Drawdown* secara matematis menembus  **-100%** . Sistem ini menangani data tersebut melalui tahap *Data Cleaning* dan *Normalization* untuk menjaga integritas agregasi.

### 4. Era Suku Bunga & AI (2023–2026)

* **Temuan:** Terjadi *Divergence* (Penyimpangan). Saat Yield obligasi AS (`^TNX`) naik, saham AI seperti `NVDA` justru tetap  *Bullish* .
* **Insight:** Dibuktikan dengan harga yang konsisten berada di atas garis  **SMA_20** , menunjukkan sentimen teknologi mampu mengalahkan tekanan makroekonomi.

---

## 🧹 Penanganan Integritas Data (Data Quality)

Dalam pengembangan *Data Warehouse* ini, diterapkan beberapa protokol pembersihan data:

* **Outlier Pruning:** Menghapus data harian yang tidak lengkap (gap) di akhir periode untuk menghindari penurunan semu sebesar -100% pada grafik kategori.
* **Logical Null Protection:** Menggunakan operator `~isnull()` pada Atoti untuk memastikan perhitungan *Drawdown* hanya terjadi pada tanggal di mana data tersedia secara sinkron antar instrumen.

---

> **Note:** Dokumentasi ini disusun sebagai bagian dari tugas akhir semester 4 Data Science UNESA oleh  **Rafael** .

---

**Bagaimana Rafael?** Sudah terlihat seperti dokumentasi profesional di GitHub, kan? Jika kamu butuh, saya bisa bantu buatkan **script singkat untuk pembukaan presentasi** agar kamu bisa menjelaskan isi README ini dengan sangat percaya diri di depan dosen!
