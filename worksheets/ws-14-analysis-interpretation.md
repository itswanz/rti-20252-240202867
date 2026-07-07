# WS-14: Analysis, Interpretation & Failure Analysis

> **Bab 14 — Analisis Data, Interpretasi & Failure Analysis**

---

## Ringkasan Materi

### Data → Knowledge Model

```
Data → Analysis → Interpretation → Explanation → Knowledge
```

Tiga level yang berbeda:
- **Analysis** — "Apa yang terjadi?" (deskriptif + inferensial)
- **Interpretation** — "Apa artinya?" (konteks RQ + literatur)
- **Failure Analysis** — "Mengapa tidak berhasil?" (boundary conditions)

### Beyond p-value

**Statistical significance ≠ practical significance.** Selalu laporkan:
1. p-value (signifikansi statistik)
2. Effect size (besarnya efek)
3. Confidence interval (rentang ketidakpastian)

| Effect Size (Cohen's d) | Interpretasi |
|-------------------------|-------------|
| < 0.2 | Small |
| 0.2 – 0.8 | Medium |
| > 0.8 | Large |

### Pemilihan Uji Statistik

| Kondisi | Uji yang Tepat |
|---------|---------------|
| 2 grup, normal, paired | Paired t-test |
| 2 grup, non-normal | Wilcoxon signed-rank |
| > 2 grup, normal | One-way ANOVA + post-hoc |
| > 2 grup, non-normal | Kruskal-Wallis + post-hoc |
| 2 variabel kontinu | Pearson (normal) / Spearman (rank) |

### Failure Analysis as Contribution

Hipotesis yang ditolak adalah **temuan yang berharga**:

| Dataset | New (F1) | Baseline (F1) | p-value | Cohen's d |
|---------|---------|--------------|---------|-----------|
| DS-1 (small, clean) | 94.2±1.1 | 89.3±1.5 | <0.001 | **3.7** |
| DS-4 (medium, noisy) | 78.3±3.2 | 82.1±2.8 | 0.008 | **-1.3** |
| DS-5 (large, noisy) | 71.6±4.1 | 80.5±3.0 | <0.001 | **-2.5** |

**Insight:** Metode baru unggul di data bersih tapi gagal di data noisy → asumsi Gaussian dilanggar → **boundary condition** ditemukan → hybrid approach direkomendasikan.

**Partial failure + deep analysis = kontribusi lebih kaya daripada full success tanpa analisis.**

### Limitation Types

| Jenis | Contoh |
|-------|--------|
| Internal validity | Confounders yang tidak dikontrol |
| External validity | Generalisasi ke domain lain |
| Construct validity | Metrik mengukur apa yang dimaksud? |
| Statistical limitation | Sample size, asumsi distribusi |

### Jebakan Kognitif

1. "Signifikan statistik = penting secara praktis" → cek effect size
2. "Hipotesis tidak didukung → cari sudut baru" → p-hacking
3. "Kegagalan tidak perlu dilaporkan detail" → missed insight
4. "Limitasi cukup disebutkan, tidak perlu dianalisis" → kedalaman hilang

---

## Template A.14 — Analysis & Interpretation Report

```
ANALYSIS & INTERPRETATION

1. Statistik Deskriptif:
   | Skenario | Mean | Std | Median | Min | Max | n |
|Mean | Suhu 29,6°C | Kelembapan| 71,8%|
|Standar Deviasi | Suhu ±1,4°C | Kelembapan ±3,2%|
|Median | Suhu 29,5°C | Kelembapan 72%|
|Minimum | Suhu 26,8°C | Kelembapan 65%|
|Maksimum | Suhu 33,1°C | Kelembapan 79%|
|Jumlah Data (n) | 984|


2. Uji Hipotesis:
   Uji yang digunakan  : Paired T-Test
   Justifikasi          :Membandingkan hasil pembacaan sensor DHT22 dengan alat ukur referensi pada kondisi yang sama.
   Hasil:p = 0,032 effect size (d/r/η²) = 0,68
   CI 95%               : [0,18 ; 1,24]
3. Keputusan:
   [x] H₀ ditolak → H₁ diterima
   [ ] H₀ tidak ditolak

4. Interpretasi:
   Hubungan ke RQ       :Sistem IoT berbasis ESP32 dan sensor DHT22 mampu melakukan monitoring suhu dan kelembapan dengan hasil yang konsisten serta memiliki perbedaan yang signifikan dibandingkan pengukuran manual.
   Practical significance: Perbedaan pengukuran relatif kecil sehingga sistem layak digunakan untuk monitoring lingkungan secara real-time.
   Perbandingan literatur: Hasil penelitian sejalan dengan beberapa penelitian sebelumnya yang menyatakan bahwa ESP32 dan DHT22 cukup akurat untuk aplikasi monitoring ruangan.

5. Limitation:
   | Jenis | Ancaman | Dampak | Mitigasi |
   |Internal Validity|Perubahan suhu ruangan secara tiba-tiba.-|Nilai sensor dapat berubah cukup cepat|Melakukan pengambilan data pada kondisi ruangan yang stabil.|
   |External Validity |Pengujian hanya dilakukan pada satu lokasi.|Hasil belum tentu sama pada lingkungan lain.|Melakukan pengujian pada beberapa lokasi berbeda. |

6. Failure Analysis (jika H₀ tidak ditolak):
   Penyebab potensial  : Gangguan koneksi WiFi atau keterlambatan pengiriman data dapat menyebabkan sebagian data tidak terkirim.
   Boundary condition   : Sistem bekerja optimal pada jaringan WiFi yang stabil dan suhu lingkungan normal.
   Insight              : Kualitas jaringan internet memengaruhi kecepatan pengiriman data IoT sehingga perlu dipertimbangkan pada implementasi nyata.
```

---

## Latihan 1 — Pemilihan Uji Statistik

Tentukan uji statistik yang tepat untuk eksperimen Anda.

| Pertanyaan | Jawaban |
|-----------|---------|
| Berapa grup yang dibandingkan? | *Contoh: 3 (BERT, LSTM, SVM)* |
| Apakah data berpasangan (paired)? | |
| Apakah distribusi normal? (uji normalitas) | |
| **Uji yang dipilih:** | |
| **Justifikasi:** | |

**Effect size yang akan dilaporkan:** [ ] Cohen's d / [ ] Eta-squared / [ ] Lainnya: ____

---

## Latihan 2 — Interpretasi Hasil

Gunakan data berikut (atau data riil Anda) untuk berlatih interpretasi.

**Data:**
| Model | Accuracy (mean ± std) | n |
|-------|----------------------|---|
| A | 89.2 ± 1.5 | 10 |
| B | 87.8 ± 2.1 | 10 |

p = 0.045, Cohen's d = 0.74, CI 95% = [0.03, 2.77]

| Aspek | Interpretasi |
|-------|-------------|
| Signifikansi statistik | *Contoh: p < 0.05 → signifikan pada α=0.05* |
| Effect size | *Contoh: d=0.74 → medium-to-large effect* |
| Practical significance | |
| Hubungan ke RQ | |
| Perbandingan literatur | |

---

## Latihan 3 — Failure Analysis

Latih kemampuan failure analysis: hipotesis TIDAK didukung. Apa yang bisa dipelajari?

**Skenario:** Metode baru Anda mendapat F1 = 83.2%, baseline = 84.7%. p = 0.12 (tidak signifikan).

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah ini "gagal"? | Tidak. Hipotesis yang tidak didukung tetap merupakan hasil penelitian yang valid dan dapat menjadi bahan evaluasi.|
| Kemungkinan penyebab? | Gangguan jaringan WiFi, perubahan kondisi lingkungan, atau keterbatasan akurasi sensor. |
| Boundary condition? | Sistem memberikan hasil terbaik pada jaringan stabil dan kondisi lingkungan yang tidak berubah secara ekstrem. |
| Insight yang bisa diambil? | Performa sistem IoT dipengaruhi oleh kualitas jaringan serta kondisi lingkungan sehingga kedua faktor tersebut perlu dikendalikan saat pengujian. |
| Apakah layak dilaporkan? Mengapa? | Ya. Hasil negatif tetap penting karena dapat menjadi referensi bagi penelitian berikutnya dan menghindari pengulangan kesalahan yang sama. |

**Limitation terkait:**
| Jenis | Ancaman | Dampak |
|-------|---------|--------|
| Statistical | Jumlah pengambilan data masih terbatas. | Kepercayaan hasil statistik menjadi lebih rendah dibandingkan jika menggunakan sampel yang lebih banyak. |
| | | |
| | | |

---

## Refleksi

> Apakah "failure" dalam riset benar-benar gagal, atau justru kontribusi? Bagaimana failure analysis mengubah cara Anda melihat hasil negatif?

Failure dalam penelitian bukan berarti penelitian gagal. Hasil yang tidak sesuai hipotesis tetap memberikan informasi penting mengenai batas kemampuan sistem, kondisi ketika metode tidak bekerja secara optimal, serta faktor-faktor yang memengaruhi hasil. Melalui failure analysis, peneliti dapat menemukan penyebab kegagalan, memberikan rekomendasi perbaikan, dan menghasilkan kontribusi ilmiah yang tetap bermanfaat bagi penelitian selanjutnya.
