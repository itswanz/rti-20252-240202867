# WS-06: System-Experiment Mapping

> **Bab 6 — System Design sebagai Experimental Artifact**

---

## Ringkasan Materi

### Sistem = Instrumen Pengujian, Bukan Produk

Seorang engineer bertanya "apakah sistem bekerja?" — seorang peneliti bertanya "apa yang bisa dibuktikan sistem ini?" Sistem dalam riset adalah **artifact** — objek yang sengaja dibuat untuk menguji klaim spesifik.

### System as Experiment Model

```
RQ → Variable → System Component → Experimental Setup → Output
```

Setiap komponen sistem harus bisa ditelusuri ke variabel riset (top-down), dan setiap pengukuran harus menjawab RQ (bottom-up).

### Mapping Variabel ke Komponen

| Tipe Variabel | Peran di Sistem | Contoh |
|---------------|----------------|--------|
| **IV** (Independent) | Modul yang bisa di-toggle/swap | Algoritma A vs B |
| **DV** (Dependent) | Modul pengukuran | Logger, metrics collector |
| **CV** (Control) | Config yang dikunci | Dataset, parameter tetap |

Jika variabel tidak bisa di-map ke komponen apapun → arsitektur perlu didesain ulang.

### 4 Prinsip Desain Eksperimental

| Prinsip | Pertanyaan Kunci |
|---------|-----------------|
| **Traceability** | Komponen ini melayani variabel yang mana? |
| **Modularity** | Bisakah IV diubah tanpa memengaruhi yang lain? |
| **Controllability** | Apakah CV dieksternalisasi ke config file? |
| **Measurability** | Apakah sistem otomatis menghasilkan data yang dibutuhkan? |

### Variable Isolation melalui Arsitektur

- **Modular architecture** — Pisahkan berdasarkan variabel
- **Configuration-driven** — Ubah config (YAML/JSON), bukan code
- **Feature toggles** — On/off flag untuk ablation study

  Contoh config YAML dengan feature toggles:
  ```yaml
  model:
    type: cnn          # IV: ganti "rf" untuk kondisi baseline
  features:
    use_temporal: true  # toggle komponen temporal
    use_normalization: true  # toggle preprocessing
  experiment:
    seed: 42
    runs: 5
  ```
  Dengan pendekatan ini, berbeda kondisi eksperimen = berbeda satu baris config, **tanpa mengubah kode**.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan sistem | Memenuhi kebutuhan user | Menguji hipotesis, menghasilkan bukti |
| Arsitektur | Optimasi performa & skalabilitas | Optimasi isolasi variabel & reprodusibilitas |
| Konfigurasi | Sering hardcoded | Dieksternalisasi ke config file |
| Fitur tambahan | Menambah nilai user | Menambah noise jika tidak terkait RQ |

### Istilah Penting

- **Artifact** — Objek yang sengaja dibuat untuk memecahkan masalah atau menguji proposisi
- **Traceability** — Kemampuan menelusuri hubungan RQ → variabel → komponen → output
- **Variable Isolation** — Mengubah hanya satu variabel sambil menahan yang lain konstan
- **Ablation Study** — Menguji kontribusi tiap komponen dengan melepasnya satu per satu
- **Configuration-driven Execution** — Semua parameter di config file, bukan hardcoded

---

## Template A.6 — Mapping RQ ke Arsitektur Sistem

```
SYSTEM-EXPERIMENT MAPPING

Research Question: ____________________

Variable → Component Mapping:
| Variabel | Tipe | Komponen Sistem | Cara Manipulasi/Pengukuran |
|----------|------|-----------------|---------------------------|
|Tegangan SoC | IV   |Power Tuning Module (AMD Adrenalin/Afterburner) |Mengubah Voltage Offset (-25mV vs 0mV)|
|Stabilitas Performa| DV   |Metrics Logger (CapFrameX / MSI Afterburner)|Pencatatan otomatis frame time setiap 1ms|
|Beban Kerja Game| CV   |Scenario Controller (Custom Game Profile)|Mengunci setting grafis (Low), Map (Ascent), dan durasi (10 menit) |

4 Prinsip Desain:
  [x] Traceability — Setiap komponen bisa ditelusuri ke variabel
  [x] Variable Isolation — IV bisa diubah tanpa mengubah CV
  [x] Measurement Integration — Pengukuran DV built-in
  [x] Reproducibility — Setup bisa direkonstruksi

Experimental Setup:
  Input data     :Skenario Deathmatch Valorant (Map Ascent
  Parameter      : Driver AMD v24.3.1, RAM 16GB Dual Channel, Ambient Temp 31°C
  Output format  : File CSV berisi log frame time dan suhu
```

