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

Research Question :"Apakah penerapan profil undervolting -25mV pada SoC iGPU Radeon Vega 7 menghasilkan nilai 1% low FPS yang lebih stabil dibandingkan dengan pengaturan Stock pada game Valorant?
Hypothesis        :Profil undervolting menghasilkan peningkatan nilai 1% low FPS $\ge$ 10% dibanding pengaturan stock
Tipe Eksperimen   : [x] Comparison  [ ] Ablation  [ ] Parameter

Kondisi Eksperimen:
| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control | Pengaturan pabrik (Default) |Stock Voltage (0mV offset)| Low Settings, Ascent Map, 31°C Ambient|
| Treatment |Pengaturan Optimasi|Undervolt (-25mV offset) |Low Settings, Ascent Map, 31°C Ambient|

Fairness Checklist:
  [x] Dataset identik untuk semua kondisi
  [x] Preprocessing setara
  [x] Tuning effort setara
  [x] Environment identik
  [x] Metrik evaluasi sama

Threat Analysis:
| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal    |Background process Windows (Update/Antivirus) tiba-tiba aktif.|Mematikan koneksi internet dan layanan non-esensial sebelum pengujian|
| External    |Hasil hanya berlaku untuk Radeon Vega 7, mungkin berbeda di iGPU Intel. | Mengakui batasan riset (scope) hanya pada arsitektur Zen 3 APU.|
| Construct   |Metrik Average FPS tidak menangkap micro-stuttering|Menggunakan 1% Low FPS dan Frame Time graph sebagai metrik utama.|
| Conclusion  |Variasi tiap sesi game (jumlah musuh berbeda)|Melakukan repetisi 5 kali dan mengambil nilai rata-rata (Mean)|

Statistical Plan:
  Uji statistik   : Independent Samples T-Test.
  Justifikasi      :Membandingkan rata-rata dari dua kelompok independen (Stock vs UV)
  Alpha            :0.05 (Tingkat kepercayaan 95%).
  Effect size min  :Cohen's d > 0.5$.
```

---

## Latihan 1 — Desain Eksperimen

Susun desain eksperimen berdasarkan RQ, variabel, dan sistem dari WS-04 sampai WS-06.

**RQ:** __________________________________________________
**Tipe eksperimen:** [ ] Comparison / [ ] Ablation / [ ] Parameter

| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control | Profil daya seimbang (Balanced) | Stock Voltage |RAM 3200MHz, Driver 24.3.1 |
| Treatment |Profil daya optimasi|Undervolt -25mV|RAM 3200MHz, Driver 24.3.1 |

---

## Latihan 2 — Fairness Checklist

Evaluasi apakah desain eksperimen di Latihan 1 sudah fair.

| Kriteria | Status | Detail |
|----------|--------|--------|
| Dataset identik | *Contoh: ✅ | Skenario game yang dimainkan identik (Map Ascent).|
| Preprocessing setara | ✅ |Tidak ada perubahan setting game di tengah jalan |
| Tuning effort setara |✅  | Keduanya diuji dalam kondisi baterai penuh (AC plugged in)|
| Environment identik |✅  |Lokasi pengujian sama, jam pengujian sama (mencegah fluktuasi suhu) |
| Metrik evaluasi sama |✅  | Keduanya menggunakan output CapFrameX yang sama|

**Ada yang tidak fair?** [ ] Ya / [x] Tidak
> Jika ya, bagaimana cara memperbaikinya? ________________

---

## Latihan 3 — Threat Analysis

Identifikasi ancaman validitas untuk desain eksperimen ini.

| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal | Fluktuasi suhu ruangan (Kebumen siang hari panas). | Pengujian dilakukan berurutan secara cepat dan dipantau termometer.|
| External |Game update (patch baru) mengubah performa.|Melakukan seluruh sesi eksperimen dalam satu hari yang sama |
| Construct |Sensor software tidak akurat dibanding hardware. |Menggunakan polling rate sensor tertinggi (20ms) |
| Conclusion |Sample size kecil (hanya 5 kali lari).|Menghitung standar deviasi untuk melihat konsistensi data|

**Ancaman mana yang paling sulit dimitigasi?** External (Game Updates)
**Mengapa?**
>Game kompetitif seperti Valorant sering melakukan update kecil yang bisa mengubah cara CPU/GPU menangani render. Jika ada update di tengah eksperimen, data sebelumnya bisa tidak valid

---

## Refleksi

> Sebuah paper melaporkan "metode kami mengalahkan semua baseline." Apa 3 pertanyaan pertama yang harus diajukan untuk mengevaluasi klaim ini?

**Jawaban:**
1.Apakah baselinenya sudah diatur dengan konfigurasi optimal (best-effort) atau hanya menggunakan pengaturan default yang lemah?" (Fairness Check)_
2. Apakah environment pengujian (hardware, software version, dataset) identik untuk semua metode?" (Internal Validity)
3. Bagaimana signifikansi statistiknya? Apakah peningkatannya nyata atau hanya fluktuasi margin of error?" (Conclusion Validity)
