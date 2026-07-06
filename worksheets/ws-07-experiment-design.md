# WS-07: Experimental Design & Validity

> **Bab 7 — Experimental Design & Validity**

---

## Ringkasan Materi

### Correlation ≠ Causality

Kausalitas membutuhkan 3 syarat:
1. **Covariance** — X dan Y bergerak bersama
2. **Temporal precedence** — X berubah sebelum Y
3. **Elimination of alternatives** — Tidak ada faktor lain yang menjelaskan Y

Controlled experiment adalah satu-satunya metode yang bisa membuktikan kausalitas.

### Empat Jenis Validitas

| Jenis | Pertanyaan | Ancaman Umum |
|-------|-----------|-------------|
| **Internal** | Apakah hubungan IV→DV nyata? | Confounding variable, selection bias |
| **External** | Apakah bisa digeneralisasi? | Dataset terlalu spesifik |
| **Construct** | Apakah mengukur konsep yang benar? | Metrik tidak sesuai |
| **Conclusion** | Apakah kesimpulan statistik valid? | Sample size kecil, uji salah |

Internal dan external validity sering berkonflik: semakin terkontrol (internal kuat) → semakin artificial (external lemah).

### Tiga Tipe Eksperimen dalam Riset TI

| Tipe | Deskripsi | Kapan Digunakan |
|------|----------|----------------|
| **Comparison Study** | Metode A vs B pada kondisi identik | Membandingkan pendekatan berbeda |
| **Ablation Study** | Full system → lepas komponen satu per satu | Mengukur kontribusi tiap komponen |
| **Parameter Study** | Variasikan satu parameter, amati dampak | Uji sensitifitas/robustness |

### Fairness dalam Perbandingan

Perbandingan yang adil = **kondisi identik** untuk semua metode: dataset sama, preprocessing sama, tuning effort sebanding, environment sama, metrik sama.

Contoh tidak adil: Transformer (30 fitur tambahan + Bayesian optimization) vs RF (default params) → hasilnya misleading.

### Threats to Validity = Diidentifikasi Sebelum Eksperimen

Ancaman validitas harus diidentifikasi **sebelum** eksperimen dan mitigasinya dirancang sebagai bagian dari desain — bukan ditulis sebagai boilerplate setelah selesai.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan testing | Memastikan sistem memenuhi requirement | Membuktikan hubungan kausal antar variabel |
| Baseline | Versi sebelumnya (last release) | Metode tervalidasi dari literatur |
| Kegagalan | Bug → fix → release | H₀ tidak ditolak → tetap kontribusi ilmiah |
| Sukses | 100% test pass | Evidence valid — mendukung atau menolak hipotesis |

### Istilah Penting

- **Causality** — Hubungan sebab-akibat (covariance + temporal + elimination)
- **Controlled Experiment** — Ubah satu variabel, kontrol sisanya, amati efek
- **Fairness** — Semua metode diuji pada kondisi yang benar-benar identik
- **Threats to Validity** — Faktor yang bisa melemahkan kesimpulan jika tidak dimitigasi
- **Conclusion Validity** — Validitas statistik: power, sample size, uji yang tepat

---

## Template A.7 — Desain Eksperimen Lengkap

