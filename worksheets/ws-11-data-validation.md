# WS-11: Data Validation & Integrity

> **Bab 11 — Validasi Data & Integritas**

---

## Ringkasan Materi

### Data Trust Model

```
Raw Data → Data Cleaning → Consistency Check → Validation Process → Trusted Data
```

Data mentah belum bisa dipercaya. Harus melewati pipeline validasi sebelum siap untuk analisis statistik.

### Empat Pilar Data Quality

| Pilar | Deskripsi | Contoh Pelanggaran |
|-------|----------|-------------------|
| **Accuracy** | Nilai dalam range masuk akal | Akurasi = 1.5 (di luar [0,1]) |
| **Consistency** | Format seragam di semua run | Run 1: CSV, Run 2: JSON |
| **Completeness** | Tidak ada data hilang dari plan | 97 dari 100 run tercatat |
| **Validity** | Data sesuai desain eksperimen | Parameter baseline tercampur treatment |

### Proses Validasi Progresif

1. **Format validation** — Tipe file, header, kolom
2. **Range validation** — Nilai dalam batas logis
3. **Consistency validation** — Format seragam antar-run
4. **Logic validation** — Data cocok dengan desain eksperimen

Jika gagal di langkah awal → tidak perlu lanjut.

### Anomaly Detection — 3 Jenis

| Jenis | Deskripsi | Deteksi |
|-------|----------|---------|
| **Statistical outlier** | Nilai di luar distribusi normal | IQR: < Q1-1.5×IQR atau > Q3+1.5×IQR |
| **Contextual anomaly** | Normal absolut, abnormal dalam konteks | Run 1-10: ~91%, Run 11-20: ~88% |
| **Pattern anomaly** | Pola sistematis (bukan random) | Performa menurun berurutan |

**Prinsip:** Detect → Investigate → Document → Decide — **JANGAN langsung hapus.**

### Engineering vs Research Validation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Data sesuai spesifikasi bisnis | Data layak untuk analisis statistik |
| Missing data | Impute / set default | Investigasi penyebab → dokumentasi |
| Outlier | Bug → fix | Mungkin temuan → investigasi |
| Dokumentasi | Minimal (log error) | Komprehensif (anomali + keputusan) |

### Jebakan Kognitif

1. "Logging otomatis ≠ data benar" → bisa ada bug di logger
2. "Outlier = hapus" → bisa jadi temuan penting
3. "Dataset kecil tidak perlu validasi" → justru lebih rentan
4. "Mean normal = data benar" → [94, 95, 93, **44**, 94] → mean 84% terlihat wajar

---

## Template A.11 — Data Validation Checklist

```
DATA VALIDATION CHECKLIST

Completeness:
  [x] Semua skenario tercakup
  [x] Jumlah run sesuai rencana
  [x] Tidak ada file output hilang
  Missing: 0 dari 15 data points

Format Consistency:
  [x] Semua file format sama (CSV)
  [x] Header konsisten
  [x] Tipe data konsisten (numerik tetap numerik)

Range & Logic:
  [x] Nilai dalam range masuk akal
  [x] Tidak ada waktu negatif
  [x] Packet Loss berada pada rentang 0–100%
  Anomali ditemukan: Tidak ada

Cross-Validation:
  [x] Run identik → hasil mendekati
  [x] Trend konsisten dengan ekspektasi teori

Keputusan:
  [x] Data siap analisis
  [ ] Perlu cleaning
  [ ] Perlu re-run (skenario: __________)
```

---

## Latihan 1 — Completeness Check

| Skenario | Run Direncanakan | Run Tercatat | Missing | Alasan |
|----------|------------------|--------------|---------|--------|
| 10 MQTT Client | 5 | 5 | 0 | — |
| 50 MQTT Client | 5 | 5 | 0 | — |
| 100 MQTT Client | 5 | 5 | 0 | — |

**Total expected:** 15

**Total actual:** 15

**Missing:** 0

**Keputusan untuk data missing:**

Tidak ada data yang hilang sehingga seluruh data dapat digunakan pada tahap analisis statistik.

---

# Latihan 2 — Anomaly Investigation

Periksa data Anda untuk anomali.

Dataset sampel:

| Run | Latency (ms) |
|-----|--------------|
| 1 | 11.8 |
| 2 | 12.1 |
| 3 | 11.9 |
| 4 | 18.6 |
| 5 | 12.0 |

Deteksi outlier:

**Q1 = 11.9**

**Q3 = 12.1**

**IQR = 0.2**

**Batas bawah (Q1 - 1.5×IQR) = 11.6**

**Batas atas (Q3 + 1.5×IQR) = 12.4**

**Outlier terdeteksi:** Run 4

Investigasi:

| Outlier | Nilai | Kemungkinan Penyebab | Keputusan |
|----------|-------|----------------------|-----------|
| Run 4 | 18.6 ms | Terjadi lonjakan trafik jaringan saat pengujian | Re-run skenario dengan kondisi jaringan yang sama dan dokumentasikan hasil sebelumnya |


---

## Latihan 3 — Validation Report

**1. Completeness:** 100% data terkumpul
**2. Format:** [x] Konsisten / [ ] Ada inkonsistensi: __________
**3. Range check (anomali):** Ditemukan satu nilai latency yang lebih tinggi dari distribusi normal dan telah diinvestigasi.
**4. Logic check:** [x] Parameter sesuai plan / [ ] Ada ketidaksesuaian: __________
**Kesimpulan:** [x] Data siap analisis / [ ] Perlu tindakan: __________

---

# Refleksi
**Apa perbedaan antara "data yang benar" dan "data yang dipercaya"? Mengapa proses validasi formal diperlukan meskipun data dikumpulkan secara otomatis?**

Data yang benar belum tentu dapat dipercaya karena masih mungkin mengandung kesalahan pencatatan, data yang hilang, atau konfigurasi eksperimen yang tidak sesuai rencana. Data yang dipercaya adalah data yang telah melalui proses validasi sehingga akurat, lengkap, konsisten, dan sesuai dengan desain eksperimen. Oleh karena itu, validasi formal tetap diperlukan meskipun pengumpulan data dilakukan secara otomatis, karena kesalahan dapat berasal dari logger, konfigurasi sistem, maupun kondisi lingkungan selama eksperimen berlangsung.
