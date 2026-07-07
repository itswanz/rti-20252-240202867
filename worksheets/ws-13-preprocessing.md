# WS-13: Data Preprocessing

> **Bab 13 — Preprocessing & Persiapan Data untuk Analisis**

---

## Ringkasan Materi

### Data Refinement Pipeline

```
Raw Data → Cleaning → Transformation → Normalization → Processed Data → Analysis Ready
```

Setiap tahap memiliki tujuan berbeda. **Preprocessing bukan langkah teknis biasa** — setiap keputusan preprocessing adalah keputusan riset yang bisa mengubah kesimpulan.

### Empat Prinsip Preprocessing

| Prinsip | Deskripsi |
|---------|----------|
| **Consistency** | Metode sama untuk data yang sama |
| **Transparency** | Setiap langkah terdokumentasi |
| **Reproducibility** | Orang lain bisa mengulang dengan hasil sama |
| **Minimal Distortion** | Ubah sesedikit mungkin; jika normalisasi tidak perlu, jangan lakukan |

### Cleaning Triad

| Masalah | Strategi | Risiko |
|---------|---------|--------|
| **Missing values** | | |
| — Listwise deletion | Missing < 5%, random | Data loss |
| — Mean/median imputation | Sedikit missing, dist. normal | Mengurangi variabilitas |
| — Model-based imputation | Banyak missing, pola sistematis | Introduces dependency |
| — Flag & separate | Missing karena alasan substantif | Kompleksitas analisis |
| **Duplikat** | Identifikasi → verifikasi → hapus | False positive (data mirip ≠ duplikat) |
| **Error format** | Standardisasi tipe, encoding | Kehilangan informasi saat konversi |

### Normalisasi — Kapan & Metode Mana

| Metode | Formula | Output | Sensitif Outlier? |
|--------|---------|--------|-------------------|
| Min-max | (x-min)/(max-min) | [0, 1] | Ya |
| Z-score | (x-mean)/std | Unbounded | Lebih robust |
| Robust scaling | (x-median)/IQR | Unbounded | Paling robust |

**Kunci:** Parameter normalisasi harus dihitung dari **training set saja** — bukan seluruh data. Pelanggaran = **data leakage**.

### Data Leakage Prevention

Data leakage terjadi ketika informasi dari test set "bocor" ke preprocessing:
- Normalisasi parameter dari seluruh dataset ← **SALAH**
- Cross-validation dilakukan sebelum split ← **SALAH**
- Feature selection menggunakan label test set ← **SALAH**

### Jebakan Kognitif

1. "Preprocessing cuma teknis — tidak perlu detail" → bisa ubah kesimpulan
2. "Lebih banyak preprocessing = lebih bersih = lebih baik" → over-processing distorsi data
3. "Normalisasi selalu diperlukan" → belum tentu, tergantung metode analisis
4. "Imputation sama untuk semua situasi" → strategi harus sesuai konteks

---

## Template A.13 — Preprocessing Documentation Log

```
PREPROCESSING LOG

Dataset           : Data monitoring suhu dan kelembapan berbasis Internet of Things menggunakan ESP32 dan sensor DHT22
Jumlah data awal  : 1000 data

Cleaning:
| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
| Missing |8 data |Listwise deletion|Missing kurang dari 5% sehingga tidak mempengaruhi hasil analisis|
| Duplikat|3 data|Menghapus data duplikat|Menghindari data yang tercatat lebih dari satu kali|
| Error   |5 data|Menghapus data tidak valid|Nilai berada di luar rentang kerja sensor DHT22|

Transformation:
| Transformasi | Variabel | Detail | Alasan |
|-------------|----------|--------|--------|
|Konversi Timestamp| Waktu |Format YYYY-MM-DD HH:MM:SS|Mempermudah analisis berdasarkan waktu|

Normalization:
  Metode    : Tidak dilakukan
  Alasan    : Data digunakan dalam satuan asli hasil pembacaan sensor sehingga lebih mudah diinterpretasikan.
  Parameter : Tidak diterapkan

Leakage Check:
  [x] Parameter normalisasi dari training set saja
  [x] Tidak ada informasi test set dalam preprocessing
  [x] Cross-validation dilakukan setelah split

Jumlah data akhir : ____________________
Script tersedia   : [x] Ya → path: ____ | [ ] Belum
```

---

## Latihan 1 — Cleaning Plan

Periksa dataset Anda (atau dataset contoh) dan dokumentasikan masalah yang ditemukan.

| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
|Missing Value|	8 data|	Listwise deletion	|Missing kurang dari 5%|
Data Duplikat	|3 data|	Menghapus data|	Menghindari pencatatan ganda|
Nilai Tidak Valid|5 data|	Menghapus data|	Nilai di luar spesifikasi sensor DHT22|
| | | | |

**Jumlah data sebelum cleaning:** 1000
**Jumlah data setelah cleaning:** 984
**Persentase data yang hilang/berubah:** 1,6%

---

## Latihan 2 — Normalisasi Decision

Tentukan apakah data Anda perlu normalisasi, dan jika ya, metode apa yang tepat.

| Variabel | Range Asli | Distribusi | Outlier? | Metode Normalisasi | Alasan |
|----------|-----------|-----------|----------|-------------------|--------|
| *Contoh: response_time* | *0.1 – 45.2s* | *Right-skewed* | *Ya (45.2s)* | *Robust scaling* | *Ada outlier, perlu robust* || *Contoh: accuracy_score* | *0.72 – 0.95* | *Normal, narrow* | *Tidak* | *Tidak perlu* | *Sudah dalam [0,1], metode berbasis distance tidak digunakan* || | | | | | |
| | | | | | |

**Apakah normalisasi diperlukan?** [ ] Ya / [ ] Tidak
**Justifikasi:**
> ___________________________________________________

**Leakage check:**
- [ ] Parameter dihitung dari training set saja
- [ ] Normalisasi diterapkan setelah train-test split

---

## Latihan 3 — Preprocessing Report

Buat ringkasan preprocessing lengkap — dokumentasi yang cukup bagi orang lain untuk mereplikasi.

```
PREPROCESSING SUMMARY

1. Dataset: ____________________
2. Data awal: ____ records, ____ features
3. Cleaning:
   - Missing values: ____ kasus, metode: ____
   - Duplikat: ____ kasus, tindakan: ____
   - Error: ____ kasus, tindakan: ____
4. Transformation: ____________________
5. Normalisasi: ____ (metode), parameter dari ____
6. Data akhir: ____ records, ____ features
7. Leakage check: [ ] Lulus / [ ] Ada masalah
```

---

## Refleksi

> Apakah Anda pernah melakukan normalisasi "karena biasa dilakukan" tanpa mempertimbangkan apakah benar-benar diperlukan? Apa risiko over-preprocessing?

> ___________________________________________________
> ___________________________________________________
