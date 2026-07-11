# 07-manuskrip

Folder ini berisi draft paper jurnal — disusun per bagian untuk memudahkan revisi.

---

## Status: 🔄 Sedang Berjalan (85% selesai)

---

## Struktur

```
07-manuskrip/
├── 01-abstract.md                # Abstrak (Bahasa Indonesia + Inggris)
├── 02-pendahuluan.md             # Latar Belakang, Problem Statement, RQ
├── 03-tinjauan-pustaka.md        # Related Work, Gap Analysis
├── 04-metodologi.md              # Dataset, Algoritma, Eksperimen
├── 05-hasil-analisis.md          # Tabel, Figure, Uji Statistik
├── 06-diskusi.md                 # Interpretasi, Implikasi, Limitasi
├── 07-kesimpulan.md              # Ringkasan Temuan, Future Work
├── 08-daftar-pustaka.md          # Referensi (APA style)
└── README.md                     # Dokumentasi ini
```

---

## Checklist Progress

| Bagian | Status | Progress | Catatan |
|--------|--------|----------|---------|
| **01. Abstract** | ✅ Selesai | 100% | Bahasa Indonesia done, Bahasa Inggris pending |
| **02. Pendahuluan** | ✅ Selesai | 100% | Latar belakang, problem statement, RQ, kontribusi |
| **03. Tinjauan Pustaka** | 🔄 Draft | 70% | Perlu tambah 3-4 paper related work |
| **04. Metodologi** | ✅ Selesai | 100% | Dataset, algoritma, eksperimen lengkap |
| **05. Hasil & Analisis** | ✅ Selesai | 100% | Tabel, figure, uji statistik sudah integrated |
| **06. Diskusi** | 🔄 Draft | 60% | Interpretasi done, perlu tambah perbandingan literatur |
| **07. Kesimpulan** | ✅ Selesai | 100% | Ringkasan temuan, future work |
| **08. Daftar Pustaka** | 🔄 Review | 80% | 15 referensi, perlu tambah 3-5 referensi |

**Overall Progress:** 85%

---

## Target Publikasi

### Opsi 1: Jurnal Lokal (Primary)

**Jurnal Informatika dan Rekayasa Perangkat Lunak** (Sinta 5)
- **Scope:** Collaborative Filtering, Recommender Systems, Tourism
- **Format:** 12-15 halaman (2-column)
- **Template:** [Link template jurnal]
- **Review Time:** 2-3 bulan
- **Bahasa:** Indonesia (Abstract dalam Inggris)

### Opsi 2: Jurnal RESTI (Stretch Goal)

**Rekayasa Sistem dan Teknologi Informasi** (Sinta 2)
- **Scope:** AI, Machine Learning, Recommender Systems
- **Format:** 10-12 halaman (2-column)
- **Template:** [Link template RESTI]
- **Review Time:** 3-4 bulan
- **Bahasa:** Indonesia atau Inggris

---

## Cara Kompilasi

### 1. Gabungkan Semua Bagian

```bash
# Menggunakan pandoc (harus install dulu)
pandoc 01-abstract.md 02-pendahuluan.md 03-tinjauan-pustaka.md \
       04-metodologi.md 05-hasil-analisis.md 06-diskusi.md \
       07-kesimpulan.md 08-daftar-pustaka.md \
       -o paper-draft-final.pdf \
       --pdf-engine=xelatex \
       --template=template-jurnal.tex
```

### 2. Export ke Word (untuk review pembimbing)

```bash
pandoc *.md -o paper-draft-final.docx
```

### 3. Export ke LaTeX (untuk submission jurnal)

```bash
pandoc *.md -o paper-draft-final.tex --standalone
```

---

## Guidelines Penulisan

### Bahasa

- ✅ **Bahasa Indonesia formal akademik**
- ✅ **Kalimat pasif** (preferred untuk paper Indonesia)
- ✅ Istilah teknis konsisten: CF, CARS, MAE, RMSE, Haversine
- ❌ Hindari bahasa kasual: "kita", "sangat bagus", "luar biasa"

### Format Tabel

