# WS-01: Distorsi & Paradigma

> **Bab 1 — Research Mindset in IT**

---

## Ringkasan Materi

### Research Trust Model

Pengetahuan ilmiah tidak muncul langsung dari kenyataan. Ia melewati **6 tahap transformasi** yang masing-masing rawan distorsi:

```
Reality → Data → Processing → Analysis → Inference → Knowledge
```

Etika mencegah distorsi yang disengaja (fabrikasi, cherry-picking). Validitas mendeteksi distorsi yang tidak disengaja (confounding variable, sampling bias).

### Tiga Jenis Validitas

| Jenis | Pertanyaan | Contoh Ancaman |
|-------|-----------|----------------|
| **Internal Validity** | Apakah hubungan kausal benar ada? | Confounding variable |
| **External Validity** | Apakah bisa digeneralisasi? | Dataset terlalu homogen |
| **Construct Validity** | Apakah mengukur hal yang benar? | Metrik tidak sesuai klaim |

### Paradigma Riset

Mata kuliah ini menggunakan pendekatan **Positivist** (fenomena TI bisa diukur objektif melalui eksperimen terkontrol) diperkuat **Design Science Research** (DSR). Penting untuk membedakan keduanya:

| Paradigma | Cara Kerja | Contoh di TI |
|-----------|-----------|---------------|
| **Positivis** | Uji hipotesis dengan eksperimen terkontrol | Apakah CNN lebih akurat dari RF pada dataset X? |
| **Design Science Research** | Bangun artefak (sistem/model/framework) untuk menguji proposisi | Dapatkah arsitektur hybrid CNN+LSTM membuktikan peningkatan recall ≥5%? |
| **Interpretivis** | Pahami makna melalui konteks & kualitatif | Bagaimana peneliti manafsirkan anomali data sensor IoT? |

Dalam DSR, artefak **bukan tujuan akhir** — ia adalah instrumen untuk menghasilkan pengetahuan. Pertanyaan riset tetap harus difalsifikasi.

### Mode Berpikir Peneliti

**Curious** (mempertanyakan fenomena) → **Critical** (mengevaluasi klaim berdasarkan bukti) → **Systematic** (merancang investigasi terstruktur dan reproducible).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Membuat sistem yang bekerja | Menghasilkan pengetahuan yang valid |
| Pertanyaan khas | "Bagaimana membuatnya jalan?" | "Apakah klaim ini benar?" |
| Ukuran sukses | Sistem berfungsi, client puas | Hipotesis terjawab, temuan tervalidasi |
| Kegagalan | Harus dihindari | Harus dilaporkan (negative result = kontribusi) |

### Istilah Penting

- **Research Mindset** — Pola pikir yang menuntut bukti dan mempertanyakan asumsi
- **Research Ethics** — Prinsip perilaku: kejujuran, objektivitas, keterbukaan, akuntabilitas
- **HARKing** — Hypothesizing After Results are Known — merumuskan hipotesis setelah melihat data
- **Falsifiability** — Hipotesis harus bisa dibuktikan salah

---

## Template A.1 — Research Mindset Self-Assessment

```
Nama Peneliti    : irwandi isnugroho
Tanggal          : 23 April 2026

1. Ketika membaca klaim "metode X 95% akurat":
   - Pertanyaan pertama saya: Apakah angka akurasi ini didapat dari pengujian pada kondisi ideal di laboratorium atau sudah mencangkup variabel gangguan(noise) di dunia nyata
   - Data yang dibutuhkan untuk verifikasi:Confusion matrix untuk melihat detail false Positives, perbandingan spesifikasi hardware yang di gunakan,dan distribusi keragaman datashet yang di uji

2. Posisi paradigma:
   - Pendekatan: [ ] Positivis  [ ] Interpretivis  [x] Design Science  [ ] Mixed
   - Alasan: ____________________

3. Identifikasi distorsi:
   - Asumsi tersembunyi: menganggap bahwa perangkat keras (sensor/komponen)akan selalu bekerja konsisten tanpa degradasi performa atau pengaruh suhu lingkungan
   - Sumber bias potensial: samplng bias yaitu hanya mengambil data pada saat sistem berjalan stabil dan mengabaikan data saat sistem mengalami spike atau gangguan koneksi 
   - Langkah mitigasi:melakukan pengujian berulang (reproduclibity) pada waktu yang berbeda dan menggunaka teknik kali brasi sensor yang ketat sebelum pegambilan data 

4. Komitmen etika:
   - Data yang tidak akan dimanipulasi: log mentah (raw data) hasil dari pengujian sensor dan anggka kegagalan sistem (seperti eror rate atau latency) meskipun hasilnya tidak mendukung hipotesis awal 
   - Batasan yang diakui sejak awal: keterbatasan pada kepekaan sensor yang digunakan dan variasi teganggan listrik yang mubgkin mempengaruhi konsistensi pembacaan dan mikrokontroler 
```

---

## Latihan 1 — Identifikasi Distorsi

Pilih satu paper riset di bidang TI yang mengklaim "metode X meningkatkan performa." Telusuri setiap tahap Research Trust Model.

