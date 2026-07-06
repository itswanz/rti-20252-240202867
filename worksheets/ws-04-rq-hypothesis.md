# WS-04: Research Question & Hypothesis

> **Bab 4 — Research Question, Contribution & Hypothesis**

---

## Ringkasan Materi

### RQ Bukan Pertanyaan Biasa

Research Question yang baik secara implisit mengandung cetak biru eksperimen: subjek, baseline, metrik, domain, dataset.

| Kualitas | Contoh |
|----------|--------|
| **Buruk** | "Bagaimana pengaruh deep learning terhadap deteksi malware?" |
| **Baik** | "Apakah CNN menghasilkan F1-Score lebih tinggi dari RF pada CIC-MalMem-2022?" |

Perbedaan: RQ yang baik menyebutkan **metode spesifik**, **metrik terukur**, **baseline**, dan **dataset**.

### Tiga Jenis RQ

| Jenis | Pola | Kebutuhan |
|-------|------|-----------|
| **Comparison** | A vs B → mana lebih baik? | ≥ 2 metode, metrik sama |
| **Improvement** | A' vs A → modifikasi lebih baik? | Pre/post, bukti perbaikan |
| **Exploratory** | Faktor X₁...Xₙ → pengaruh terhadap Y? | Multi-variabel, korelasi/regresi |

### Contribution Statement

Tiga jenis kontribusi: **Improvement** (metode terbukti lebih baik), **Comparison** (perbandingan sistematis yang belum ada), **Novel Approach** (pendekatan baru). Kontribusi harus terhubung langsung dengan gap — kontribusi tanpa gap = klaim tanpa justifikasi.

### Hypothesis H₀ / H₁

- **H₀** (Null) = Tidak ada perbedaan signifikan — asumsi default, harus dibuktikan salah
- **H₁** (Alternative) = Ada perbedaan signifikan — diterima hanya jika H₀ ditolak
- Harus **falsifiable**, mengandung **metrik terukur**, dirumuskan **SEBELUM eksperimen**

### Rantai Operasionalisasi

```
RQ → Variable → Metric → Data → Analysis
```

Jika rantai ini tidak lengkap, RQ belum mature. Bi-directional: RQ yang tidak bisa jadi hipotesis testable harus direvisi mundur.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan pertanyaan | Apa yang harus dibangun? | Apa yang harus dibuktikan? |
| Bentuk jawaban | Sistem yang berfungsi | Bukti empiris terukur |
| Sukses diukur oleh | User satisfaction, uptime | Signifikansi statistik, effect size |
| Jika gagal | Debug dan perbaiki | Laporkan, analisis mengapa |

### Istilah Penting

- **Research Question (RQ)** — Pertanyaan spesifik: variabel terukur + metrik + konteks
- **Contribution Statement** — Apa yang diketahui setelah riset selesai yang sebelumnya belum ada
- **H₀ / H₁** — Null vs Alternative Hypothesis
- **Falsifiability** — Kondisi hipotesis ditolak harus bisa didefinisikan sebelum eksperimen
- **Operationalization** — Proses mewujudkan konsep abstrak menjadi variabel terukur

---

## Template A.4 — RQ-Contribution-Hypothesis

```
RQ-CONTRIBUTION-HYPOTHESIS

Gap Statement  : Kurangnya penelitian yang menganalisis performa protokol MQTT menggunakan kombinasi metrik latency, throughput, dan packet loss pada kondisi jumlah client yang bervariasi.

Research Question:
  Tipe         : [ ] Comparison  [ ] Improvement  [x] Exploratory
  Formulasi    : Bagaimana pengaruh jumlah client terhadap performa protokol MQTT pada jaringan Internet of Things berdasarkan latency, throughput, dan packet loss?
  Variabel IV  : Jumlah client MQTT
  Variabel DV  : Latency, Throughput, dan Packet Loss
  Metrik       : Latency (ms), Throughput (Mbps), Packet Loss (%)
  Dataset      : Simulasi komunikasi perangkat IoT menggunakan broker MQTT
  Baseline     : Pengujian dengan jumlah client rendah (10 client)

Quality Check RQ:
  [x] Variabel spesifik
  [x] Metrik jelas
  [x] Baseline ada
  [x] Konteks disebutkan
  [x] Memerlukan eksperimen (bukan hanya survei literatur)

Contribution Statement:
  Apa yang baru diketahui : Pengaruh peningkatan jumlah client terhadap performa komunikasi MQTT berdasarkan beberapa metrik secara bersamaan.
  Jenis kontribusi        : [ ] Improvement  [x] Comparison  [ ] Novel approach
  Gap yang diisi          : Mengisi performance gap mengenai evaluasi performa MQTT pada berbagai jumlah client.

Hypothesis Pair:
  H₀ : Tidak terdapat perbedaan signifikan pada latency, throughput, dan packet loss ketika jumlah client MQTT bertambah.
  H₁ : Peningkatan jumlah client MQTT memberikan perbedaan signifikan terhadap latency, throughput, dan packet loss.
  Threshold              : Perubahan latency minimal 10% disertai perubahan throughput atau packet loss.
  Justifikasi threshold  : Perubahan sebesar 10% dianggap cukup untuk menunjukkan adanya perubahan performa komunikasi yang dapat diukur secara statistik.
```

