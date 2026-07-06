# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi

### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

**Perbandingan pendekatan Author-centric vs Concept-centric:**

| Aspek | Author-centric (Hindari) | Concept-centric (Gunakan) |
|-------|--------------------------|---------------------------|
| Struktur | Per penulis/paper ("Rahman et al. menyatakan...") | Per konsep/metode ("Pendekatan berbasis transformer") |
| Tujuan | Ringkasan isi paper | Perbandingan metode & identifikasi gap |
| Contoh paragraph | "Rahman (2023) pakai CNN. Lee (2022) pakai LSTM. Zhang (2021) pakai RF." | "Tiga pendekatan dominan: CNN digunakan oleh 4 paper untuk representasi fitur visual; LSTM untuk data sekuensial; RF sebagai baseline klasik." |
| Hasil akhir | Daftar paper | Peta pengetahuan + gap yang teridentifikasi |

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database utama**: IEEE Xplore, ACM DL, Scopus
   - Akses IEEE/ACM melalui jaringan kampus atau VPN institusi
   - Alternatif bebas biaya: Google Scholar, ResearchGate ([researchgate.net](https://www.researchgate.net)), arXiv ([arxiv.org](https://arxiv.org))
2. **Boolean query** yang terdokumentasi eksplisit
   - Contoh: `("anomaly detection" OR "intrusion detection") AND ("deep learning" OR "neural network") NOT ("medical imaging")`
   - Gunakan tanda kutip untuk frasa eksak; AND/OR/NOT mengontrol scope
3. **Snowballing** — dua arah:
   - **Backward snowballing**: buka daftar referensi di paper kunci → telusuri paper yang dikutip
   - **Forward snowballing**: di Google Scholar, klik "Cited by" di bawah paper kunci → temukan paper yang mengutipnya
   - Ulangi 1–2 tingkat untuk membangun cakupan komprehensif
4. Klaim "belum ada penelitian" harus didukung **bukti pencarian**

### Baseline Selection — 3 Kriteria

| Kriteria | Pertanyaan |
|----------|-----------|
| **Relevan** | Apakah menyelesaikan masalah yang sama? |
| **Representatif** | Apakah mewakili common practice? |
| **State-of-the-Art** | Apakah terbaru/terbaik? |

Membandingkan deep learning 2024 dengan decision tree sederhana tanpa justifikasi = **straw man comparison** (perbandingan tidak jujur).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan baca literatur | Mencari solusi yang sudah ada | Memahami apa yang belum terjawab |
| Cara membaca paper | Tutorial, how-to | Metode, limitasi, gap |
| Baseline | Framework terpopuler | State-of-the-art yang rigorous |
| Dokumentasi pencarian | Tidak diperlukan | Wajib (reproducible) |

### Istilah Penting

- **Concept-centric** — Organisasi literatur berdasarkan konsep/metode, bukan per penulis
- **Snowballing** — Backward (telusuri referensi) + Forward (cari yang mengutip paper kunci)
- **Research Position** — Pernyataan eksplisit posisi riset terhadap studi sebelumnya
- **Straw man comparison** — Memilih baseline lemah agar metode sendiri terlihat lebih baik

---

## Template A.3 — Literature Mapping & Gap Identification

```
LITERATURE MAPPING

Topik      : Analisis Performa Protokol MQTT pada Jaringan Internet of Things (IoT)
Database   : Google Scholar, IEEE Xplore, ResearchGate
Query      :("MQTT" OR "Message Queuing Telemetry Transport") AND ("IoT" OR "Internet of Things") AND ("performance" OR "latency" OR "throughput")
Tahun      : 2020–2026
Hasil awal : 52 paper → Screening → 5 paper final

Literature Matrix (concept-centric):

| Study | Tahun | Method | Data | Result | Limitation |
|-------|-------|--------|------|--------|------------|
|Sharma et al. | 2021  | Evaluasi MQTT QoS     |   Simulasi IoT   | QoS meningkatkan keandalan pesan | Tidak menguji banyak client |

Pola yang ditemukan:
  Metode dominan     : Pengujian latency, QoS, dan load testing pada broker MQTT.
  Dataset umum       : Simulasi jaringan IoT dan perangkat sensor.
  Limitasi berulang  : Sebagian besar penelitian hanya mengukur satu atau dua parameter performa dan belum mengevaluasi latency, throughput, serta packet loss secara bersamaan pada berbagai jumlah client.

GAP IDENTIFICATION

Gap 1: [Jenis: performance / method / data / context]
  Deskripsi    : Sebagian besar penelitian hanya mengukur satu atau dua parameter performa dan belum mengevaluasi latency, throughput, serta packet loss secara bersamaan pada berbagai jumlah client.
  Bukti        : Sebagian besar penelitian hanya berfokus pada latency atau QoS tanpa melakukan evaluasi performa secara menyeluruh.
  Signifikansi : Hasil penelitian dapat memberikan gambaran yang lebih lengkap mengenai kemampuan MQTT dalam menangani komunikasi data pada jaringan IoT dengan banyak perangkat.


Baseline Selection:
| Baseline | Relevansi | Representatif | Source |
|MQTT QoS Level 0|Digunakan sebagai konfigurasi dasar MQTT|Pengaturan default yang paling banyak digunakan|MQTT Specification|
|MQTT QoS Level 1|Digunakan untuk meningkatkan keandalan pengiriman pesan|Banyak digunakan pada implementasi IoT|MQTT Specification
```

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan database akademik.

> **Panduan pencarian:**
> - Database: IEEE Xplore, ACM DL, Google Scholar, atau ResearchGate
> - Tulis query Boolean yang digunakan: contoh `("object detection" OR "image classification") AND ("edge computing") NOT ("medical")`. Dokumentasikan query secara eksplisit.
> - Akses gratis: buka Google Scholar → cari judul paper → klik [PDF] jika tersedia, atau akses lewat campus VPN

**Topik riset:** Analisis Performa Protokol MQTT pada Jaringan Internet of Things (IoT)
**Query pencarian:** ("MQTT" OR "Message Queuing Telemetry Transport") AND ("IoT") AND ("performance" OR "latency" OR "throughput")
**Database:** Google Scholar dan IEEE Xplore

| # | Study | Tahun | Method | Dataset | Result | Limitasi |
|---|-------|-------|--------|---------|--------|----------|
| 1 | *Sharma et al. | 2021 | QoS Analysis | IoT Simulation |Latency rendah | Latency rendah|
| 2 | | | | | | |
| 3 | | | | | | |
| 4 | | | | | | |
| 5 | | | | | | |

**Pola yang terlihat — Metode dominan:** Pengujian latency, QoS, dan load testing pada broker MQTT.
**Limitasi yang berulang:** Belum banyak penelitian yang mengukur latency, throughput, dan packet loss secara bersamaan pada berbagai jumlah client.

---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
| Performance Gap | [x] Ya / [ ] Tidak | Belum banyak penelitian yang mengevaluasi latency, throughput, dan packet loss secara bersamaan.|
| Method Gap | [ ] Ya / [ ] Tidak | |
| Data Gap | [ ] Ya / [ ] Tidak | |
| Context Gap | [x] Ya / [ ] Tidak | Masih sedikit penelitian pada skenario IoT dengan jumlah client yang terus bertambah.|

**Gap utama yang dipilih:** _____________________________
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
> Karena performa komunikasi merupakan faktor utama dalam menentukan keandalan sistem IoT. Evaluasi yang hanya menggunakan satu parameter belum cukup untuk menggambarkan kualitas komunikasi secara menyeluruh, sehingga diperlukan analisis menggunakan beberapa parameter performa sekaligus.

---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
| 1 |MQTT QoS Level 0 | Konfigurasi dasar MQTT | Digunakan secara luas | Bukan, tetapi merupakan standar | MQTT Specification |
| 2 |MQTT QoS Level 1 | Banyak digunakan pada aplikasi IoT|Menjamin pengiriman pesan |Bukan, tetapi common practice | MQTT Specification|


**Apakah pemilihan baseline ini bisa dianggap straw man?** [ ] Ya / [ x] Tidak
> Justifikasi: Kedua baseline merupakan konfigurasi standar MQTT yang umum digunakan pada implementasi IoT sehingga perbandingan dilakukan secara adil dan relevan dengan penelitian.

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> Perbedaan antara klaim "belum ada yang meneliti ini" dan research gap yang valid terletak pada bukti pendukungnya. Klaim tanpa bukti hanya merupakan asumsi peneliti, sedangkan research gap harus didukung oleh hasil penelusuran literatur yang sistematis dari berbagai sumber ilmiah. Suatu gap dapat dibuktikan dengan membandingkan penelitian-penelitian sebelumnya, mengidentifikasi keterbatasan yang berulang, serta menunjukkan aspek yang masih belum terjawab atau belum dievaluasi secara memadai. Dengan demikian, research gap memiliki dasar ilmiah yang jelas dan dapat dipertanggungjawabkan.
