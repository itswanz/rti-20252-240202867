# WS-06: System-Experiment Mapping

> **Bab 6 — System Design sebagai Experimental Artifact**

---

## Ringkasan Materi

### Sistem = Instrumen Pengujian, Bukan Produk

Seorang engineer bertanya "apakah sistem bekerja?" — seorang peneliti bertanya "apa yang bisa dibuktikan sistem ini?" Sistem dalam riset adalah **artifact** — objek yang sengaja dibuat untuk menguji klaim spesifik.

### System as Experiment Model

```
RQ → Variable → System Component → Experimental Setup → Output
```

Setiap komponen sistem harus bisa ditelusuri ke variabel riset (top-down), dan setiap pengukuran harus menjawab RQ (bottom-up).

### Mapping Variabel ke Komponen

| Tipe Variabel | Peran di Sistem | Contoh |
|---------------|----------------|--------|
| **IV** (Independent) | Modul yang bisa di-toggle/swap | Algoritma A vs B |
| **DV** (Dependent) | Modul pengukuran | Logger, metrics collector |
| **CV** (Control) | Config yang dikunci | Dataset, parameter tetap |

Jika variabel tidak bisa di-map ke komponen apapun → arsitektur perlu didesain ulang.

### 4 Prinsip Desain Eksperimental

| Prinsip | Pertanyaan Kunci |
|---------|-----------------|
| **Traceability** | Komponen ini melayani variabel yang mana? |
| **Modularity** | Bisakah IV diubah tanpa memengaruhi yang lain? |
| **Controllability** | Apakah CV dieksternalisasi ke config file? |
| **Measurability** | Apakah sistem otomatis menghasilkan data yang dibutuhkan? |

### Variable Isolation melalui Arsitektur

- **Modular architecture** — Pisahkan berdasarkan variabel
- **Configuration-driven** — Ubah config (YAML/JSON), bukan code
- **Feature toggles** — On/off flag untuk ablation study

  Contoh config YAML dengan feature toggles:
  ```yaml
  model:
    type: cnn          # IV: ganti "rf" untuk kondisi baseline
  features:
    use_temporal: true  # toggle komponen temporal
    use_normalization: true  # toggle preprocessing
  experiment:
    seed: 42
    runs: 5
  ```
  Dengan pendekatan ini, berbeda kondisi eksperimen = berbeda satu baris config, **tanpa mengubah kode**.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan sistem | Memenuhi kebutuhan user | Menguji hipotesis, menghasilkan bukti |
| Arsitektur | Optimasi performa & skalabilitas | Optimasi isolasi variabel & reprodusibilitas |
| Konfigurasi | Sering hardcoded | Dieksternalisasi ke config file |
| Fitur tambahan | Menambah nilai user | Menambah noise jika tidak terkait RQ |

### Istilah Penting

- **Artifact** — Objek yang sengaja dibuat untuk memecahkan masalah atau menguji proposisi
- **Traceability** — Kemampuan menelusuri hubungan RQ → variabel → komponen → output
- **Variable Isolation** — Mengubah hanya satu variabel sambil menahan yang lain konstan
- **Ablation Study** — Menguji kontribusi tiap komponen dengan melepasnya satu per satu
- **Configuration-driven Execution** — Semua parameter di config file, bukan hardcoded

---

## Template A.6 — Mapping RQ ke Arsitektur Sistem

