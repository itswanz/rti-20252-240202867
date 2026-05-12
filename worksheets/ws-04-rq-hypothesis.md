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

Gap Statement  : Kurangnya studi mengenai efektivitas kombinasi undervolting manual dan memory profile terhadap kestabilan frame time (1% low FPS) pada iGPU Radeon Vega 7 dalam kondisi suhu lingkungan tinggi (>30°C

Research Question:
  Tipe         : [ ] Comparison  [x] Improvement  [ ] Exploratory
  Formulasi    :Apakah penerapan profil undervolting -25mV pada SoC iGPU Radeon Vega 7 menghasilkan nilai 1% low FPS yang lebih stabil (standar deviasi lebih rendah) dibandingkan dengan pengaturan Auto-Clock pada game Valorant di lingkungan suhu >30°C?
  Variabel IV  : Profil tegangan iGPU (Stock vs Undervolt -25mV)
  Variabel DV  : Stabilitas frame time dan suhu kerja
  Metrik       : 1% Low FPS (FPS) dan Standard Deviation dari Frame Time (ms)
  Dataset      : Game Valorant (Map Ascent, durasi 10 menit Deathmatch
  Baseline     : Pengaturan Default pabrik (Stock)

Quality Check RQ:
  [ ] Variabel spesifik
  [ ] Metrik jelas
  [x] Baseline ada
  [ ] Konteks disebutkan
  [ ] Memerlukan eksperimen (bukan hanya survei literatur)

Contribution Statement:
  Apa yang baru diketahui : Pengaruh presisi dari penurunan voltase terhadap konsistensi performa iGPU pada suhu tropis
  Jenis kontribusi        : [x] Improvement  [ ] Comparison  [ ] Novel approach
  Gap yang diisi          : Mengatasi performance gap (stuttering) akibat panas berlebih pada hardware entry-leve
Hypothesis Pair:
  H₀ : Tidak ada perbedaan signifikan pada nilai 1% low FPS antara profil undervolting dan pengaturan stock
  H₁ : Profil undervolting menghasilkan peningkatan nilai 1% low FPS minimal sebesar 10% dibanding pengaturan stock
  Threshold              :  Peningkatan 10% pada metrik 1% low FPS
  Justifikasi threshold  : Angka 10% adalah batas minimal perbedaan yang dapat dirasakan secara visual (perceptible) oleh pemain game kompetitif
```

---

## Latihan 1 — Dari Gap ke RQ

Gunakan gap yang ditemukan di WS-03. Transformasikan menjadi Research Question.

**Gap dari WS-03:** Kurangnya data pengujian stabilitas frame time pada iGPU Ryzen di suhu ruangan non-AC

**RQ versi pertama (tulis bebas):**
>Bagaimana pengaruh modifikasi kurva voltase terhadap konsistensi frame time iGPU Radeon Vega 7 saat menjalankan beban kerja game kompetitif di suhu lingkungan 30-33°C?

**Evaluasi RQ:**

| Komponen | Ada? | Isi |
|----------|------|-----|
| Metode spesifik | Tidak ada perbedaan signifikan pada nilai 1% low FPS antara profil undervolting dan pengaturan stock|
| Metrik terukur | Profil undervolting menghasilkan peningkatan nilai 1% low FPS minimal sebesar 10% dibanding pengaturan stock |
| Baseline | |Peningkatan  10% pada metrik 1% low FPS |
| Dataset/konteks | |Angka 10% adalah batas minimal perbedaan yang dapat dirasakan secara visual (perceptible) oleh pemain game kompetitif |

**Tipe RQ:** [ ] Comparison / [ ] Improvement / [ ] Exploratory

**RQ versi revisi (setelah evaluasi):**
> ___________________________________________________

---

## Latihan 2 — Hypothesis Pair

Rumuskan pasangan hipotesis dari RQ di Latihan 1.

| Komponen | Isi |
|----------|-----|
| H₀ | Modifikasi voltase tidak menurunkan frekuensi stuttering (frame time spike) |
| H₁ |Modifikasi voltase menurunkan frekuensi frame time spike secara signifikan |
| Metrik |Frame time variance (ms)|
| Threshold |Penurunan varians  15% |


**Apakah hipotesis ini falsifiable?** [x] Ya / [ ] Tidak
> Bagaimana cara membuktikannya salah? ___________________

---

## Latihan 3 — Rantai Operasionalisasi

Lengkapi rantai dari RQ hingga metode analisis.

| Tahap | Isi |
|-------|-----|
| RQ |Apakah undervolting meningkatkan stabilitas 1% low FPS? |
| Variable (IV) | Tegangan SoC iGPU (Volt |
| Variable (DV) |1% Low FPS |
| Metric |Frames per second (FPS) |
| Data source |Log dari software MSI Afterburner / CapFrameX |
| Analysis method |Comparative Analysis (T-test) antara data Stock vs Undervolt |

**Apakah rantai lengkap?** [ ] Ya / [ ] Tidak
> Jika tidak, tahap mana yang perlu direvisi? ______________

---

## Refleksi

> Ambil satu judul skripsi/paper yang pernah dibaca. Coba ekstrak RQ-nya. Apakah RQ tersebut memenuhi semua komponen (metode, metrik, baseline, konteks)? Jika tidak, apa yang hilang?

**Judul:** Performance Optimization of Integrated Graphics in Competitive Gaming
**RQ yang diekstrak:**Dapatkan overclocking RAM meningkatkan FPS?
**Komponen yang hilang:**Tidak menyebutkan Metode overclocking secara spesifik (XMP atau Manual), tidak menyebutkan Dataset/Game yang digunakan, dan tidak menyebutkan Baseline pembandingnya_
