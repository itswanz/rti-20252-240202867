# WS-02: Problem Statement

> **Bab 2 — Problem Formulation & System Context**

---

## Ringkasan Materi

### Problem Formation Model

Masalah riset melewati 5 tahap transformasi. Melompat langsung dari Reality ke Variable adalah kesalahan paling umum.

```
Reality → Observed Issue (Symptom) → Diagnosed Problem (Root Cause)
→ Researchable Problem (Scoped) → Measurable Variable (Operationalized)
```

### Topic ≠ Problem ≠ Research Problem

| Level | Contoh | Status |
|-------|--------|--------|
| **Topik** | Keamanan IoT | Terlalu luas, tidak bisa diuji |
| **Problem** | MQTT tidak terenkripsi | Spesifik tapi belum riset |
| **Research Problem** | Belum ada studi membandingkan overhead TLS 1.3 vs DTLS pada MQTT di IoT RAM < 64KB | Bisa dirancang eksperimennya |

### Symptom vs Root Cause

Apa yang diamati (gejala) ≠ mengapa terjadi (akar masalah). Gunakan **5 Whys** atau **Fishbone Diagram** untuk menggali.

Contoh: "User meninggalkan checkout" (symptom) → "Waktu loading > 8 detik karena API call sequential" (root cause).

### System Thinking

Setiap masalah riset TI harus terikat pada komponen sistem: **Input → Process → Output → Outcome → Constraints → Stakeholders**.

### Problem Quality Check

Masalah riset yang layak harus memenuhi 5 kriteria:
- **Clarity** — Satu orang membaca akan paham
- **Measurability** — Ada metrik kuantitatif
- **Relevance** — Penting untuk domain
- **Testability** — Bisa gagal (falsifiable)
- **Impact** — Ada kontribusi jika terjawab

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Menyelesaikan masalah (*solve*) | Memahami dan membuktikan (*understand & prove*) |
| Masalah | Bug, error, fitur belum ada | Gap dalam pengetahuan |
| Scope | Selesaikan semua yang perlu | Batasi agar bisa dibuktikan |
| Output | Working system | Evidence, paper, replicable findings |

### Istilah Penting

- **Problem Statement** — Formulasi tertulis: konteks sistem + gap + dampak + justifikasi
- **System Context** — Deskripsi lengkap: input, proses, output, outcome, constraints, stakeholders
- **Problem Drift** — Masalah "bermutasi" dari pendahuluan ke metodologi karena statement awal tidak presisi
- **Solution-First Thinking** — Memulai dari solusi tanpa masalah yang jelas — berbahaya dalam riset
- **Operational Definition** — Definisi variabel yang cukup jelas agar peneliti lain bisa mengukur hal yang sama

---

## Template A.2 — Problem Statement Builder

```
PROBLEM STATEMENT BUILDER

Domain & Konteks
  Domain   : Internet of Things (IoT) & Network Communication
  Konteks  : Penggunaan protokol MQTT untuk komunikasi data antar perangkat IoT

System Context
  Input       : Jumlah client MQTT, ukuran payload, dan QoS (Quality of Service)
  Process     : Broker MQTT menerima, memproses, dan mendistribusikan pesan ke setiap client.
  Output      : Nilai latency, throughput, dan packet loss komunikasi data.
  Outcome     : Komunikasi data IoT yang cepat, stabil, dan andal.
  Constraints : Keterbatasan bandwidth jaringan, kapasitas broker, dan spesifikasi perangkat IoT.
  Stakeholders: Pengembang IoT, peneliti, dan industri yang menggunakan sistem IoT.

Fenomena → Problem
  Fenomena yang diamati             : Performa komunikasi MQTT menurun ketika jumlah perangkat IoT yang terhubung meningkat.
  Gejala (symptom) yang terukur     : Terjadi peningkatan latency dan penurunan throughput saat jumlah client bertambah.
  Masalah yang didiagnosis          : Broker MQTT mengalami peningkatan beban sehingga waktu pemrosesan dan distribusi pesan menjadi lebih lama.
  Masalah riset (researchable)      : Bagaimana pengaruh jumlah client terhadap performa protokol MQTT berdasarkan latency, throughput, dan packet loss pada jaringan IoT?
  Variabel yang terukur             : Latency (ms), Throughput (Mbps), dan Packet Loss (%).

Problem Quality Check
  [x] Clarity — Apakah satu orang membaca akan paham?
  [x] Measurability — Apakah ada metrik kuantitatif?
  [x] Relevance — Apakah penting untuk domain?
  [x] Testability — Apakah bisa gagal?
  [x] Impact — Apakah ada kontribusi jika terjawab?

Problem Statement (1 paragraf):
  Protokol MQTT banyak digunakan pada sistem Internet of Things (IoT) karena ringan dan efisien dalam komunikasi data. Namun, ketika jumlah perangkat yang terhubung ke broker meningkat, performa komunikasi dapat mengalami penurunan yang ditandai dengan meningkatnya latency serta menurunnya throughput. Kondisi ini berpotensi mengurangi keandalan sistem IoT, terutama pada aplikasi yang membutuhkan pertukaran data secara real-time. Oleh karena itu, penelitian ini bertujuan menganalisis pengaruh jumlah client terhadap performa protokol MQTT menggunakan parameter latency, throughput, dan packet loss sehingga dapat diperoleh gambaran mengenai batas kemampuan komunikasi MQTT pada lingkungan IoT.
```