```
SYSTEM-EXPERIMENT MAPPING

Research Question:
Bagaimana pengaruh jumlah client terhadap performa protokol MQTT pada jaringan Internet of Things berdasarkan latency, throughput, dan packet loss?

Variable → Component Mapping:

| Variabel | Tipe | Komponen Sistem | Cara Manipulasi/Pengukuran |
|----------|------|-----------------|---------------------------|
|Jumlah Client MQTT|IV|MQTT Client Simulator|Mengubah jumlah client yang terhubung ke broker (10, 50, 100 client)|
|Performa MQTT|DV|MQTT Monitoring & Logger|Mencatat latency, throughput, dan packet loss secara otomatis|
|Ukuran Payload|CV|MQTT Publisher Configuration|Menggunakan ukuran payload yang sama pada setiap pengujian|

4 Prinsip Desain:
  [x] Traceability — Setiap komponen bisa ditelusuri ke variabel
  [x] Variable Isolation — IV bisa diubah tanpa mengubah CV
  [x] Measurement Integration — Pengukuran DV built-in
  [x] Reproducibility — Setup bisa direkonstruksi

Experimental Setup:
  Input data     : Simulasi komunikasi perangkat IoT menggunakan broker MQTT
  Parameter      : Broker MQTT, ukuran payload tetap, QoS 1, variasi jumlah client
  Output format  : File CSV berisi latency, throughput, dan packet loss

---

# Latihan 1 — Variable-to-Component Mapping

RQ:
Bagaimana pengaruh jumlah client terhadap performa protokol MQTT pada jaringan Internet of Things?

| Variabel | Tipe | Komponen Sistem | Cara Manipulasi / Pengukuran |
|----------|------|-----------------|------------------------------|
|Jumlah Client MQTT|IV|MQTT Client Simulator|Mengubah jumlah client yang terhubung ke broker|
|Latency, Throughput, Packet Loss|DV|MQTT Monitoring & Logger|Pencatatan otomatis hasil komunikasi selama pengujian|
|Ukuran Payload|CV|MQTT Publisher Configuration|Menggunakan ukuran payload yang sama pada setiap percobaan|

Apakah semua variabel bisa di-map? [x] Ya / [ ] Tidak

Jika tidak, komponen apa yang perlu ditambahkan? __________________

---

# Latihan 2 — 4 Prinsip Desain

| Prinsip | Status | Bukti / Penjelasan |
|---------|--------|--------------------|
|Traceability|✅|Jumlah client dikontrol melalui simulator dan hasil diukur menggunakan logger MQTT.|
|Modularity|✅|Simulator client, broker, dan logger dipisahkan sehingga mudah dimodifikasi.|
|Controllability|✅|Ukuran payload dan QoS dikunci agar setiap pengujian menggunakan konfigurasi yang sama.|
|Measurability|✅|Logger MQTT secara otomatis menghasilkan data latency, throughput, dan packet loss.|

**Prinsip mana yang paling sulit dipenuhi?**

Controllability

**Strategi untuk mengatasinya:**

Menggunakan konfigurasi jaringan yang sama pada setiap pengujian, mengunci ukuran payload, QoS, dan parameter broker agar hasil eksperimen tetap konsisten.

---

# Latihan 3 — Ablation Study Planning

| Kondisi | Komponen A | Komponen B | Komponen C | Hasil yang Diharapkan |
|---------|------------|------------|------------|-----------------------|
|Full|✅ QoS 1|✅ Payload Tetap|✅ Logger Aktif|Performa komunikasi dapat diukur secara lengkap|
|– A|❌ QoS 0|✅|✅|Latency lebih rendah tetapi keandalan pengiriman pesan menurun|
|– B|✅|❌ Payload Berbeda|✅|Throughput berubah dan hasil kurang konsisten|
|– C|✅|✅|❌ Logger Nonaktif|Performa tidak dapat dianalisis secara lengkap|

Komponen mana yang diprediksi paling berkontribusi?

Komponen A (QoS)

Mengapa?

Karena Quality of Service (QoS) secara langsung memengaruhi mekanisme pengiriman pesan pada MQTT sehingga berdampak terhadap latency, throughput, dan tingkat keberhasilan pengiriman data.

---

# Refleksi

**Jawaban:**

Risiko jika sistem dibangun seperti produk yang bersifat monolitik adalah sulit mengetahui komponen mana yang benar-benar memengaruhi hasil penelitian. Ketika performa berubah, peneliti tidak dapat memastikan apakah perubahan tersebut disebabkan oleh variabel yang diteliti atau oleh komponen lain dalam sistem. Oleh karena itu, arsitektur modular sangat penting dalam penelitian karena memungkinkan setiap variabel dipisahkan dan dikendalikan secara independen. Dengan cara ini, perubahan pada hasil pengujian dapat dikaitkan secara langsung dengan variabel yang dimanipulasi sehingga eksperimen menjadi lebih valid, mudah direproduksi, dan sesuai dengan tujuan penelitian.
