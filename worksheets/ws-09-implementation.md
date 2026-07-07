# WS-09: Implementation & Environment

> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**

---

## Ringkasan Materi

### Implementasi Riset ≠ Coding Biasa

Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.

> **Mengapa reproducibility penting?** Sains dibangun di atas prinsip verifikasi — temuan harus bisa dikonfirmasi oleh peneliti lain. _Replicability crisis_ yang terjadi di banyak paper riset ML/AI disebabkan oleh environment tidak terdokumentasi: orang lain tidak bisa reproduksi, hasil diragukan, kepercayaan terhadap temuan hilang. Prinsip: **dokumentasi environment = snapshot kredibilitas riset Anda.**

### Reproducible Implementation Model

```
Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result
```

Setiap transisi memiliki syarat:
- Design → Implementation: kode sesuai mapping variabel-ke-komponen
- Implementation → Environment: versi, dependency, seed, path, OS eksplisit
- Environment → Consistency: seed terkunci, urutan deterministik
- Consistency → Reproducibility: dokumentasi lengkap
- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa

### Repeatability vs Reproducibility

| Level | Peneliti | Environment | Hasil |
|-------|---------|-------------|-------|
| **Repeatability** | Sama | Sama | Sama persis |
| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |

Capai **repeatability** dulu, baru **reproducibility**.

### Engineering vs Research Perspective

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |
| Dependency | Update ke terbaru | Lock di versi spesifik |
| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |
| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |
| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |

### Jebakan Kognitif

1. Menunda environment setup → bug sulit dilacak
2. Tidak pakai version control → hasil tidak bisa direkonstruksi
3. Menolak Docker/container → "di laptop saya bisa" saat review
   - **Docker** = teknologi container yang "membungkus" aplikasi beserta seluruh dependency-nya dalam satu unit terisolasi. Hasilnya: kode berjalan identik di laptop, server, maupun reviewer lain. Intro singkat: `docker run -v $(pwd):/workspace environment-image python run_experiment.py`
4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)

### Dependency Locking

Mengandalkan "install library terbaru" berbahaya: versi berbeda = perilaku berbeda = hasil tidak reproducible. Praktik:
- **Python**: buat `requirements.txt` dengan versi eksplisit: `scikit-learn==1.3.2`, lalu kunci dengan `pip freeze > requirements.txt`
- **Conda**: gunakan `conda env export > environment.yml` untuk snapshot lengkap
- **Node.js/R/Julia**: gunakan `package-lock.json` / `renv.lock` / `Project.toml` — semua fungsi serupa: lock versi + hash

### Istilah Penting

- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed
- **Dependency** — Komponen eksternal yang harus di-lock versinya
- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode

---

## Template A.9 — Dokumentasi Setup Eksperimen

```
EXPERIMENT SETUP DOCUMENTATION

Hardware:
  CPU     : Intel Core i5-12400
  RAM     : 16 GB DDR4
  Network : LAN 1 Gbps
  Storage : SSD 512 GB

Software:
  OS        : Windows 11 Pro 64-bit
  Runtime   : Python 3.12
  Framework : Eclipse Paho MQTT + Eclipse Mosquitto Broker

Dependencies:

| Library | Version | Sumber | Hash/Checksum |
|---------|---------|--------|---------------|
| paho-mqtt | 2.1.0 | PyPI | - |
| pandas | 2.2.2 | PyPI | - |
| numpy | 2.1.0 | PyPI | - |
| matplotlib | 3.9.0 | PyPI | - |
| psutil | 6.0.0 | PyPI | - |

Konfigurasi:
  Config file     : config.json
  Random seed     : 42
  Hyperparameters : Jumlah client (10, 50, 100), QoS 0, Payload 256 Byte

Reproducibility Check:
  [x] Dependency terdokumentasi (requirements.txt / lock file)
  [x] Seed ditetapkan di semua level
  [x] Config di version control
  [x] README instruksi reproduksi lengkap
```

---

## Latihan 1 — Environment Specification

Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).

| Komponen | Spesifikasi |
|----------|------------|
| CPU | Amd Rayzen5 5560GT |
| RAM | 16GB GDDR4 |
| GPU |Rayzen RX 6600 8GB|
| OS | Windows 11 |
| Runtime | Python 3.12|
| Framework | Eclipse Paho MQTT + Eclipse Mosquitto Broker|
| Random Seed |42 |

**Dependencies (minimal 5):**

| Library | Version | Alasan Dibutuhkan |
|---------|---------|-------------------|
| paho-mqtt | 2.1.0 | Implementasi komunikasi MQTT |
| pandas | 2.2.2 | Mengolah data hasil pengujian |
| numpy | 2.1.0 | Perhitungan numerik |
| matplotlib | 3.9.0 | Visualisasi grafik performa |
| psutil | 6.0.0 | Monitoring penggunaan resource sistem |

---

## Latihan 2 — Repeatability Test Plan

Rancang tes repeatability sederhana: jalankan kode yang sama 3× di environment yang sama.

| Run | Seed | Metrik Utama | Hasil Sama? |
|-----|------|-------------|-------------|
| 1 | 42 | Latency rata-rata | — |
| 2 | 42 | Latency rata-rata | [x] Ya |
| 3 | 42 | Latency rata-rata | [x] Ya |

**Jika hasil berbeda, kemungkinan penyebab:**

> Penyebab umum non-repeatability:
- Beban jaringan berubah selama pengujian.
- Broker MQTT menerima trafik dari perangkat lain.
- Background process pada sistem memengaruhi performa.
- Random seed belum diterapkan secara konsisten.


___________________________________________________

- [x] Random seed di-set di semua level
- [x] Tidak ada background process yang mengganggu
- [x] Jaringan hanya digunakan untuk eksperimen
- [x] Config file yang sama untuk semua run

---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen: Analisis Performa Protokol MQTT pada Jaringan Internet of Things (IoT)

## 1. Environment

- OS : Windows 11 Pro 64-bit
- Runtime : Python 3.12
- MQTT Broker : Eclipse Mosquitto
- MQTT Client : Eclipse Paho MQTT
- RAM : 16 GB DDR4
- Network : LAN 1 Gbps

## 2. Installation

1. Install Python 3.12
2. Install Eclipse Mosquitto Broker
3. Install dependency:

```bash
pip install -r requirements.txt
```

## 3. Data

Data diperoleh dari hasil komunikasi antara MQTT Client dan MQTT Broker berupa nilai latency, throughput, dan packet loss yang disimpan dalam format CSV.

## 4. Execution

Jalankan broker terlebih dahulu kemudian jalankan publisher, subscriber, dan logger.

```bash
python publisher.py
python subscriber.py
python logger.py
```

## 5. Configuration

Seluruh parameter eksperimen disimpan pada file **config.json**, meliputi:

- Jumlah client
- QoS
- Payload Size
- Jumlah pengiriman pesan

## 6. Expected Output

Eksperimen menghasilkan:

- File CSV hasil pengukuran
- Nilai Latency (ms)
- Throughput (Mbps)
- Packet Loss (%)
- Grafik performa MQTT
```

---

## Refleksi

>Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda?

**Level saat ini:** [ ] Repeatability / [x] Reproducibility / [ ] Belum keduanya

**Komponen yang belum terdokumentasi:**

Dokumentasi topologi jaringan, contoh file **config.json**, serta langkah konfigurasi Mosquitto Broker agar peneliti lain dapat mereplikasi eksperimen dengan hasil yang serupa.
