# WS-15: Scientific Writing

> **Bab 15 — Penulisan Ilmiah**

---

## Ringkasan Materi

### Scientific Argument Flow

```
Problem → Gap → RQ → Method → Result → Analysis → Conclusion → Contribution
```

Paper ilmiah adalah **satu argumen utuh** dari masalah ke kontribusi. Setiap node harus terhubung logis ke node sebelum dan sesudahnya.

### Struktur IMRAD

| Section | Peran | Pertanyaan Kunci |
|---------|-------|-----------------|
| **Introduction** | Motivasi + frame | Why is this needed? |
| **Method** | Deskripsi (reproducible) | How was it done? |
| **Results** | Laporan objektif | What was found? |
| **Discussion** | Interpretasi + refleksi | What does it mean? |
| **Conclusion** | Ringkasan + kontribusi | So what? |

### Logical Flow — "Red Thread"

Setiap paragraf menjawab satu pertanyaan dan memicu pertanyaan berikutnya. Alur logis ini harus terasa di tiga level:
1. **Antar-kalimat** dalam paragraf
2. **Antar-paragraf** dalam section
3. **Antar-section** dalam paper

### Internal Consistency

Setiap elemen yang dijanjikan di Introduction harus hadir di Discussion/Conclusion.

**Consistency Matrix:**
```
           Intro  Method  Result  Discuss  Conclude
RQ1          ✓      ✓       ✓       ✓        ✓
RQ2          ✓      ✓       ✓       ✗ ←      ✓
Metrik-X     ✗      ✗       ✓ ←     ✗        ✗
```
**Masalah:** RQ2 dibahas di semua bagian kecuali Discussion. Metrik-X muncul di Result tapi tidak diperkenalkan di Method.

### Writing Quality Triad

| Kualitas | Deskripsi | Contoh Buruk → Baik |
|----------|----------|---------------------|
| **Clarity** | Dipahami sekali baca | "Performa meningkat" → "Accuracy meningkat dari 85.3% ke 89.7%" |
| **Precision** | Istilah eksak, tanpa ambiguitas | "signifikan" → "signifikan secara statistik (p=0.003, d=1.2)" |
| **Conciseness** | Setiap kata menambah informasi | Hapus kalimat redundan, filler words |

### Urutan Penulisan yang Disarankan

1. **Method & Results** — paling stabil, tulis pertama
2. **Discussion** — interpretasi berdasarkan hasil
3. **Introduction** — frame sesuai temuan aktual
4. **Abstract & Conclusion** — terakhir

### Target Jumlah Kata

| Section | Target |
|---------|--------|
| Introduction | 500–700 |
| Related Work | 700–1000 |
| Method | 800–1200 |
| Results | 500–800 |
| Discussion | 600–900 |
| Conclusion | 200–400 |

### Jebakan Kognitif

1. "Lebih panjang = lebih lengkap" → conciseness lebih berharga
2. "Introduction harus ditulis pertama" → justru ditulis terakhir
3. "Jargon teknis = lebih ilmiah" → clarity lebih penting
4. "Discussion = ringkasan Results" → Discussion = interpretasi + konteks

---

## Template A.15 — Paper Structure Checklist

```
PAPER STRUCTURE CHECKLIST

Title   : Rancang Bangun Sistem Monitoring Suhu dan Kelembapan Berbasis IoT Menggunakan ESP32 dan Sensor DHT22
Target  : [ ] Jurnal  [ ] Konferensi  [x] Laporan

Section Check:
  [ x] Abstract — masalah, metode, hasil utama, kontribusi (max 250 kata)
  [ x] Introduction — konteks → gap → RQ → kontribusi → struktur paper
  [ x] Related Work — concept-centric, gap positioning
  [ x] Method — reproducible: desain, variabel, metrik, setup, prosedur
  [ x] Results — tabel + grafik + observasi (tanpa interpretasi)
  [x ] Discussion — interpretasi, perbandingan, implikasi, limitation
  [ x] Conclusion — jawaban RQ, kontribusi, future work

Consistency Matrix:
  [x ] RQ di Introduction = RQ di Method = RQ di Conclusion
  [x ] Variabel di Method = variabel di Results
  [ x] Klaim di Discussion didukung data di Results
  [ x] Limitasi di Discussion di-address di Conclusion/Future Work

Writing Quality:
  [ x] Clarity — mudah dipahami tanpa re-read
  [x ] Precision — tidak ada istilah ambigu
  [ x] Conciseness — tidak ada kalimat redundan
```

---

## Latihan 1 — Paper Outline

Buat outline paper untuk riset Anda menggunakan struktur IMRAD.

