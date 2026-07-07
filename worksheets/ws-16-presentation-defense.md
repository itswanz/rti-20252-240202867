# WS-16: Presentation & Defense (UAS)

> **Bab 16 — Presentasi & Pertahanan Ilmiah**

---

## Ringkasan Materi

### Scientific Defense Model

```
Research Work → Presentation → Questioning → Defense → Evaluation → Acceptance
```

### Presentasi ≠ Ringkasan Paper

| Paper | Presentasi |
|-------|-----------|
| Dibaca (self-paced) | Didengar (presenter-paced) |
| Detail lengkap | Ide kunci + highlight |
| Tabel numerik detail | Grafik visual + angka kunci |
| Pembaca bisa re-read | Audiens dengar sekali |

**Prinsip:** Presentasi membutuhkan **reformulasi**, bukan kompresi. Medium berbeda = pendekatan berbeda.

### Claim-Evidence-Reasoning (CER)

Setiap jawaban defense harus memiliki:
1. **Claim** — Pernyataan yang dijawab
2. **Evidence** — Data/fakta pendukung
3. **Reasoning** — Logika yang menghubungkan evidence ke claim

**Contoh:**
| Pertanyaan | Bad Answer | Good Answer (CER) |
|-----------|-----------|-------------------|
| "Kenapa hanya 3 dataset?" | "Tiga sudah cukup" | "3 dataset mewakili variasi: small-clean, medium-clean, medium-noisy [E]. Generalisasi perlu validasi lanjut — listed as limitation [R]" |
| "Hasil DS-3 menurun?" | "Itu outlier" | "Ya, karena distribusi heavy-tail melanggar asumsi Gaussian [E]. Ini menunjukkan boundary condition metode [R]" |
| "Effect size?" | "p=0.003, jadi signifikan" | "Cohen's d=1.2 (large effect) [E] — bukan hanya signifikan tapi substansial [R]" |

### Slide Design — One Slide, One Message

**Optimal 9-Slide Plan (15 menit):**

| # | Slide | Waktu | Pesan |
|---|-------|-------|-------|
| 1 | Title + context | 1 min | Apa ini tentang apa |
| 2 | Problem + motivation | 2 min | Mengapa penting |
| 3 | Gap + RQ | 1.5 min | Apa yang belum terjawab |
| 4 | Method overview | 2 min | Bagaimana dijawab (diagram) |
| 5 | Key result — tabel | 2 min | Temuan utama |
| 6 | Key result — grafik | 2 min | Pola visual |
| 7 | Interpretation + failure | 2 min | Apa artinya |
| 8 | Limitation + future | 1.5 min | Batasan & arah |
| 9 | Conclusion + contribution | 1 min | Closing message |

### Anticipatory Defense

Prediksi pertanyaan berdasarkan kategori:

| Kategori | Contoh Pertanyaan |
|---------|------------------|
| Problem | "Mengapa masalah ini penting?" |
| Gap | "Bagaimana dengan studi X yang sudah menjawab ini?" |
| Method | "Mengapa metode ini, bukan Y?" |
| Results | "Bagaimana menjelaskan anomali di DS-3?" |
| Generalization | "Apakah bisa diterapkan di domain lain?" |

### Tiga Prinsip Jawaban

1. **Direct** — Jawab dulu, elaborasi kemudian
2. **Data-based** — Tunjuk evidence spesifik
3. **Honest** — Akui limitasi jika memang ada

### Jebakan Kognitif

1. "Presentasi = semua yang ada di paper" → terlalu padat
2. "Slide cantik = presentasi bagus" → konten > estetika
3. "Tidak bisa jawab = gagal" → "I don't know, but..." menunjukkan kejujuran
4. "Tidak perlu latihan — saya paham riset saya" → latihan = menemukan celah

---

## Template A.16 — Defense Preparation Sheet

```
DEFENSE PREPARATION

Slide Deck Plan:
  Total slides   : 9 (target: 10-12 konten + title/closing)
  Time per slide : ~2 min
  Total time     : 15 menit

Slide Outline:
| # | Pesan Utama | Visual | Waktu |
|---|-------------|--------|-------|
| 1 | Title       |Judul penelitian dan gambar ilustrasi sistem IoT | 1 menit   |
| 2 | Problem     | Diagram perkembangan Internet of Things| 2min  |
| 3 | Gap + RQ    | Diagram alur penelitian | 2min  |
| 4|Metode Penelitian|  Diagram blok ESP32, Sensor DHT22, WiFi, dan Dashboard     |  2 menit     |
|5| Hasil Pengujian|Tabel hasil pengujian suhu dan kelembapan|2 menit|

Anticipatory Defense Matrix:
| Kategori | Pertanyaan Potensial | Jawaban (CER) |
|----------|---------------------|---------------|
| Problem  |Mengapa memilih IoT untuk monitoring suhu dan kelembapan?|IoT memungkinkan pemantauan secara real-time,Data sensor dapat dikirim melalui WiFi ke dashboard secara langsung,Monitoring menjadi lebih cepat dan efisien dibanding cara manual.|
| Gap      |Mengapa menggunakan ESP32 dan DHT22? |  ESP32 memiliki WiFi bawaan dan DHT22 memiliki akurasi yang baik.ESP32 mudah terhubung ke internet dan DHT22 mampu mengukur suhu serta kelembapan dengan stabil.Kombinasi keduanya sesuai untuk sistem monitoring IoT.|
| Method   | Bagaimana memastikan data sensor akurat? | Pengujian dilakukan berulang pada kondisi yang sama.Hasil pembacaan sensor relatif konsisten pada setiap pengujian.Konsistensi menunjukkan sistem bekerja dengan baik.|
| Results  | Mengapa terjadi sedikit perbedaan hasil pengukuran?    |  Sensor memiliki toleransi pembacaan.Perbedaan masih berada dalam batas spesifikasi sensor DHT22.Perbedaan tersebut masih dapat diterima dalam penelitian. |
| Generalization |Apakah sistem dapat digunakan pada lingkungan lain?|  Ya, dengan sedikit penyesuaian konfigurasi.ESP32 dapat digunakan pada berbagai jaringan WiFi dan lokasi.Sistem memiliki fleksibilitas untuk dikembangkan lebih lanjut. |

Latihan:
  Latihan 1: [tanggal] — [catatan timing & feedback]
  Latihan 2: [tanggal] — [catatan timing & feedback]
  Latihan 3: [tanggal] — [catatan timing & feedback]
```

