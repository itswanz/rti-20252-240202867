# WS-05: Variabel & Metrik

> **Bab 5 — Metric, Measurement & Data**

---

## Ringkasan Materi

### Measurement Alignment Model

Setiap pengukuran yang valid harus bisa ditelusuri melalui rantai ini tanpa lompatan logis:

```
Problem → Concept → Variable → Metric → Data → Result
```

### Operationalization = Keputusan Desain

Menerjemahkan konsep abstrak menjadi variabel terukur bukan proses mekanis. "Code quality" yang diukur via SonarQube code smells membawa asumsi implisit. Setiap operasionalisasi harus didokumentasikan dan dijustifikasi.

### Empat Tipe Data (NOIR)

| Tipe | Ciri | Contoh | Operasi Valid |
|------|------|--------|---------------|
| **Nominal** | Kategori, tanpa urutan | Jenis algoritma (RF, SVM, CNN) | Modus, chi-square |
| **Ordinal** | Urutan, interval tidak sama | Skala Likert (1-5) | Median, Spearman |
| **Interval** | Jarak bermakna, tanpa nol absolut | Suhu Celsius | Mean, Pearson, t-test |
| **Ratio** | Jarak bermakna + nol absolut | Waktu eksekusi (ms) | Semua operasi |

Tipe data menentukan uji statistik yang valid. Kebanyakan metrik performa TI = ratio; persepsi pengguna = ordinal.

### Kriteria Pemilihan Metrik

- **Representative** — Mewakili konsep yang diteliti
- **Sensitive** — Cukup peka menangkap perbedaan bermakna (hindari ceiling effect)
- **Feasible** — Bisa dikumpulkan dalam batasan waktu dan biaya

### Pre-registration

Metrik harus ditentukan **sebelum** eksperimen. Memilih metrik setelah melihat data = **p-hacking**. Metrik tambahan yang ditemukan kemudian dilaporkan sebagai *exploratory*, bukan *confirmatory*.

### Primary vs Secondary Metric

- **Primary Metric** — Langsung terikat ke hipotesis, menentukan kesimpulan
- **Secondary Metric** — Pendukung, dilaporkan di samping primary; statusnya suplementer

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Pemilihan metrik | Berdasarkan kebiasaan/tool yang ada | Berdasarkan construct validity |
| Anomali | Dihapus untuk laporan bersih | Diinvestigasi — bisa jadi temuan |
| Kapan dipilih | Setelah sistem jadi (monitoring) | Sebelum eksperimen (by design) |

### Istilah Penting

- **Operationalization** — Transformasi konsep abstrak menjadi variabel terukur
- **Construct Validity** — Sejauh mana pengukuran benar-benar mengukur konsep yang dimaksud
- **Measurement Scale** — Klasifikasi data (NOIR) yang menentukan analisis valid
- **Multi-metric Evaluation** — Menggunakan beberapa metrik untuk menangkap konsep kompleks

---

## Template A.5 — Definisi Variabel, Metrik & Justifikasi

```
VARIABLE & METRIC DEFINITION

Research Question:
Bagaimana pengaruh jumlah client terhadap performa protokol MQTT pada jaringan Internet of Things berdasarkan latency, throughput, dan packet loss?

| Variabel | Tipe | Konsep | Metrik | Skala | Satuan | Cara Mengukur | Justifikasi |
|----------|------|--------|--------|-------|--------|---------------|-------------|
|Jumlah Client MQTT|IV|Beban komunikasi|Jumlah client|Ratio|Client|Konfigurasi jumlah client pada broker MQTT|Menentukan tingkat beban komunikasi yang diuji|
|Performa MQTT|DV|Kinerja komunikasi|Latency, Throughput, Packet Loss|Ratio|ms, Mbps, %|Monitoring hasil komunikasi menggunakan broker MQTT|Ketiga metrik mewakili performa komunikasi secara menyeluruh|
|Ukuran Payload|CV|Beban data|Ukuran paket data|Ratio|Byte|Mengatur ukuran payload yang sama pada setiap pengujian|Menjaga konsistensi hasil pengujian|

Alignment Check:
  RQ → Concept → Variable → Metric → Data → Result
  [x] Setiap langkah terdokumentasi
  [x] Tidak ada "lompatan logis"
  [x] Metrik mengukur apa yang dimaksud (construct validity)
```

