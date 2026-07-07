# WS-10: Experiment Execution & Data Collection

> **Bab 10 — Eksekusi Eksperimen & Pengumpulan Data**

---

## Ringkasan Materi

### Experiment Execution Pipeline

```
Design → Execution Plan → Controlled Execution → Data Collection → Data Logging → Dataset for Analysis
```

### Multiple Run = Non-Negotiable

Single run **tidak pernah cukup** untuk klaim ilmiah. Minimum 5-10 run per skenario dengan seed berbeda. Multiple run menghasilkan:
- Mean, std, confidence interval
- Distribusi hasil → uji statistik
- Variabilitas → error bar di grafik

### Execution Plan

Setiap eksperimen harus memiliki plan sebelum eksekusi:
- Daftar skenario
- Jumlah run per skenario
- Random seed per run (pre-determined!)
- Urutan eksekusi (randomisasi/counterbalancing)
- Pre-execution checklist

### Data Logging Komprehensif

Setiap run menghasilkan log terstruktur:
1. **Identitas** — Run ID, timestamp, skenario
2. **Konfigurasi** — Semua parameter, seed, code version
3. **Hasil** — Semua metrik, output detail
4. **Metadata** — Waktu eksekusi, resource usage, warning/error

Format: CSV/JSON/database — **bukan stdout yang di-copy-paste**.

### Engineering vs Research Execution

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Run | Sekali (deploy) | Multiple (min 5-10, seed berbeda) |
| Logging | Error log, access log | Semua parameter, metrik, metadata |
| Anomali | Bug → fix → redeploy | Investigasi → dokumentasi → analisis |
| Urutan | Tidak penting | Bisa bias — perlu randomisasi |

### Anomali = Dokumentasi, Bukan Hapus

Run gagal/anomali tidak boleh dihapus tanpa dokumentasi. Bisa jadi:
- **Bug** → fix & re-run (dokumentasikan!)
- **Batas kemampuan metode** → DNF = temuan
- **Data yang bias** jika hanya simpan run "berhasil"

### Jebakan Kognitif

1. "Satu angka cukup" → tanpa distribusi, tidak bisa diuji
2. "Seed tidak penting" → bahkan algoritma deterministik bisa dipengaruhi library stokastik
3. "Run gagal langsung hapus" → kehilangan temuan potensial
4. "Semua run harus hari ini" → thermal throttling, fatigue

---

## Template A.10 — Execution Plan & Data Log

```
EXECUTION PLAN

| Run # | Skenario | Seed | Parameter | Status | Waktu | Output File |
|-------|----------|------|-----------|--------|-------|-------------|
| 1 | 10 Client | 42 | QoS=0, Payload=256B | Planned | - | run01.csv |
| 2 | 10 Client | 123 | QoS=0, Payload=256B | Planned | - | run02.csv |
| 3 | 50 Client | 42 | QoS=0, Payload=256B | Planned | - | run03.csv |
| 4 | 50 Client | 123 | QoS=0, Payload=256B | Planned | - | run04.csv |
| 5 | 100 Client | 42 | QoS=0, Payload=256B | Planned | - | run05.csv |

Jumlah runs per skenario : 5
Total runs               : 15

DATA LOG (per run):

  Run ID    : run-001
  Timestamp : 2026-07-07 10:00 WIB
  Skenario  : 10 MQTT Client
  Input     : QoS=0, Payload=256 Byte
  Output    : Latency, Throughput, Packet Loss
  Anomali   : Tidak ada
  Catatan   : Pengujian berjalan normal
```

---

## Latihan 1 — Execution Plan

Susun execution plan untuk eksperimen Anda. Tentukan skenario, jumlah run, dan seed sebelum eksekusi.

| Run # | Skenario | Seed | Parameter Kunci | Status |
|-------|----------|------|-----------------|--------|
| 1 | 10 MQTT Client | 42 | QoS=0, Payload=256 Byte | Planned |
| 2 | 10 MQTT Client | 123 | QoS=0, Payload=256 Byte | Planned |
| 3 | 50 MQTT Client | 42 | QoS=0, Payload=256 Byte | Planned |
| 4 | 50 MQTT Client | 123 | QoS=0, Payload=256 Byte | Planned |
| 5 | 100 MQTT Client | 42 | QoS=0, Payload=256 Byte | Planned |

**Total skenario:** 3
**Run per skenario:** 5
**Total run keseluruhan:** 15


---

## Latihan 2 — Data Log Terstruktur

Desain format data log untuk eksperimen Anda. Tentukan field apa saja yang akan dicatat.

### Identitas
| Field | Contoh |
|------|---------|
| Run ID | run-001 |
| Timestamp | 2026-07-07T10:00:00 |

### Konfigurasi
| Field | Contoh |
|------|---------|
| Seed | 42 |
| Code Version | commit 8ab123c |
| QoS | 0 |
| Payload | 256 Byte |
| Jumlah Client | 10 |

### Hasil
| Metrik | Tipe Data | Range Valid |
|---------|-----------|-------------|
| Latency | float | ≥ 0 ms |
| Throughput | float | ≥ 0 Mbps |
| Packet Loss | float | 0–100 % |

**Format output:** [x] CSV / [ ] JSON / [ ] Database / [ ] Lainnya: ______


---

## Latihan 3 — Anomaly Protocol

Rencanakan bagaimana menangani anomali.

| Jenis Anomali | Contoh | Tindakan |
|---------------|--------|----------|
| Run gagal (crash) | Broker MQTT berhenti tiba-tiba | Dokumentasikan penyebab, restart broker, lalu ulangi run yang gagal |
| Hasil ekstrem | Latency jauh lebih tinggi dari run lainnya | Periksa kondisi jaringan, ulangi pengujian, dan simpan kedua hasil |
| Waktu eksekusi anomali | Pengujian berlangsung jauh lebih lama | Cek penggunaan CPU, RAM, dan koneksi jaringan sebelum re-run |
| Inkonsistensi dengan run lain | Throughput turun drastis hanya pada satu run | Bandingkan konfigurasi, investigasi log, kemudian putuskan apakah perlu re-run |

**Prinsip:** Detect → Investigate → Document → Decide

---

# Refleksi

**Pengalaman sebelumnya:**

Saya pernah melaporkan hasil pengujian hanya berdasarkan satu kali percobaan. Cara tersebut berisiko karena hasil yang diperoleh bisa dipengaruhi oleh kondisi sesaat, seperti beban jaringan atau proses lain yang berjalan di sistem, sehingga belum tentu mewakili kondisi sebenarnya.

**Yang akan dilakukan berbeda:**

Saya akan menjalankan setiap skenario minimal lima kali dengan seed yang telah ditentukan sebelumnya, kemudian menghitung nilai rata-rata dan standar deviasi. Dengan demikian, hasil eksperimen menjadi lebih konsisten, lebih dapat dipercaya, dan layak digunakan sebagai dasar pengambilan kesimpulan ilmiah.