```markdown
| Fold | Baseline MAE | Context-Aware MAE | Δ MAE |
|------|--------------|-------------------|-------|
| 1    | 0,6720       | 0,6487            | -0,0233 |
| ...  | ...          | ...               | ...   |
```

**Note:** Gunakan koma (,) sebagai decimal separator untuk paper Indonesia.

### Format Figure

```markdown
![Perbandingan MAE Baseline vs Context-Aware](../06-output/figures/boxplot_mae_comparison.png)

**Gambar 1.** Boxplot perbandingan distribusi MAE untuk kedua algoritma pada 5-Fold Cross Validation. Context-Aware CF menunjukkan median MAE lebih rendah (0,6511) dibanding Baseline CF (0,6720) dengan variance lebih kecil.
```

### Referensi (APA 7th Edition)

```markdown
Adomavicius, G., & Tuzhilin, A. (2011). Context-aware recommender systems. 
In F. Ricci, L. Rokach, B. Shapira, & P. B. Kantor (Eds.), *Recommender 
Systems Handbook* (pp. 217-253). Springer. 
https://doi.org/10.1007/978-0-387-85820-3_7
```

---

## Review Cycle

### Siklus 1 (Target: 2024-03-25)

- [ ] Submit draft ke pembimbing
- [ ] Feedback pembimbing (1-2 minggu)
- [ ] Revisi berdasarkan feedback
- [ ] Self-review checklist

### Siklus 2 (Target: 2024-04-08)

- [ ] Submit revisi ke pembimbing
- [ ] Approval final
- [ ] Polish formatting (template jurnal)
- [ ] Submission ke jurnal

---

## Self-Review Checklist

Sebelum submit ke pembimbing, pastikan:

### Konten

- [ ] Semua claim didukung data/referensi
- [ ] Tidak ada placeholder text (`TODO`, `[FILL THIS]`)
- [ ] Formula matematis ditulis benar (LaTeX notation)
- [ ] Semua figure & table direferensikan dalam teks
- [ ] Interpretasi hasil jelas dan tidak berlebihan

### Format

- [ ] Abstract ≤ 250 kata
- [ ] Keywords 4-6 kata (Bahasa Indonesia + Inggris)
- [ ] Heading hierarchy konsisten (H1 → H2 → H3)
- [ ] Decimal separator: koma (,) bukan titik (.)
- [ ] Spasi setelah tanda baca

### Referensi

- [ ] Minimal 15 referensi (target: 18-20)
- [ ] Semua referensi disitasi dalam teks
- [ ] Tidak ada sitasi tanpa referensi di daftar pustaka
- [ ] Format APA 7th konsisten
- [ ] DOI disertakan (jika tersedia)

### Etika

- [ ] Dataset tidak mengandung PII
- [ ] Geolokasi hanya untuk destinasi publik
- [ ] No plagiarism (Turnitin ready)
- [ ] Acknowledgment (pembimbing, sponsor)

---

## Backup & Version Control

```bash
# Backup draft sebelum revisi besar
cp -r 07-manuskrip 07-manuskrip-backup-$(date +%Y%m%d)

# Track changes dengan git
git add 07-manuskrip/*.md
git commit -m "Draft paper: complete Section 5 (Hasil & Analisis)"
```

---

## Troubleshooting

**Error: Pandoc not found**
```bash
# Install pandoc
# Windows: Download dari https://pandoc.org/installing.html
# Mac: brew install pandoc
# Linux: sudo apt install pandoc
```

**Error: LaTeX engine not found**
```bash
# Install MiKTeX (Windows) atau TeX Live (Mac/Linux)
# https://miktex.org/download
```

**Figure tidak muncul di PDF**
- Pastikan path figure benar (relative path)
- Gunakan format PNG (bukan JPEG untuk grafik)
- Resolusi minimal 300 DPI

---

## Next Actions (Priority)

1. **Urgent:** Lengkapi Tinjauan Pustaka (tambah 3-4 paper)
2. **Important:** Review Diskusi (tambah perbandingan literatur)
3. **Nice-to-have:** Translate Abstract ke Bahasa Inggris
4. **Before submission:** Self-review checklist + Grammarly check

---

**Last Updated:** 2024-03-18  
**Next Deadline:** Submit draft ke pembimbing (2024-03-25)
