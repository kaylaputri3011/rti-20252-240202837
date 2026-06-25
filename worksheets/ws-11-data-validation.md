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
  Missing: 0 dari 10 data points

Format Consistency:
  [x] Semua file format sama (CSV)
  [x] Header konsisten
  [x] Tipe data konsisten (numerik tetap numerik)

Range & Logic:
  [x] Nilai dalam range masuk akal (Metrik Error MAE/RMSE harus positif dan masuk akal)
  [x] Tidak ada waktu negatif pada durasi eksekusi
  [x] Metrik tidak di luar range skala 1-5
  Anomali ditemukan: Ada 1 simulasi anomali pada Run 4 (Skor Error terlalu kecil secara tidak wajar).

Cross-Validation:
  [x] Run identik → hasil mendekati
  [x] Trend konsisten dengan ekspektasi teori

Keputusan:
  [x] Data siap analisis
  [ ] Perlu cleaning
  [ ] Perlu re-run (skenario: ____)

```

---

## Latihan 1 — Completeness Check

Verifikasi apakah semua data yang direncanakan sudah terkumpul.

| Skenario                      | Run Direncanakan | Run Tercatat | Missing | Alasan |
|-------------------------------|------------------|--------------|---------|--------|
| Baseline (Standard CF)        | 5                | 5            | 0       | Eksekusi berjalan lancar tanpa OOM |
| Intervensi (Context-Aware CF) | 5                | 5            | 0       | Eksekusi berjalan lancar tanpa OOM |

**Total expected:** 10 | **Total actual:** 10 | **Missing:** 0

**Keputusan untuk data missing:**
> Karena tidak ada data yang *missing* (0), proses dapat langsung dilanjutkan ke tahap deteksi anomali pada skor metrik hasil eksperimen.

---

## Latihan 2 — Anomaly Investigation

Periksa data Anda untuk anomali. Gunakan metode IQR atau z-score.

**Dataset sampel (Simulasi Skor MAE dari 5 Run Baseline):**

| Run | MAE Score |
|-----|-----------|
| 1   | 0.85      |
| 2   | 0.87      |
| 3   | 0.86      |
| 4   | **0.21** |
| 5   | 0.88      |

**Deteksi outlier:**
- Q1 = 0.85 | Q3 = 0.87 | IQR = 0.02
- Batas bawah (Q1 - 1.5×IQR) = 0.82
- Batas atas (Q3 + 1.5×IQR) = 0.90
- Outlier terdeteksi: **Run 4 (0.21)**

**Investigasi (untuk setiap outlier):**

| Outlier | Nilai | Kemungkinan Penyebab                                                                                             | Keputusan                                                                                                                                   |
|---------|-------|------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| Run 4   | 0.21  | Skor *error* (MAE) tiba-tiba sangat kecil secara tidak wajar. Kemungkinan terjadi *data leakage* (data uji ikut masuk ke data latih). | Telusuri indeks *train_test_split* pada *seed* tersebut. Jika benar terbukti *data leakage*, perbaiki pembagian data, lalu *re-run*. |

---

## Latihan 3 — Validation Report

Buat laporan validasi ringkas untuk dataset eksperimen Anda.

**1. Completeness:** 100% data terkumpul (10 dari 10 log)
**2. Format:** [x] Konsisten / [ ] Ada inkonsistensi: -
**3. Range check (anomali):** Skor MAE/RMSE dipastikan masuk akal dan berada pada batas toleransi skala bintang 1-5.
**4. Logic check:** [x] Parameter sesuai plan / [ ] Ada ketidaksesuaian: -

**Kesimpulan:** [x] Data siap analisis / [ ] Perlu tindakan: -

---

## Refleksi

> Apa perbedaan antara "data yang benar" dan "data yang dipercaya"? Mengapa proses validasi formal diperlukan meskipun data dikumpulkan secara otomatis?

**Jawaban:**
> "Data yang benar" sekadar merujuk pada angka yang berhasil direkam oleh sistem tanpa adanya *error* (seperti nilai MAE 0.21 pada Latihan 2). Namun, angka tersebut belum tentu menjadi "data yang dipercaya" sebelum divalidasi. Data baru bisa dipercaya jika angkanya masuk akal, tidak melanggar batasan logika, dan konsisten dengan teori.
> 
> Proses validasi formal sangat penting meskipun menggunakan *script* otomatis (seperti Python), karena mesin tidak tahu konteks penelitian kita. *Script* yang berjalan mulus tanpa pesan *error* bisa jadi sebenarnya menyimpan *bug* logika matematis atau *data leakage* yang membuat hasilnya bias secara diam-diam.