> **Panduan pencarian paper:** Gunakan [IEEE Xplore](https://ieeexplore.ieee.org), [ACM Digital Library](https://dl.acm.org), atau Google Scholar. Pilih paper **tahun 2020 ke atas**, di topik yang Anda minati: deteksi anomali, klasifikasi citra, NLP, keamanan siber, IoT, dsb.
>
> **Contoh domain TI:** "Deteksi anomali lalu-lintas jaringan menggunakan CNN — akurasi meningkat 94% vs baseline SVM 87%." Distorsi potensial: apakah dataset normal/anomali seimbang? Apakah hanya diuji pada satu vendor traffic?

**Paper yang dipilih:**
> Judul: Deep Learning-based Methods for Recognition of Electronic Components on Printed Circuit Boards
> Penulis (Tahun): Khan dkk(2021)
> Sumber/Link DOI: [[_____________________________________](https://doi.org/10.3390/electronics10192383)]

| Tahap | Apa yang Dilakukan | Potensi Distorsi |
|-------|-------------------|-----------------|
| Reality → Data | Mengambil dataset gambar komponen elektronik (Kapasitor, Resistor, IC) dari berbagai papan sirkuit (PCB) | Gambar diambil dengan pencahayaan studio yang sempurna, bukan kondisi bengkel atau lapangan yang berdebu/gelap |
| Data → Processing | Melakukan Augmentasi Data (memutar dan mengubah kontras gambar) untuk memperbanyak jumlah dataset|Augmentasi yang berlebihan bisa menciptakan data "palsu" yang tidak pernah terjadi di dunia nyata, bikin model terlihat lebih pintar dari aslinya |
| Processing → Analysis |Menggunakan algoritma YOLOv4 untuk mendeteksi komponen dan menghitung mAP (mean Average Precision) | Menghitung performa hanya berdasarkan kotak deteksi, bukan apakah komponen itu berfungsi atau rusak (hanya bentuk fisik)|
| Analysis → Inference |Menyimpulkan metode ini sangat efektif untuk otomatisasi industri perakitan elektronik. |Inference ini mengasumsikan semua PCB memiliki tata letak yang rapi, padahal PCB kustom atau lama seringkali berantakan |
| Inference → Knowledge |Menyarankan penggunaan model ini untuk robot pemilah limbah elektronik|Tidak mempertimbangkan variasi bentuk komponen dari manufaktur yang berbeda (beda merk, beda bentuk dikit, model bisa bingung) |

**Distorsi paling besar di tahap:** reality -> data

**Dua distorsi spesifik yang teridentifikasi:**
1. Idealized Environment: Data diambil dalam kondisi pencahayaan dan sudut kamera yang sangat konsisten, sehingga sulit diterapkan pada alat handheld (seperti kamera HP) yang sudutnya goyang-goyang
2. Dataset Homogeneity: Meskipun komponennya banyak, biasanya berasal dari batch produksi yang serupa, sehingga kurang variasi "cacat fisik" yang biasanya ditemui pada barang bekas atau rusak

---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

| Perspektif | Analisis |
|------------|---------|
| Kejujuran ilmiah |Melaporkan kedua versi (dengan dan tanpa outliner |
| Transparansi | peneliti harus menjelaskan secara  terbuka mengapa date tersebut dianggap outliner (misal karena glich sensor atau kesalahan input|
| Peer review | memberikan kesempatan bagi penelaah untuk menilai  apakah menghapusan data tersebut secara metodologis dapat di terima atau justru mencederai validaitas riset|

**Keputusan akhir dan justifikasi:**
> keputusan tetap menyertakan outliner dalam laporan utama, atau jika dihapus harus dicantumkan dalam lampiran dengan penjelasan eksplisit

> justifikasi dalam riset TI negative result tetaplah sebuah kontribusi pengetahuan. Menghapus outliner demi menggejar signifikansi bisa menyesatkan peneliti lain yang ingin mereplikasi eksperimen tersebut di masa depan

## Latihan 3 — Posisi Paradigma

**Topik riset:** Rancang Bangun Sistem Monitoring Suhu dan Kelembapan Ruang Server Berbasis Arduino Uno dengan Notifikasi Real-Time

> **Skala 1–5:** 1 = tidak sesuai sama sekali dengan topik ini, 5 = sangat sesuai dan dominan digunakan pada riset bertopik serupa.

| Kriteria | Positivis | Interpretivis | Design Science |
|----------|-----------|---------------|----------------|
| Kesesuaian dengan topik (1–5) | 4 — Karena penelitian ini melibatkan pengujian akurasi sensor secara kuantitatif| 2 — Kurang sesuai karena riset ini tidak fokus pada persepsi atau makna sosial manusia | *Contoh: 5 — 5 — Sangat sesuai karena fokus utamanya adalah membangun alat (artefak) sebagai solusi |
| Jenis data yang dikumpulkan | Angka statistik, selisih error sensor, dan log durasi pengiriman data (latency) | Testimoni atau kepuasan admin server terhadap tampilan antarmuka sistem | Spesifikasi teknis alat, fungsionalitas fitur, dan hasil pengujian prototipe |
| Limitasi paradigma |Terlalu kaku pada angka sehingga mengabaikan kemudahan penggunaan (usability) alat oleh manusia | Hasilnya sangat subjektif dan sulit untuk dijadikan standar teknis hardware yang baku|Fokus pada "apakah alat itu jalan", terkadang kurang mendalami teori dasar di balik fenomena data sensornya |

**Paradigma yang dipilih:** Design Science Research (DSR)_
**Alasan:** Karena penelitian ini bertujuan untuk menghasilkan solusi praktis berupa produk teknologi (sistem monitoring) Dalam dunia TI keberhasilan riset ini ditentukan oleh sejauh mana sistem yang dibangun bisa menjawab masalah dan bekerja sesuai spesifikasi teknis yang direncanakan

---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sebelumnya, saya sering langsung percaya pada klaim performa sebuah perangkat keras hanya dari brosur atau review singkat. Setelah memahami rantai distorsi, saya menyadari bahwa setiap data bisa terlihat bagus jika diambil dalam kondisi yang terlalu ideal. Sekarang, ketika membaca paper atau klaim teknologi, saya akan bertanya: Bagaimana karakteristik datasetnya? Apakah ada variabel lingkungan yang disembunyikan?, dan Apakah hasil ini bisa diulang jika menggunakan hardware yang berbeda?
