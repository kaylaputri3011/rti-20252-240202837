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
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Baseline (Standard CF) | 42 | K=20, split=80:20 | Planned | ~2 min | res_baseline_42.csv |
| 2 | Baseline (Standard CF) | 123 | K=20, split=80:20 | Planned | ~2 min | res_baseline_123.csv |
| 3 | Baseline (Standard CF) | 456 | K=20, split=80:20 | Planned | ~2 min | res_baseline_456.csv |
| 4 | Baseline (Standard CF) | 789 | K=20, split=80:20 | Planned | ~2 min | res_baseline_789.csv |
| 5 | Baseline (Standard CF) | 999 | K=20, split=80:20 | Planned | ~2 min | res_baseline_999.csv |
| 6 | Context-Aware CF | 42 | K=20, radius=10km | Planned | ~3 min | res_ca_42.csv |
| 7 | Context-Aware CF | 123 | K=20, radius=10km | Planned | ~3 min | res_ca_123.csv |
| 8 | Context-Aware CF | 456 | K=20, radius=10km | Planned | ~3 min | res_ca_456.csv |
| 9 | Context-Aware CF | 789 | K=20, radius=10km | Planned | ~3 min | res_ca_789.csv |
| 10 | Context-Aware CF | 999 | K=20, radius=10km | Planned | ~3 min | res_ca_999.csv |

Jumlah runs per skenario : 5
Total runs               : 10
DATA LOG (Contoh isian per run nanti saat dieksekusi):
  Run ID    : run-001-baseline
  Timestamp : 2026-06-15T08:00:00
  Skenario  : Baseline (Standard CF)
  Input     : dataset_semarang_real.csv (4.362 baris), K=20
  Output    : MAE: [Akan diisi hasil Python], RMSE: [Akan diisi hasil Python]
  Anomali   : Tidak ada anomali memori.
  Catatan   : Run pertama berjalan lancar, utilisasi RAM laptop stabil.

```

---

## Latihan 1 — Execution Plan
Susun execution plan untuk eksperimen Anda. Tentukan skenario, jumlah run, dan seed sebelum eksekusi.

| Run # | Skenario | Seed | Parameter Kunci | Status |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Baseline (Standard CF) | 42 | K=20, split=80:20 | Planned |
| 2 | Baseline (Standard CF) | 123 | K=20, split=80:20 | Planned |
| 3 | Baseline (Standard CF) | 456 | K=20, split=80:20 | Planned |
| 4 | Baseline (Standard CF) | 789 | K=20, split=80:20 | Planned |
| 5 | Baseline (Standard CF) | 999 | K=20, split=80:20 | Planned |
| 6 | Context-Aware CF | 42 | K=20, radius=10km | Planned |
| 7 | Context-Aware CF | 123 | K=20, radius=10km | Planned |
| 8 | Context-Aware CF | 456 | K=20, radius=10km | Planned |
| 9 | Context-Aware CF | 789 | K=20, radius=10km | Planned |
| 10 | Context-Aware CF | 999 | K=20, radius=10km | Planned |

**Total skenario:** 2 (Baseline & Intervensi)
**Run per skenario:** 5
**Total run keseluruhan:** 10
---
## Latihan 2 — Data Log Terstruktur
Desain format data log untuk eksperimen Anda. Tentukan field apa saja yang akan dicatat.
**Identitas:**

| Field | Contoh |
| :--- | :--- |
| Run ID | *run-001-baseline* |
| Timestamp | *2026-06-15T08:30:00* |
| Skenario | *Context-Aware CF* |

**Konfigurasi:**

| Field | Contoh |
| :--- | :--- |
| Seed | *42* |
| Dataset Size | *4362 rows* |
| K_Neighbors | *20* |
| Max_Radius_KM | *10* |

**Hasil:**

| Metrik | Tipe Data | Range Valid |
| :--- | :--- | :--- |
| MAE (Mean Absolute Error) | float | 0.0 – 5.0 (Makin kecil makin baik) |
| RMSE (Root Mean Sq. Error) | float | 0.0 – 5.0 (Makin kecil makin baik) |
| Execution Time (seconds) | float | > 0.0 |

**Format output:** [x] CSV / [ ] JSON / [ ] Database / [ ] Lainnya: ____
---
## Latihan 3 — Anomaly Protocol
Rencanakan bagaimana menangani anomali. Untuk setiap jenis, tentukan langkah yang diambil.

| Jenis Anomali | Contoh | Tindakan |
| :--- | :--- | :--- |
| Run gagal (crash) | *MemoryError (OOM) saat menghitung similarity matrix dari 4000+ data.* | Dokumentasikan error, hentikan run. Turunkan ukuran *batch* kalkulasi, lalu re-run dan catat perubahan konfigurasi memori. |
| Hasil ekstrem | *Skor RMSE tiba-tiba melonjak di atas 2.0 atau MAE bernilai 0 absolut.* | Cek distribusi data latih/uji pada *seed* tersebut. Verifikasi apakah ada *division by zero* pada pembobotan jarak geospasial. |
| Waktu eksekusi anomali | *Run ke-4 memakan waktu 3x lipat lebih lama dari run pertama.* | Indikasi *thermal throttling* pada CPU laptop. Jeda eksperimen 10 menit untuk *cooling down*, catat waktu anomali, lanjutkan run ke-5. |
| Inkonsistensi dengan run lain | *Seed 789 menghasilkan skor akurasi yang jauh lebih buruk dibanding 4 seed lainnya.* | **Jangan dihapus/dibuang!** Tetap catat di log hasil sebagai bagian dari variabilitas. Hitung *Standard Deviation* pada akhir eksperimen. |

**Prinsip:** Detect → Investigate → Document → Decide

---

## Refleksi

> Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? Bagaimana multiple run mengubah kepercayaan terhadap hasil?

**Pengalaman sebelumnya:**
> Sejujurnya, saya belum pernah mengambil mata kuliah *Machine Learning* dan belum mendiskusikan teknis eksperimen komputasi ini. Namun, pada tugas-tugas pemrograman atau praktikum biasa sebelumnya, saya terbiasa hanya melakukan *single run*—yang penting kode berjalan sekali tanpa *error*, hasilnya langsung saya kumpulkan. Setelah mempelajari materi ini, saya baru menyadari bahwa untuk riset algoritma, *single run* sangat berisiko. Risikonya adalah hasil evaluasi (seperti nilai akurasi) bisa jadi hanya kebetulan semata karena faktor acak, sehingga klaim keberhasilan sistem menjadi tidak valid secara ilmiah.

**Yang akan dilakukan berbeda:**
> Karena ini adalah pengalaman riset algoritma pertama saya, saya akan langsung menerapkan standar *multiple runs* sejak awal. Meskipun belum bertemu dosen, saya akan menjalankan skenario algoritma *Baseline* dan *Context-Aware* masing-masing 5 kali dengan *seed* berbeda sebelum melaporkannya. Dengan menyajikan nilai rata-rata dari beberapa kali percobaan, saya akan merasa jauh lebih percaya diri dan memiliki bukti kuat bahwa sistem rekomendasi yang saya buat benar-benar stabil saat didiskusikan nanti.
