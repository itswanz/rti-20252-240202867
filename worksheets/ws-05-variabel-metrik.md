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

Research Question:Apakah penerapan profil undervolting -25mV pada SoC iGPU Radeon Vega 7 menghasilkan nilai 1% low FPS yang lebih stabil dibandingkan dengan pengaturan Stock pada game Valorant?

| Variabel | Tipe | Konsep | Metrik | Skala | Satuan | Cara Mengukur | Justifikasi |
|----------|------|--------|--------|-------|--------|---------------|-------------|
|Tegangan SoC| IV   | Konfigurasi Daya |Voltase Profil|Nominal|mV|Software AMD Adrenalin|Membedakan kelompok uji (Stock vs UV)|
|Stabilitas Performa| DV   | Konsistensi Frame|1% Low FPS|Ratio|FPS |CapFrameX / Afterburner|1% Low lebih sensitif terhadap stutter dibanding rata-rata|
|Suhu Lingkungan| CV   |Kondisi Eksternal|Ambient Temp|Interval|°C| Termometer Ruangan |Memastikan pengaruh suhu luar tetap konstan (30°C)|

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
| Profil Tegangan | *IV* |Efisiensi Daya | Voltase (-25mV vs 0) | Nominal | mV |
|Profil Tegangan| DV |Kenyamanan Visual|1% Low FPS|ratio|fps|
|beban kerja| CV |konsistensi uji |Durasi dam Skenario|ratio|detik|

**Apakah ada lompatan logis dalam rantai?** [ ] Ya / [x] Tidak
> Jika ya, di mana? ____________________________________

---

## Latihan 2 — Evaluasi Metrik

Evaluasi metrik DV yang dipilih di Latihan 1 menggunakan 3 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Representative | 5  |Sangat mewakili konsep "mulus" karena menangkap drop FPS terjauh |
| Sensitive |5|Sangat peka; undervolting biasanya langsung berdampak pada frame time |
| Feasible |5|Mudah diambil menggunakan software gratis (CapFrameX |

**Apakah perlu secondary metric?** [x] Ya / [ ] Tidak
> Jika ya, apa dan mengapa?Average FPS dan Max Temperature, untuk memastikan bahwa undervolting tidak menurunkan performa puncak secara drastis sambil tetap menekan panas

**Contoh kasus ceiling effect untuk metrik ini:**
> ___________________________________________________

---

## Latihan 3 — Data Quality Check

Bayangkan data yang akan dikumpulkan dari eksperimen. Evaluasi 4 dimensi kualitas data.

| Dimensi | Pertanyaan | Jawaban | Strategi Mitigasi |
|---------|-----------|---------|------------------|
| Completeness | Apakah semua data point terkumpul? |Ya, log per detik.| Mengulang sesi jika software log crash.|
| Consistency | Apakah ada kontradiksi internal? | Mungkin suhu naik tapi FPS tetap| Cek apakah ada background process Windows Update|
| Validity |Apakah benar-benar mengukur yang dimaksud? |Ya, 1% low = stutter | Kalibrasi software sebelum pengambilan data.|
| Representativeness | Apakah sampel mewakili populasi? | mewakili populasi?	Ya, untuk user iGPU Ryzen|Melakukan pengujian minimal 5 kali repetisi|

---

## Refleksi

> Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?

**Jawaban:**
>Memilih metrik setelah melihat data dianggap p-hacking karena peneliti cenderung memilih metrik yang hanya menunjukkan hasil positif/signifikan saja, sehingga membiaskan kebenaran ilmiah. Bedanya dengan eksplorasi data yang sah adalah: Eksplorasi bertujuan untuk mencari pola baru untuk penelitian di masa depan, sedangkan Confirmatory (metrik yang dipre-registrasi) bertujuan untuk menguji hipotesis yang sudah dibuat secara jujur tanpa memanipulasi parameter keberhasilan
> ___________________________________________________
