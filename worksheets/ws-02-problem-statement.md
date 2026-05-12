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
  Domain   : Hardware & Performance Optimization
  Konteks  : Penggunaan Integrated Graphics (iGPU) pada prosesor Ryzen untuk game kompetitif
System Context
  Input       : Clock speed GPU, Shared Memory (VRAM), dan Voltage
  Process     : Alokasi resource sistem oleh driver grafis saat menjalankan beban kerja real-time.
  Output      : Frame rate (FPS) dan Temperature.
  Outcome     : Pengalaman bermain game yang stabil tanpa stuttering
  Constraints : Batas suhu operasional (thermal limit) dan keterbatasan bandwith memori sistem
  Stakeholders: Gamer dengan budget terbatas (PC tanpa diskrit GPU)

Fenomena → Problem
  Fenomena yang diamati             : iGPU sering mengalami penurunan performa setelah dimainkan selama 1 jam
  Gejala (symptom) yang terukur     : FPS drop dari 100 ke 40 secara tiba-tiba (thermal throttling)
  Masalah yang didiagnosis          : Pengaturan voltase default pabrik terlalu tinggi, menyebabkan panas berlebih pada SoC
  Masalah riset (researchable)      : Sejauh mana teknik undervolting dapat menstabilkan frame time tanpa mengurangi peak performance
  Variabel yang terukur             : Nilai 1% low FPS dan suhu derajat Celcius

Problem Quality Check
  [ ] Clarity — Apakah satu orang membaca akan paham?
  [ ] Measurability — Apakah ada metrik kuantitatif?
  [ ] Relevance — Apakah penting untuk domain?
  [ ] Testability — Apakah bisa gagal?
  [ ] Impact — Apakah ada kontribusi jika terjawab?

Problem Statement (1 paragraf):
  ____________________
```

---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:** Optimasi Performa iGPU Ryzen untuk Gaming
| Tahap | Hasil |
|-------|-------|
| Reality | Banyak mahasiswa IT menggunakan laptop/PC iGPU untuk kuliah sekaligus gaming |
| Observed Issue (Symptom) | Game terasa patah-patah (stuttering) setelah beberapa menit dimainkan |
| Diagnosed Problem (Root Cause) |Suhu mencapai 85°C sehingga sistem menurunkan clock speed secara otomatis |
| Researchable Problem |Perbandingan efektivitas profil undervolting manual vs auto-overclock vendor |
| Measurable Variable |Suhu (°C), Clock Speed (MHz), dan Frame Time (ms) |

**Apakah terjebak solution-first thinking?** [ ] Ya / [x] Tidak
> Jika ya, kembali ke tahap mana? ________________________

---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input | Preset kualitas grafis game dan profil daya sistem |
| Process |Rendering objek 3D oleh Radeon Vega 7|
| Output |Tampilan visual di monitor dan log performa |
| Outcome | Kelancaran bermain (tidak ada input lag)|
| Constraints |Kecepatan RAM (DDR4/DDR5) yang membatasi performa iGPU |
| Stakeholders |Mahasiswa, Gamer Kompetitif, Teknisi PC |

**Komponen mana yang paling relevan dengan masalah riset?** _______________

---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity | 5 | Fokus jelas: mengatasi panas untuk stabilitas FPS|
| Measurability |5 | Suhu dan FPS adalah angka yang pasti|
| Relevance |4 |Sangat relevan bagi pengguna hardware budget |
| Testability | 4| Sangat bisa gagal jika undervolting justru membuat sistem crash|
| Impact |4|Memberikan panduan optimasi bagi pengguna iGPU|

**Skor total:** 23 / 25

**Problem statement versi final (1 paragraf):**
> ___________________________________________________
> ___________________________________________________

---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
> Perbedaan fundamentalnya terletak pada tujuannya. Masalah coding (bug) adalah hambatan teknis yang harus segera diperbaiki agar sistem jalan (fokus pada 'how'). Sedangkan masalah riset adalah celah pengetahuan yang ingin dibuktikan kebenarannya secara sistematis (fokus pada 'why'). Dalam coding kita menghindari error, dalam riset, 'error' atau hasil negatif justru merupakan temuan yang valid selama prosesnya benar.