| Section | Konten Utama (2-3 kalimat) | Target Kata |
|---------|---------------------------|------------|
| Abstract | Penelitian ini merancang sistem monitoring suhu dan kelembapan berbasis Internet of Things menggunakan ESP32 dan sensor DHT22. Sistem mampu mengirimkan data secara real-time melalui jaringan internet sehingga kondisi lingkungan dapat dipantau dengan mudah. Hasil pengujian menunjukkan sistem bekerja dengan baik dan memiliki tingkat kestabilan yang tinggi. | 200-250 |
| Introduction | Internet of Things memungkinkan perangkat saling terhubung melalui internet untuk melakukan monitoring secara otomatis. Salah satu penerapannya adalah monitoring suhu dan kelembapan ruangan. Penelitian ini bertujuan merancang sistem monitoring berbasis ESP32 dan sensor DHT22 yang mampu mengirimkan data secara real-time serta mengevaluasi performa sistem tersebut. | 500-700 |
| Related Work | | 700-1000 |
| Method | | 800-1200 |
| Results | | 500-800 |
| Discussion | | 600-900 |
| Conclusion | | 200-400 |

---

## Latihan 2 — Consistency Matrix

Buat consistency matrix untuk memverifikasi internal consistency paper Anda.

|  | Intro | Method | Result | Discussion | Conclusion |
|--|-------|--------|--------|-----------|-----------|
| *Contoh: RQ1* | *✓* | *✓* | *✓* | *✓* | *✓* |
| *Contoh: Metrik-X* | *✗ ←* | *✗ ←* | *✓* | *✗ ←* | *✗ ←* |
| RQ1 |✓ | ✓| ✓|✓|✓ |
| RQ2 |✓  |✓ |✓ |✓ |✓|
| Metrik utama |✓ |✓ |✓ |✓ |✓ |
| Variabel IV |✓ |✓ |✓ |✓ |✓ |
| Variabel DV | ✓|✓ |✓ |✓ |✓ |
| Klaim/kontribusi | ✓| ✓| ✓|✓ |✓ |

**Isi setiap sel:** ✓ (ada & konsisten), ✗ (missing), ~ (ada tapi inkonsisten)

**Inkonsistensi yang ditemukan:**
> Tidak ditemukan inkonsistensi. Semua bagian menggunakan istilah, variabel, dan tujuan penelitian yang sama.

**Tindakan perbaikan:**
> Menjaga konsistensi istilah, nama variabel, dan metrik pada seluruh bagian laporan sehingga tidak terjadi perubahan makna.

---

## Latihan 3 — Writing Quality Check

Ambil satu paragraf dari tulisan Anda (atau tulis paragraf baru) dan evaluasi kualitasnya.

**Paragraf asli:**
Sistem monitoring berbasis IoT dibuat menggunakan ESP32 dan sensor DHT22. Sistem ini dapat membaca suhu dan kelembapan kemudian mengirimkan data ke internet sehingga pengguna dapat melihat kondisi lingkungan secara real-time.

| Kriteria | Evaluasi | Perbaikan |
|----------|---------|-----------|
| Clarity | Kalimat sudah mudah dipahami, namun dapat dibuat lebih spesifik. | Menambahkan informasi mengenai fungsi sistem secara lebih jelas. |
| Precision |Istilah "internet" diperjelas menjadi platform monitoring IoT.| Menggunakan istilah teknis yang lebih tepat.|
| Conciseness |Tidak terdapat kalimat yang berulang sehingga paragraf sudah cukup ringkas. |Sistem monitoring berbasis Internet of Things menggunakan ESP32 dan sensor DHT22 dirancang untuk mengukur suhu dan kelembapan ruangan secara real-time. Data hasil pembacaan sensor dikirim melalui jaringan WiFi menuju platform monitoring sehingga pengguna dapat memantau kondisi lingkungan secara cepat dan akurat.|

**Paragraf setelah perbaikan:**
> (tulis paragraf yang sudah diperbaiki)

---

## Refleksi

> Apa perbedaan antara menulis "tentang" riset dan menulis sebagai "argumen" riset? Bagaimana urutan penulisan (Method → Discussion → Introduction) mengubah kualitas tulisan?

> Menulis tentang riset hanya menjelaskan apa yang dilakukan selama penelitian, sedangkan menulis sebagai argumen riset bertujuan meyakinkan pembaca bahwa metode yang digunakan mampu menjawab research question berdasarkan bukti yang diperoleh. Menulis dimulai dari Method, kemudian Results dan Discussion, lalu Introduction membuat isi pendahuluan menjadi lebih sesuai dengan hasil penelitian sehingga alur penulisan menjadi lebih logis, konsisten, dan mudah dipahami.