```
EXPERIMENT DESIGN

Research Question : Bagaimana pengaruh jumlah client terhadap performa protokol MQTT pada jaringan Internet of Things berdasarkan latency, throughput, dan packet loss?

Hypothesis        : Peningkatan jumlah client memberikan perbedaan signifikan terhadap latency, throughput, dan packet loss.

Tipe Eksperimen   : [x] Comparison  [ ] Ablation  [ ] Parameter

Kondisi Eksperimen:

| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control | Beban komunikasi rendah | 10 Client | QoS 1, Payload 256 Byte, Broker MQTT, Jaringan yang sama |
| Treatment | Beban komunikasi tinggi | 100 Client | QoS 1, Payload 256 Byte, Broker MQTT, Jaringan yang sama |

Fairness Checklist:
  [x] Dataset identik untuk semua kondisi
  [x] Preprocessing setara
  [x] Tuning effort setara
  [x] Environment identik
  [x] Metrik evaluasi sama

Threat Analysis:

| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal | Aplikasi lain menggunakan bandwidth jaringan selama pengujian. | Menutup seluruh aplikasi yang tidak diperlukan dan menggunakan jaringan khusus untuk eksperimen. |
| External | Hasil hanya berlaku pada konfigurasi broker dan jaringan yang digunakan. | Menjelaskan batasan penelitian serta menggunakan konfigurasi yang terdokumentasi. |
| Construct | Latency dipengaruhi oleh kondisi jaringan di luar sistem MQTT. | Menggunakan jaringan lokal yang stabil selama seluruh eksperimen. |
| Conclusion | Jumlah pengujian terlalu sedikit sehingga hasil kurang mewakili. | Melakukan minimal lima kali pengulangan untuk setiap kondisi dan menghitung nilai rata-rata serta standar deviasi. |

Statistical Plan:
  Uji statistik   : Independent Samples T-Test
  Justifikasi     : Membandingkan rata-rata performa antara dua kelompok pengujian dengan jumlah client yang berbeda.
  Alpha           : 0.05 (Tingkat kepercayaan 95%)
  Effect size min : Cohen's d > 0.5

---

# Latihan 1 — Desain Eksperimen

RQ:
Bagaimana pengaruh jumlah client terhadap performa protokol MQTT pada jaringan Internet of Things?

Tipe eksperimen: [x] Comparison / [ ] Ablation / [ ] Parameter

| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control | Jumlah client rendah | 10 Client | Payload 256 Byte, QoS 1, Broker MQTT yang sama |
| Treatment | Jumlah client tinggi | 100 Client | Payload 256 Byte, QoS 1, Broker MQTT yang sama |

---

# Latihan 2 — Fairness Checklist

| Kriteria | Status | Detail |
|----------|--------|--------|
| Dataset identik | ✅ | Seluruh pengujian menggunakan skenario komunikasi dan payload yang sama. |
| Preprocessing setara | ✅ | Konfigurasi broker dan QoS tidak diubah selama eksperimen. |
| Tuning effort setara | ✅ | Semua kondisi menggunakan konfigurasi broker yang identik. |
| Environment identik | ✅ | Pengujian dilakukan pada jaringan dan perangkat yang sama. |
| Metrik evaluasi sama | ✅ | Semua kondisi dievaluasi menggunakan latency, throughput, dan packet loss. |

Ada yang tidak fair? [ ] Ya / [x] Tidak

Jika ya, bagaimana cara memperbaikinya? __________________

---

# Latihan 3 — Threat Analysis

| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal | Trafik jaringan lain memengaruhi hasil pengujian. | Menggunakan jaringan lokal khusus selama eksperimen. |
| External | Hasil mungkin berbeda pada broker MQTT atau topologi jaringan lain. | Menjelaskan ruang lingkup penelitian dan spesifikasi sistem yang digunakan. |
| Construct | Latency dipengaruhi kondisi jaringan, bukan hanya performa MQTT. | Menjaga kondisi jaringan tetap stabil dan melakukan pengujian berulang. |
| Conclusion | Jumlah sampel pengujian kurang banyak. | Melakukan minimal lima kali pengulangan dan menggunakan analisis statistik. |

Ancaman mana yang paling sulit dimitigasi?

External (Perbedaan kondisi jaringan dan broker MQTT)

Mengapa?

Karena performa MQTT dapat dipengaruhi oleh jenis broker, spesifikasi perangkat, dan kondisi jaringan yang berbeda. Walaupun konfigurasi eksperimen dibuat sebaik mungkin, hasil penelitian belum tentu dapat digeneralisasikan ke seluruh lingkungan IoT yang memiliki karakteristik jaringan berbeda.

---

# Refleksi

Jawaban:

1. Apakah seluruh baseline diuji menggunakan konfigurasi, dataset, dan lingkungan yang sama sehingga perbandingan benar-benar adil? (Fairness)

2. Apakah peningkatan performa yang dilaporkan didukung oleh analisis statistik yang menunjukkan perbedaan signifikan, bukan hanya selisih angka? (Conclusion Validity)

3. Apakah metode pengukuran dan metrik yang digunakan benar-benar mewakili tujuan penelitian sehingga hasilnya dapat dipercaya? (Construct Validity)

**Jawaban:**
1.Apakah baselinenya sudah diatur dengan konfigurasi optimal (best-effort) atau hanya menggunakan pengaturan default yang lemah?" (Fairness Check)_
2. Apakah environment pengujian (hardware, software version, dataset) identik untuk semua metode?" (Internal Validity)
3. Bagaimana signifikansi statistiknya? Apakah peningkatannya nyata atau hanya fluktuasi margin of error?" (Conclusion Validity)
