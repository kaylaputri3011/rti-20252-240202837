# example-riset-directory

Contoh struktur direktori penelitian yang lengkap — rekonstruksi berdasarkan penelitian riil Kayla Putri Arsonisr (240202837).

---

## Konteks Penelitian

**Judul:** Peningkatan Akurasi Sistem Rekomendasi Pariwisata Semarang Menggunakan Algoritma Context-Aware Collaborative Filtering

**Peneliti:** Kayla Putri Arsonisr (NIM: 240202837), Program Studi Teknik Informatika (Kelas 4IKRA)

**Metode:** Eksperimen terkontrol menggunakan dataset 4.362 ulasan riil Google Maps, perbandingan Baseline User-Based CF vs Context-Aware CF dengan spatial pre-filtering (Haversine, radius 10 km), validasi 5-Fold Cross Validation

**Status:** Tahap 1–4 selesai; Tahap 5 (penulisan paper) sedang berjalan (85%)

---

## Struktur Direktori

| Folder | Isi | Deliverable |
|---|---|---|
| [00-admin/](00-admin/) | Jadwal penelitian, log progres, risk management | `jadwal-dan-log-penelitian.md` |
| [01-proposal/](01-proposal/) | Proposal penelitian lengkap | `proposal-penelitian.md` |
| [02-literatur/](02-literatur/) | Matriks literatur (15 paper), gap analysis | `matriks-literatur.md` |
| [03-teori/](03-teori/) | Arsitektur sistem, landasan teori (CF, CARS), formula Haversine | `arsitektur-sistem.md` |
| [04-data/](04-data/) | Dataset raw (5.123) dan clean (4.362), EDA | `raw/`, `clean/` |
| [05-kode/](05-kode/) | Source code (Baseline CF, Context-Aware CF, eksperimen) | `src/`, `notebooks/`, `tests/` |
| [06-output/](06-output/) | Tabel hasil eksperimen, visualisasi (boxplot, scatter, improvement) | `tables/`, `figures/` |
| [07-manuskrip/](07-manuskrip/) | Draft paper jurnal (Abstrak–Kesimpulan) | Draft sedang berjalan (85%) |
| [08-laporan/](08-laporan/) | Laporan penelitian lengkap | [`laporan-penelitian.md`](08-laporan/laporan-penelitian.md) |
| [09-docs/](09-docs/) | Dokumentasi rencana & status tiap tahap (1–5) | `rencana-penelitian.md`, `tahap-N-*.md` |

---

## Temuan Utama (Ringkasan)

- **Baseline CF (standar):** MAE = 0,6720 ± 0,0025 (Pearson Correlation, K=30)
- **Context-Aware CF (spatial):** MAE = **0,6511 ± 0,0021** (pre-filtering Haversine, radius 10 km)
- **Improvement:** Penurunan MAE **3,11%** (0,0209 poin), signifikan dengan ***p* < 0,001**, Cohen's *d* = 8,37
- **Error by Distance:** Perbaikan terbesar pada destinasi dekat (**3,88%** untuk jarak < 5 km)
- **Coverage:** 87,7% prediksi menggunakan CF penuh (12,3% ter-filter di luar radius)
- **Hipotesis H₁ DITERIMA:** Context-Aware CF terbukti secara empiris lebih akurat dibanding Baseline CF

Detail lengkap: [08-laporan/laporan-penelitian.md](08-laporan/laporan-penelitian.md)

---

## Kontribusi Penelitian

| Aspek | Kontribusi |
|-------|------------|
| **Context Gap** | Membuktikan empiris bahwa dimensi spasial meningkatkan akurasi CF pada domain pariwisata |
| **Method Gap** | Implementasi Context-Aware CF untuk pariwisata lokal Indonesia (Semarang) |
| **Evaluation Gap** | Protokol validasi ketat (5-Fold CV) yang reproducible |
| **Dataset** | Dataset terstruktur pariwisata Semarang (4.362 ulasan) untuk penelitian lanjutan |

---

## Status Tahapan

- [x] **Tahap 1** — Perancangan Arsitektur & Studi Literatur — *Selesai* ([detail](09-docs/tahap-1-arsitektur-dan-studi-literatur.md))
- [x] **Tahap 2** — Pengumpulan & Preprocessing Data — *Selesai* ([detail](09-docs/tahap-2-pengumpulan-data.md))
- [x] **Tahap 3** — Implementasi Algoritma — *Selesai* ([detail](09-docs/tahap-3-implementasi-algoritma.md))
- [x] **Tahap 4** — Eksperimen & Evaluasi — *Selesai* ([detail](09-docs/tahap-4-eksperimen-evaluasi.md))
- [ ] **Tahap 5** — Penulisan Draft Paper — *Sedang Berjalan (85%)* ([detail](09-docs/tahap-5-penulisan-paper.md))

---

## Cara Reproduksi

```bash
# Tahap 2: Preprocessing data
cd 05-kode/src/data && python preprocess.py

# Tahap 3: Grid search threshold jarak optimal
cd 05-kode/notebooks && jupyter notebook 03_grid_search_radius.ipynb

# Tahap 4: Eksperimen 5-Fold CV
cd 05-kode/src && python experiment.py

# Tahap 4: Analisis hasil & visualisasi
cd 05-kode/notebooks && jupyter notebook 04_analysis.ipynb
```

---

## Catatan

- Dataset raw (5.123 records) dan clean (4.362 records) tersedia di folder `04-data/`
- Source code fully documented dengan unit tests (12 test cases, 100% pass)
- Random seed = 42 untuk reproducibility
- Visualisasi hasil (3 figures) tersedia di `06-output/figures/`
- Paper draft (85% selesai) sedang dalam review pembimbing

---

## Author

Kayla Putri Arsonisr (240202837)  
Program Studi Teknik Informatika (Kelas 4IKRA)