---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:** Optimasi Performa iGPU Ryzen untuk Gaming
| Tahap | Hasil |
|-------|-------|
| Reality | Semakin banyak sistem IoT menggunakan protokol MQTT untuk komunikasi data antar perangkat secara real-time. |
| Observed Issue (Symptom) |Latency meningkat dan pengiriman data menjadi lebih lambat ketika jumlah perangkat bertambah. |
| Diagnosed Problem (Root Cause) |Broker MQTT mengalami peningkatan beban sehingga waktu pemrosesan dan distribusi pesan menjadi lebih lama.|
| Researchable Problem |Bagaimana pengaruh jumlah client terhadap performa protokol MQTT berdasarkan latency, throughput, dan packet loss pada jaringan IoT? |
| Measurable Variable |Latency (ms), Throughput (Mbps), dan Packet Loss (%).|

**Apakah terjebak solution-first thinking?** [ ] Ya / [x] Tidak
> Jika ya, kembali ke tahap mana? ________________________

---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input | Jumlah client MQTT, ukuran payload, dan QoS (Quality of Service). |
| Process |Broker MQTT menerima, memproses, dan mendistribusikan pesan ke seluruh client yang terhubung.|
| Output |Nilai latency, throughput, dan packet loss hasil komunikasi data. |
| Outcome |Komunikasi data IoT yang stabil, cepat, dan andal.|
| Constraints |Kapasitas broker, bandwidth jaringan, dan spesifikasi perangkat IoT.|
| Stakeholders |Pengembang IoT, peneliti, dan industri yang memanfaatkan sistem IoT. |

**Komponen mana yang paling relevan dengan masalah riset?** Process, karena proses pemrosesan dan distribusi pesan pada broker MQTT secara langsung memengaruhi performa komunikasi.

---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity | 5 | Fokus penelitian jelas, yaitu menganalisis performa MQTT berdasarkan jumlah client.|
| Measurability |5 | Latency, throughput, dan packet loss dapat diukur secara kuantitatif.|
| Relevance |4 |Sangat relevan dengan perkembangan teknologi Internet of Things|
| Testability | 4| Hipotesis dapat diuji melalui simulasi atau eksperimen dengan variasi jumlah client.|
| Impact |4|Hasil penelitian dapat menjadi referensi dalam merancang sistem IoT yang lebih efisien.|

**Skor total:** 23 / 25

**Problem statement versi final (1 paragraf):**
> Protokol MQTT merupakan salah satu protokol komunikasi yang banyak digunakan pada sistem Internet of Things (IoT) karena ringan dan efisien. Namun, peningkatan jumlah perangkat yang terhubung dapat menyebabkan penurunan performa komunikasi berupa meningkatnya latency, menurunnya throughput, dan kemungkinan terjadinya packet loss. Kondisi tersebut dapat memengaruhi keandalan sistem, khususnya pada aplikasi IoT yang membutuhkan komunikasi data secara real-time. Oleh karena itu, penelitian ini bertujuan menganalisis pengaruh jumlah client terhadap performa protokol MQTT berdasarkan parameter latency, throughput, dan packet loss sehingga dapat memberikan gambaran mengenai kemampuan protokol MQTT dalam mendukung komunikasi pada jaringan IoT

---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
> Perbedaan fundamental antara masalah coding dan masalah riset terletak pada tujuan penyelesaiannya. Masalah coding, seperti bug atau error, berfokus pada memperbaiki sistem agar dapat berjalan sesuai fungsinya. Sementara itu, masalah riset berfokus pada menemukan atau membuktikan pengetahuan baru melalui proses ilmiah yang sistematis. Dalam coding, solusi yang berhasil menjadi tujuan utama, sedangkan dalam riset, hasil yang tidak sesuai hipotesis tetap memiliki nilai karena dapat menjadi bukti ilmiah dan memberikan pemahaman baru terhadap suatu permasalahan.
