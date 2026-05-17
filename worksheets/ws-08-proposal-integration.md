# WS-08: Proposal Integration (UTS)

> **Bab 8 — Proposal & Checkpoint**

---

## Ringkasan Materi

### Proposal = Satu Argumen Utuh

Proposal riset bukan kumpulan bab yang independen. Ia adalah **satu argumen** yang mengalir dari masalah ke rencana solusi. Jika satu koneksi putus, seluruh proposal kehilangan koherensi.

### Integration Map — 6 Koneksi Kritis

```
Problem (Bab 2) → Gap (Bab 3) → RQ & H (Bab 4) → Metrik (Bab 5) → Sistem (Bab 6) → Eksperimen (Bab 7)
```

| Koneksi | Pertanyaan Verifikasi |
|---------|----------------------|
| Problem → Gap | Apakah gap muncul dari analisis literatur terhadap masalah? |
| Gap → RQ | Apakah RQ langsung menjawab gap yang teridentifikasi? |
| RQ → Metrik | Apakah setiap variabel di RQ punya metrik terdefinisi? |
| Metrik → Sistem | Apakah setiap metrik bisa diukur oleh komponen sistem? |
| Sistem → Eksperimen | Apakah desain eksperimen menggunakan sistem sebagai instrumen? |

### Koherensi Vertikal + Horizontal

- **Vertikal** — Alur logis atas-ke-bawah (problem → experiment)
- **Horizontal** — Konsistensi terminologi (nama variabel di RQ = di hipotesis = di metrik = di desain)

### Jebakan Kognitif

| Jebakan | Deskripsi |
|---------|----------|
| "Selling" Introduction | Menulis promosi, bukan menyajikan data dan gap |
| Copy-paste Methodology | Menyalin deskripsi tekstbook tanpa menyesuaikan ke RQ |
| Optimistic Timeline | Meremehkan waktu implementasi; selalu tambah buffer 30-50% |
| No Possibility of Failure | Mengimplikasikan hasil pasti sukses — proposal jujur mengakui H₀ mungkin tidak ditolak |

### Struktur Proposal

1. **Pendahuluan** — Latar belakang + problem statement (Bab 1-2)
2. **Tinjauan Pustaka** — Literature review + gap + baseline (Bab 3)
3. **RQ / Kontribusi / Hipotesis** — (Bab 4)
4. **Metodologi** — Metrik + sistem + desain eksperimen (Bab 5-7)
5. **Timeline & Output**

### Istilah Penting

- **Integration Map** — Diagram 6 koneksi kritis antar komponen proposal
- **Vertical Coherence** — Alur logis atas-ke-bawah
- **Horizontal Coherence** — Konsistensi terminologi di semua bagian
- **Checkpoint** — Titik self-assessment sebelum transisi dari desain ke eksekusi

---

## Template A.8 — Integration Checklist

PROPOSAL INTEGRATION CHECKLIST

Koneksi Vertikal (Flow Atas-Bawah):
  [x] Problem → Gap: masalah terdokumentasi di literatur
  [x] Gap → RQ: pertanyaan menjawab gap spesifik
  [x] RQ → Hypothesis: hipotesis memprediksi jawaban
  [x] Hypothesis → Metric: metrik mengukur variabel dalam hipotesis
  [x] Metric → System: komponen sistem menghasilkan/mengukur metrik
  [x] System → Experiment: desain eksperimen menggunakan sistem

Koneksi Horizontal (Konsistensi):
  [x] Istilah sama di semua bagian
  [x] Variabel di RQ = variabel di hipotesis = metrik di desain
  [x] Scope tidak berubah dari masalah ke eksperimen

Rubrik Self-Assessment:
| Kriteria | 1 (Lemah) | 2 (Cukup) | 3 (Baik) | Skor |
|----------|-----------|-----------|----------|------|
| Koherensi |          |           |    [x]   |  3   |
| Specificity |        |           |    [x]   |  3   |
| Feasibility |        |    [x]    |          |  2   |
| Rigor     |          |           |    [x]   |  3   |

---

## Latihan 1 — Kompilasi Proposal Mini

Kumpulkan hasil dari WS-02 sampai WS-07 menjadi satu ringkasan proposal.

| Komponen | Sumber | Isi (1-2 kalimat) |
|----------|--------|-------------------|
| Problem Statement | WS-02 | *Contoh: Sistem rekomendasi memiliki akurasi tinggi (RMSE 0.87) tetapi satisfaction score rendah (45/100). Gap antara metrik teknis dan kepuasan pengguna belum diteliti.* |
| Gap | WS-03 | *Contoh: Tidak ada studi yang mengintegrasikan collaborative filtering dengan user-context signals untuk meningkatkan satisfaction.* |
| RQ | WS-04 | *Contoh: Apakah penambahan context-aware signals pada collaborative filtering meningkatkan satisfaction score tanpa menurunkan RMSE?* |
| Hipotesis | WS-04 | *Contoh: H₁: Sistem CF+context menghasilkan satisfaction ≥ 70/100 dengan RMSE ≤ 0.90 dibanding baseline CF murni.* |
| Variabel & Metrik | WS-05 | *Contoh: IV = jenis sistem (CF vs CF+context); DV = satisfaction score (skala 0-100) + RMSE (regresi).* |
| Sistem | WS-06 | |
| Desain Eksperimen | WS-07 | |

---

## Latihan 2 — Integration Checklist

Verifikasi 6 koneksi kritis. Isi dengan merujuk tabel di Latihan 1.

| Koneksi | Status | Bukti |
|---------|--------|-------|
| Problem → Gap | *Contoh: ✅ — gap muncul dari 15 paper Bab 3 yang tidak ada yang mengkombinasikan CF + context untuk satisfaction* | |
| Gap → RQ | *Contoh: ✅ — RQ langsung menanyakan apakah CF+context meningkatkan satisfaction* | |
| RQ → Hypothesis | *Contoh: ✅ — H₁ memprediksi satisfaction ≥ 70 dengan threshold RMSE ≤ 0.90* | |
| Hypothesis → Metric | | |
| Metric → System | | |
| System → Experiment | | |

**Koneksi mana yang paling lemah?** _______________________
**Bagaimana cara memperkuatnya?**
> ___________________________________________________

**Konsistensi horizontal — apakah istilah dan scope konsisten?** [ ] Ya / [ ] Tidak
> Jika tidak, di bagian mana terjadi inkonsistensi? _________

---

## Latihan 3 — Rubrik Self-Assessment

Evaluasi proposal mini menggunakan rubrik.

| Kriteria | Skor (1-3) | Justifikasi |
|----------|-----------|-------------|
| Koherensi | *Contoh: 2 — koneksi gap→RQ masih lemah karena gap belum cukup narrow* | |
| Specificity | *Contoh: 3 — metrik (satisfaction 0-100, RMSE) sudah terdefinisi numerik* | |
| Feasibility | | |
| Rigor | | |

**Skor total:** _____ / 12

**Apakah proposal siap untuk fase eksekusi?** [ ] Ya / [ ] Belum
> Jika belum, apa yang perlu diperbaiki? __________________

---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-08, bagian mana yang paling mudah dan paling sulit? Mengapa? Apa yang akan dilakukan berbeda jika mengulang dari awal?

**Bagian termudah:** ____________________________________
**Bagian tersulit:** ____________________________________
**Yang akan dilakukan berbeda:**
> ___________________________________________________
> ___________________________________________________