---

## Latihan 1 — Dari Gap ke RQ

Kurangnya penelitian yang mengevaluasi performa MQTT menggunakan kombinasi latency, throughput, dan packet loss pada jumlah client yang berbeda.

RQ versi pertama (tulis bebas):

Bagaimana pengaruh jumlah client terhadap performa komunikasi protokol MQTT pada jaringan Internet of Things?

Evaluasi RQ:

Komponen	Ada?	Isi
Metode spesifik	Ya	Pengujian performa MQTT dengan variasi jumlah client
Metrik terukur	Ya	Latency, Throughput, dan Packet Loss
Baseline	Ya	Pengujian dengan jumlah client rendah (10 client)
Dataset/konteks	Ya	Simulasi komunikasi perangkat IoT menggunakan broker MQTT

Tipe RQ:
[ ] Comparison / [ ] Improvement / [x] Exploratory

RQ versi revisi (setelah evaluasi):

Bagaimana pengaruh variasi jumlah client terhadap performa protokol MQTT pada jaringan Internet of Things berdasarkan metrik latency, throughput, dan packet loss?

---

## Latihan 2 — Hypothesis Pair

Rumuskan pasangan hipotesis dari RQ di Latihan 1.

Komponen	Isi
H₀	Penambahan jumlah client tidak memberikan perbedaan signifikan terhadap latency, throughput, dan packet loss.
H₁	Penambahan jumlah client memberikan perbedaan signifikan terhadap latency, throughput, dan packet loss.
Metrik	Latency (ms), Throughput (Mbps), Packet Loss (%)
Threshold	Perubahan minimal 10% pada salah satu metrik performa.

Apakah hipotesis ini falsifiable? [x] Ya / [ ] Tidak

Bagaimana cara membuktikannya salah?

Melakukan pengujian menggunakan beberapa variasi jumlah client, kemudian membandingkan hasil latency, throughput, dan packet loss menggunakan analisis statistik. Apabila tidak ditemukan perbedaan yang signifikan, maka hipotesis alternatif (H₁) ditolak dan H₀ diterima.
---

## Latihan 3 — Rantai Operasionalisasi

Lengkapi rantai dari RQ hingga metode analisis.

| Tahap	Isi
RQ	Bagaimana pengaruh jumlah client terhadap performa protokol MQTT?
Variable (IV)	Jumlah client MQTT
Variable (DV)	Latency, Throughput, dan Packet Loss
Metric	Latency (ms), Throughput (Mbps), Packet Loss (%)
Data source	Hasil pengujian komunikasi pada broker MQTT
Analysis method	Analisis komparatif dan statistik terhadap hasil pengujian

Apakah rantai lengkap? [x] Ya / [ ] Tidak

Jika tidak, tahap mana yang perlu direvisi? __________________

---

## Refleksi

> Ambil satu judul skripsi/paper yang pernah dibaca. Coba ekstrak RQ-nya. Apakah RQ tersebut memenuhi semua komponen (metode, metrik, baseline, konteks)? Jika tidak, apa yang hilang?

**Judul:** Performance Analysis of MQTT Protocol in Internet of Things Applications
**RQ yang diekstrak:**Bagaimana pengaruh jumlah client terhadap performa protokol MQTT berdasarkan latency dan throughput?
**Komponen yang hilang:**RQ tersebut belum menyebutkan baseline yang digunakan sebagai pembanding, belum menjelaskan skenario pengujian secara rinci, serta belum memasukkan metrik packet loss sehingga evaluasi performanya belum sepenuhnya komprehensif.