---

## Latihan 1 — Slide Outline

Rencanakan presentasi 15 menit untuk riset Anda.

| # | Pesan Utama | Visual yang Digunakan | Waktu |
|---|-------------|----------------------|-------|
| 1 | Mengapa menggunakan sensor DHT22 dibanding DHT11? | Karena DHT22 memiliki rentang pengukuran dan tingkat akurasi yang lebih baik dibanding DHT11. | *1 min* |
| 2 | Bagaimana jika koneksi WiFi terputus? | Data tidak dapat dikirim ke dashboard, namun ESP32 tetap dapat membaca data sensor hingga koneksi kembali normal. | *2 min* |
| 3 | Apa pengembangan yang dapat dilakukan pada penelitian ini? | Menambahkan sensor lain seperti MQ-2, BMP280, atau membuat notifikasi otomatis melalui Telegram atau WhatsApp. | *1.5 min* |
| 4 | | | |
| 5 | | | |
| 6 | | | |
| 7 | | | |
| 8 | | | |
| 9 | | | |

**Total waktu estimasi:** ____ menit

---

## Latihan 2 — Anticipatory Defense

Prediksi 5 pertanyaan yang mungkin diajukan penguji, lalu siapkan jawaban CER.

| # | Kategori | Pertanyaan | Claim | Evidence | Reasoning |
|---|----------|-----------|-------|----------|-----------|
| 1 | *Problem* | *Contoh: Mengapa fokus kepuasan, bukan akurasi?* | *Akurasi tinggi tidak menjamin kepuasan* | *Survey: 45/100 satisfaction meski RMSE 0.87* | *Gap antara metrik teknis dan pengalaman pengguna* |
| 2 | *Method* | *Contoh: Mengapa hanya 3 dataset?* | *3 dataset mewakili variasi: small-clean, medium-clean, medium-noisy* | *Tabel karakteristik dataset di Bab Method* | *Generalisasi perlu validasi lanjut — tercatat sebagai limitasi* |
| 3 | | | | | |
| 4 | | | | | |
| 5 | | | | | |

---

## Latihan 3 — Simulasi Q&A

Minta teman/kolega mengajukan 3 pertanyaan tentang riset Anda. Catat pertanyaan dan evaluasi jawaban Anda.

| # | Pertanyaan | Jawaban Saya | Evaluasi |
|---|-----------|-------------|---------|| *1* | *Contoh: "Mengapa tidak membandingkan dengan metode Y?"* | *Contoh: "Karena Y memerlukan dataset labeled yang tidak tersedia. Disebutkan sebagai limitasi di halaman X."* | *[✓] Direct [✓] Data-based [✓] Honest* || 1 | | | [ ] Direct [ ] Data-based [ ] Honest |
| 2 |Bagaimana jika jaringan internet terputus? |Data tidak dapat dikirim ke server hingga koneksi kembali normal. Pengembangan selanjutnya dapat menamba | [✓ ] Direct [✓ ] Data-based [✓ ] Honest |
| 3 | | | [ ] Direct [ ] Data-based [ ] Honest |

**Pertanyaan yang paling sulit dijawab:**
Bagaimana jika sistem digunakan pada lingkungan dengan suhu dan kelembapan yang ekstrem?

**Apa yang perlu disiapkan lebih baik:**
>Menambah referensi penelitian, melakukan pengujian pada lebih banyak kondisi lingkungan, serta menyiapkan data pembanding dari sensor lain.

---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-16 — dari paradigma riset hingga presentasi — bagian mana yang paling mengubah cara Anda berpikir tentang riset? Apa satu hal yang akan selalu Anda terapkan di riset berikutnya?

**Insight terbesar:**
Saya memahami bahwa penelitian bukan hanya membuat sistem yang bekerja, tetapi juga membuktikan hasilnya melalui metode ilmiah, pengujian yang terstruktur, serta analisis yang dapat dipertanggungjawabkan.
**Yang akan selalu diterapkan:**
>Selalu menyusun research question yang jelas, menentukan variabel dan metrik sejak awal, mendokumentasikan seluruh proses penelitian, serta melakukan pengujian secara berulang agar hasil penelitian lebih valid dan mudah direproduksi.