---

## Latihan 1 — Operationalization Chain

Gunakan RQ dari WS-04. Definisikan variabel dan metriknya.

**RQ:**Pengaruh undervolting terhadap stabilitas 1% Low FPS pada iGPU

| Variabel | Tipe | Konsep Abstrak | Metrik Konkret | Skala (NOIR) | Satuan |
|----------|------|---------------|----------------|-------------|--------|
| Jumlah Client MQTT | *IV* |Beban komunikasi | Jumlah client yang terhubung | Ratio | Client |
|Performa MQTT  | DV |Kinerja komunikasi|Ratio|ms, Mbps, %|
|Ukuran Payload| CV |Konsistensi pengujian |DUkuran paket data|ratio|Byte|

**Apakah ada lompatan logis dalam rantai?** [ ] Ya / [x] Tidak
> Jika ya, di mana? ____________________________________

---

## Latihan 2 — Evaluasi Metrik

Evaluasi metrik DV yang dipilih di Latihan 1 menggunakan 3 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Representative | 5  |Latency, throughput, dan packet loss secara langsung menggambarkan performa komunikasi MQTT.|
| Sensitive |5|Ketiga metrik peka terhadap perubahan jumlah client dan beban komunikasi.|
| Feasible |5|Data dapat dikumpulkan menggunakan broker MQTT dan aplikasi monitoring tanpa memerlukan perangkat khusus. |

**Apakah perlu secondary metric?** [x] Ya / [ ] Tidak
> Delivery Rate (%) dan CPU Usage Broker, untuk mengetahui apakah peningkatan jumlah client memengaruhi tingkat keberhasilan pengiriman pesan serta penggunaan sumber daya broker MQTT.

**Contoh kasus ceiling effect untuk metrik ini:**
> Apabila throughput sudah mencapai kapasitas maksimum jaringan, penambahan jumlah client tidak lagi meningkatkan throughput sehingga metrik tersebut tidak mampu menunjukkan perbedaan performa secara jelas.

---

## Latihan 3 — Data Quality Check

Bayangkan data yang akan dikumpulkan dari eksperimen. Evaluasi 4 dimensi kualitas data.

| Dimensi | Pertanyaan | Jawaban | Strategi Mitigasi |
|---------|-----------|---------|------------------|
| Completeness | Apakah semua data point terkumpul? |Ya, seluruh hasil pengujian dicatat pada setiap variasi jumlah client.| Mengulang pengujian jika terjadi kegagalan pencatatan data.|
| Consistency | Apakah ada kontradiksi internal? | Mungkin terjadi perbedaan hasil antar pengujian.| Melakukan pengujian berulang dengan konfigurasi yang sama.|
| Validity |Apakah benar-benar mengukur yang dimaksud? |Ya, latency, throughput, dan packet loss merupakan indikator utama performa MQTT. | Menggunakan konfigurasi jaringan yang konsisten selama eksperimen.|
| Representativeness | Apakah sampel mewakili populasi? | Ya, variasi jumlah client mewakili kondisi komunikasi pada sistem IoT.|Melakukan beberapa kali pengujian dengan jumlah client yang berbeda.|

---

## Refleksi

> Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?

**Jawaban:**
Memilih metrik setelah melihat data dianggap p-hacking karena peneliti dapat memilih metrik yang menghasilkan nilai paling menguntungkan sehingga kesimpulan penelitian menjadi bias. Sebaliknya, eksplorasi data yang sah dilakukan setelah analisis utama selesai dan bertujuan menemukan pola atau temuan baru tanpa mengubah hipotesis maupun metrik yang telah ditetapkan sebelumnya. Dengan demikian, hasil eksplorasi digunakan sebagai dasar penelitian lanjutan, sedangkan pengujian hipotesis tetap mengacu pada metrik yang telah ditentukan sebelum eksperimen dimulai.
> ___________________________________________________
