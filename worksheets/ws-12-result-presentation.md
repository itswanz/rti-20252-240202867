# WS-12: Result Presentation & Visualization

> **Bab 12 — Penyajian Hasil & Visualisasi**

---

## Ringkasan Materi

### Data → Insight Model

```
Validated Data → Structured Presentation → Visualization → Pattern Recognition → Insight
```

Penyajian **mendahului** analisis. Tabel dan grafik membantu peneliti "melihat" data sebelum menghitung. Langsung ke uji statistik tanpa visualisasi berisiko kesimpulan yang secara teknis benar tapi kontekstual salah (Anscombe's Quartet, 1973).

### Tabel = Presisi, Grafik = Pola

Keduanya **saling melengkapi**:
- Tabel: angka presisi, self-contained (dipahami tanpa teks), sortable
- Grafik: pola visual, tren, perbandingan cepat

### Jenis Grafik Berdasarkan Tujuan

| Tujuan | Jenis Grafik |
|--------|-------------|
| Perbandingan antar-skenario | Bar chart (grouped/stacked) |
| Distribusi per-skenario | Box plot / violin plot |
| Tren temporal | Line chart |
| Korelasi dua variabel | Scatter plot |
| Proporsi (total = 100%) | Pie chart (hati-hati!) |

### Contoh Tabel Hasil yang Baik

| Model | Accuracy (%) | F1-Score (%) | Training Time (min) |
|-------|-------------|-------------|---------------------|
| BERT | 88.4 ± 1.2 | 87.1 ± 1.4 | 45.2 ± 3.1 |
| LSTM | 86.1 ± 1.8 | 84.5 ± 2.0 | 12.8 ± 1.2 |
| SVM | 82.3 ± 0.9 | 80.7 ± 1.1 | 0.3 ± 0.1 |

*N=10 per model. Mean ± std. Diurutkan berdasarkan Accuracy.*

### Visualization Bias — Yang Harus Dihindari

| Bias | Deskripsi | Dampak |
|------|----------|--------|
| Truncated axis | Y tidak dari 0 | Memperbesar perbedaan kecil |
| Inconsistent scale | Dua grafik skala beda | Perbandingan menyesatkan |
| Cherry-picked data | Hanya tampilkan yang "menang" | Selektif, tidak jujur |
| 3D effects | Efek 3D tanpa dimensi data ke-3 | Distorsi tanpa informasi |
| Missing error bar | Tidak ada variabilitas | Menyembunyikan ketidakpastian |

### Engineering vs Research Presentation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan grafik | Dashboard monitoring | Mendukung argumen ilmiah |
| Informasi wajib | KPI, threshold | Mean, std, CI, N, p-value |
| Bias handling | Less critical | Wajib dihindari (peer-review) |

---

## Template A.12 — Result Presentation Plan

```
RESULT PRESENTATION PLAN

Research Question :Apakah sistem monitoring suhu dan kelembapan berbasis ESP32 dan sensor DHT22 mampu mengirimkan data secara real-time dengan tingkat akurasi yang baik?
Metrik Utama      : Akurasi pembacaan sensor (%), Waktu pengiriman data (ms)
Tabel Hasil:
| Skenario | Metrik 1 (mean ± std) | Metrik 2 (mean ± std) | n |
|pengujian outdor|Akan diperoleh dari eksperimen|Akan diperoleh dari eksperimen|5|
|pengujian indor | Akan diperoleh dari eksperimen  |Akan diperoleh dari eksperime |5 |

Visualisasi yang Direncanakan:
| # | Jenis Grafik | Pesan Utama | Metrik |
|3  |Box Plot|Sebaran waktu pengiriman data|Waktu Pengiriman Data|
| 1 | Bar Chart|  Perbandingan akurasi sensor pada kondisi indoor dan outdoor  | Akurasi Sensor |
| 2 |Line Chart | Perubahan suhu dan kelembapan terhadap waktu|Suhu dan Kelembapan|

Bias Check:
  [ x] Y-axis mulai dari 0 (atau dijustifikasi)
  [ x] Error bar/CI ditampilkan
  [ x] Semua data disertakan (tidak cherry-picked)
  [ x] Tidak menggunakan 3D tanpa alasan
```
---

## Latihan 1 — Tabel Hasil

Buat tabel hasil eksperimen Anda (boleh dengan data simulasi jika belum punya data riil).

| Skenario | Metrik 1 (mean ± std) | Metrik 2 (mean ± std) | n |
|----------|----------------------|----------------------|---|
|Pengujian Indoor|Akan diperoleh dari eksperimen| Akan diperoleh dari eksperimen | 5 |
| Pengujian Outdoor| Akan diperoleh dari eksperimen|Akan diperoleh dari eksperimen|5 |
| | | | |

**Checklist tabel:**
- [ x] Self-contained (judul jelas, satuan ada, N tercantum)
- [x ] Mean ± std (bukan single number)
- [ x] Diurutkan berdasarkan metrik utama
- [ x] Format konsisten di semua baris

---

## Latihan 2 — Rencana Visualisasi

Rencanakan 2-3 grafik untuk menyajikan data dari Latihan 1. Setiap grafik = satu pesan.

| # | Jenis Grafik | Pesan | Data yang Digunakan |
|---|-------------|-------|---------------------|
|1	|Bar Chart|	Membandingkan akurasi sensor pada dua kondisi pengujian|	Mean akurasi ± standar deviasi|
|2	|Line Chart	|Menampilkan perubahan suhu dan kelembapan terhadap waktu|	Data sensor setiap interval|
|3	|Box Plot|	Menunjukkan distribusi waktu pengiriman data|Seluruh data waktu pengiriman|

---

## Latihan 3 — Bias Detection

Evaluasi visualisasi berikut untuk bias (skenario dari contoh):

**Skenario:** Metode A = 91.2%, Metode B = 90.8%. Bar chart dengan Y-axis mulai dari 90%.

| Pertanyaan | Jawaban |
|-----------|---------|
|Apakah Y-axis menyesatkan?|	Tidak, menggunakan skala yang proporsional.|
|Apakah error bar ditampilkan?|	Ya.|
|Apakah semua kondisi ditampilkan?	|Ya.|
|Apa solusinya?|	Menampilkan seluruh data eksperimen dengan skala yang konsisten dan error bar.|

**Evaluasi grafik Anda sendiri dari Latihan 2:**
- [x] Semua bias check lulus
- [ ] Ada yang perlu diperbaiki: ____

---

## Refleksi

> Mengapa tabel dan grafik keduanya diperlukan — tidak cukup salah satu saja? Pernahkah Anda membuat grafik yang (tanpa sengaja) menyesatkan?

Tabel memberikan informasi numerik secara rinci, sedangkan grafik memudahkan pembaca melihat pola, tren, dan perbandingan hasil eksperimen. Keduanya saling melengkapi sehingga hasil penelitian lebih mudah dipahami. Grafik yang baik juga harus menghindari bias visual, misalnya menggunakan skala yang konsisten, menampilkan error bar, dan menyajikan seluruh data eksperimen secara objektif.
