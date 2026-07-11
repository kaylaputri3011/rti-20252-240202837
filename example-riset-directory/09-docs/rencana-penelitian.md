# Rencana Penelitian: Context-Aware Collaborative Filtering untuk Pariwisata Semarang

## 1. Ringkasan

| Item | Keterangan |
|---|---|
| Judul | Peningkatan Akurasi Sistem Rekomendasi Pariwisata Semarang Menggunakan Algoritma Context-Aware Collaborative Filtering |
| Peneliti | Kayla Putri Arsonisr (240202837) |
| Target Publikasi | Skripsi / Jurnal Lokal (Sinta 4-5) |
| Stack | Python, pandas, scikit-learn, geopy, scipy |
| Masalah | CF standar mengabaikan jarak geografis → rekomendasi tidak praktis (destinasi terpisah puluhan km) |
| Solusi | Integrasi filter spasial (Haversine, radius 10 km) + 5-Fold CV untuk validasi ketat |
| Dataset | 4.362 ulasan Google Maps Semarang (0 missing values) |
| Hasil Target | MAE Context-Aware < MAE Baseline (penurunan ≥ 2%, p < 0.05) |

---

## 2. Alur Kerja (Roadmap)

Setiap tahap memiliki file rencana detail tersendiri agar lebih rapi:

- [x] **Tahap 1** — [Perancangan Arsitektur & Studi Literatur](tahap-1-arsitektur-dan-studi-literatur.md) — *Selesai*
- [x] **Tahap 2** — [Pengumpulan & Preprocessing Data](tahap-2-pengumpulan-data.md) — *Selesai*
- [x] **Tahap 3** — [Implementasi Algoritma (Baseline & Context-Aware)](tahap-3-implementasi-algoritma.md) — *Selesai*
- [x] **Tahap 4** — [Eksperimen, Evaluasi & Analisis Statistik](tahap-4-eksperimen-evaluasi.md) — *Selesai*
- [ ] **Tahap 5** — [Penulisan Draft Paper/Laporan](tahap-5-penulisan-paper.md) — *Sedang Berjalan*

---

## 3. Catatan

Dokumen ini adalah indeks utama. Detail teknis, skema, dan keputusan masing-masing tahap dicatat pada file `tahap-N-*.md` terkait dan diperbarui seiring progres pengerjaan.

**Status Keseluruhan:** 🔄 Tahap 5 (Penulisan) — 85% selesai

**Progres Milestone:**
- ✅ Dataset collected & cleaned (4.362 records)
- ✅ Baseline CF implemented & validated
- ✅ Context-Aware CF implemented (Haversine pre-filtering)
- ✅ 5-Fold CV executed (MAE: 0.651 vs 0.672, p < 0.001)
- 🔄 Draft paper in progress

**Next Actions:**
- Finalisasi bagian Related Work
- Revisi visualisasi hasil eksperimen
- Review pembimbing