---

## Latihan 1 — Variable-to-Component Mapping

Gunakan RQ dan variabel dari WS-05. Petakan ke komponen sistem.

**RQ:** __________________________________________________

| Variabel | Tipe | Komponen Sistem | Cara Manipulasi / Pengukuran |
|----------|------|-----------------|---------------------------|
| Voltase SoC | *IV* | AMD Adrenalin Performance Tab| Ganti profil manual voltage_offset|
|1% Low FPS | DV |CapFrameX Analysis Tool|Kalkulasi otomatis dari distribusi frame time|
|Suhu Kerja| CV |HWInfo64 Monitoring|Pembacaan sensor dioda SoC iGPU|

**Apakah semua variabel bisa di-map?** [x] Ya / [ ] Tidak
> Jika tidak, komponen apa yang perlu ditambahkan? _________

---

## Latihan 2 — 4 Prinsip Desain

Evaluasi desain sistem terhadap 4 prinsip.

| Prinsip | Status | Bukti / Penjelasan |
|---------|--------|-------------------|
| Traceability |  ✅  |Voltase dikontrol lewat Adrenalin, hasil diukur lewat CapFrameX|
| Modularity | ✅|Software tuning terpisah dari software pengukur (logger). |
| Controllability | ✅|Setting game dikunci di file GameUserSettings.ini|
| Measurability | ✅| CapFrameX menyediakan metrik presisi hingga milidetik.|

**Prinsip mana yang paling sulit dipenuhi?**Controllability
**Strategi untuk mengatasinya:**
> Menggunakan mode "Practice" atau "Deathmatch" yang variabel musuhnya lebih acak, namun tetap konsisten dalam durasi dan beban grafis

---

## Latihan 3 — Ablation Study Planning

Jika sistem memiliki 3 komponen utama, rencanakan ablation study.

> **Panduan jumlah kondisi:** Untuk 3 komponen (A, B, C), kondisi minimal yang direkomendasikan:
> Full + (-A) + (-B) + (-C) = **4 kondisi dasar**. Jika waktu memungkinkan, tambahkan kombinasi ganda: (-A,-B), (-A,-C), (-B,-C) = **7 kondisi**. Sesuaikan dengan *computational cost* dan tenggat waktu penelitian.

| Kondisi | Komponen A | Komponen B | Komponen C | Hasil yang Diharapkan |
|---------|-----------|-----------|-----------|----------------------|
| Full | ✅ undervolt| ✅ xmp provile | ✅ Aggressive Curve | Performa paling stabil & dingin |
| – A | ❌ Stock Volt) | ✅ | ✅ |Suhu naik, kemungkinan throttling|
| – B | ✅ | ❌ Stock (2133MHz) | ✅ |FPS rata-rata turun drastis |
| – C | ✅ | ✅ | ❌ Default/Quiet |Suhu naik, kipas lambat |

**Komponen mana yang diprediksi paling berkontribusi?** Komponen B (RAM)
**Mengapa?**
> Karena iGPU sangat bergantung pada memory bandwidth. Namun, Komponen A diprediksi paling berkontribusi pada stabilitas (mengurangi stutter)

---

## Refleksi

> Apa risiko jika sistem dibangun seperti produk (monolitik, fitur lengkap) lalu baru dilakukan eksperimen? Mengapa arsitektur modular penting untuk riset?

**Jawaban:**
Risiko jika sistem dibangun sebagai "produk" monolitik adalah kita tidak bisa mengisolasi penyebab perubahan hasil. Jika sistem tiba-tiba kencang, kita tidak tahu apakah itu karena algoritma A, konfigurasi B, atau sekadar keberuntungan.

Arsitektur modular sangat penting karena memungkinkan peneliti untuk melakukan Variable Isolation. Kita bisa menukar satu komponen (IV) sementara komponen lainnya (CV) tetap diam, sehingga kita yakin bahwa perubahan output (DV) benar-benar disebabkan oleh manipulasi yang kita lakukan, bukan karena noise dari fitur lain
