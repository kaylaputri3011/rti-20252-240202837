# WS-02: Problem Statement

> **Bab 2 — Problem Formulation & System Context**

---

## Ringkasan Materi

### Problem Formation Model

Masalah riset melewati 5 tahap transformasi. Melompat langsung dari Reality ke Variable adalah kesalahan paling umum.

```
Reality → Observed Issue (Symptom) → Diagnosed Problem (Root Cause)
→ Researchable Problem (Scoped) → Measurable Variable (Operationalized)
```

### Topic ≠ Problem ≠ Research Problem

| Level | Contoh | Status |
|-------|--------|--------|
| **Topik** | Keamanan IoT | Terlalu luas, tidak bisa diuji |
| **Problem** | MQTT tidak terenkripsi | Spesifik tapi belum riset |
| **Research Problem** | Belum ada studi membandingkan overhead TLS 1.3 vs DTLS pada MQTT di IoT RAM < 64KB | Bisa dirancang eksperimennya |

### Symptom vs Root Cause

Apa yang diamati (gejala) ≠ mengapa terjadi (akar masalah). Gunakan **5 Whys** atau **Fishbone Diagram** untuk menggali.

Contoh: "User meninggalkan checkout" (symptom) → "Waktu loading > 8 detik karena API call sequential" (root cause).

### System Thinking

Setiap masalah riset TI harus terikat pada komponen sistem: **Input → Process → Output → Outcome → Constraints → Stakeholders**.

### Problem Quality Check

Masalah riset yang layak harus memenuhi 5 kriteria:
- **Clarity** — Satu orang membaca akan paham
- **Measurability** — Ada metrik kuantitatif
- **Relevance** — Penting untuk domain
- **Testability** — Bisa gagal (falsifiable)
- **Impact** — Ada kontribusi jika terjawab

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Menyelesaikan masalah (*solve*) | Memahami dan membuktikan (*understand & prove*) |
| Masalah | Bug, error, fitur belum ada | Gap dalam pengetahuan |
| Scope | Selesaikan semua yang perlu | Batasi agar bisa dibuktikan |
| Output | Working system | Evidence, paper, replicable findings |

### Istilah Penting

- **Problem Statement** — Formulasi tertulis: konteks sistem + gap + dampak + justifikasi
- **System Context** — Deskripsi lengkap: input, proses, output, outcome, constraints, stakeholders
- **Problem Drift** — Masalah "bermutasi" dari pendahuluan ke metodologi karena statement awal tidak presisi
- **Solution-First Thinking** — Memulai dari solusi tanpa masalah yang jelas — berbahaya dalam riset
- **Operational Definition** — Definisi variabel yang cukup jelas agar peneliti lain bisa mengukur hal yang sama

---

## Template A.2 — Problem Statement Builder

```
PROBLEM STATEMENT BUILDER

Domain & Konteks
  Domain   : Machine Learning / Pariwisata (Sistem Rekomendasi)
  Konteks  : Rekomendasi destinasi wisata di Kota Semarang berbasis personalisasi pengguna.

System Context
  Input       : Data historis rating tempat wisata dari berbagai pengguna (User-Item Rating Matrix).
  Process     : Penghitungan kemiripan (similarity) antar pengguna dan prediksi nilai rating menggunakan algoritma Collaborative Filtering.
  Output      : Daftar rekomendasi tempat wisata (Top-N recommendation) beserta prediksi ratingnya.
  Outcome     : Wisatawan mendapatkan rekomendasi yang relevan dengan seleranya, menghemat waktu pencarian informasi.
  Constraints : Masalah sparsity (matriks rating banyak yang kosong) dan cold-start (pengguna baru yang belum memberi rating).
  Stakeholders: Wisatawan (pengguna akhir) dan pengelola tempat wisata.

Fenomena → Problem
  Fenomena yang diamati             : Wisatawan sering kebingungan memilih tempat wisata di Semarang karena banyaknya pilihan (information overload).
  Gejala (symptom) yang terukur     : Pencarian destinasi memakan waktu lama dan rekomendasi yang ada di internet sering kali bersifat umum (tidak sesuai selera spesifik).
  Masalah yang didiagnosis          : Belum adanya sistem penyaringan informasi yang memanfaatkan kemiripan preferensi antar pengguna untuk merekomendasikan tempat secara personal.
  Masalah riset (researchable)      : Bagaimana tingkat akurasi algoritma Collaborative Filtering dalam memprediksi rating tempat wisata di Kota Semarang berdasarkan matriks data pengguna?
  Variabel yang terukur             : Tingkat error prediksi algoritma, yang diukur menggunakan metrik Mean Absolute Error (MAE).

Problem Quality Check
  [x] Clarity — Apakah satu orang membaca akan paham?
  [x] Measurability — Apakah ada metrik kuantitatif?
  [x] Relevance — Apakah penting untuk domain?
  [x] Testability — Apakah bisa gagal?
  [x] Impact — Apakah ada kontribusi jika terjawab?

Problem Statement (1 paragraf):
  Wisatawan yang berkunjung ke Kota Semarang kerap mengalami kesulitan dalam memilih destinasi akibat kelebihan informasi dan banyaknya pilihan tempat wisata yang ada (information overload). Masalah ini berakar dari kurangnya sistem rekomendasi terpersonalisasi yang mampu menyaring pilihan berdasarkan selera unik masing-masing individu, bukan sekadar popularitas tempat wisata secara umum. Meskipun data riwayat kunjungan dan rating dari wisatawan lain tersedia, data tersebut belum dimanfaatkan secara optimal untuk memprediksi preferensi pengguna secara komputasional. Oleh karena itu, penelitian ini bertujuan mengimplementasikan dan mengukur tingkat akurasi metode Collaborative Filtering dalam memprediksi rating destinasi wisata di Kota Semarang, sehingga dapat menghasilkan rekomendasi yang secara spesifik relevan dengan preferensi masing-masing wisatawan.

```

---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:** Sistem Rekomendasi Pariwisata Berbasis Machine Learning.

| Tahap | Hasil |
|-------|-------|
| Reality | Banyaknya jumlah tempat wisata di Semarang membuat wisatawan kesulitan menentukan tujuan yang sesuai dengan selera mereka. |
| Observed Issue (Symptom) | Rekomendasi wisata di brosur atau portal web seringkali tidak relevan karena bersifat statis dan memukul rata semua wisatawan. |
| Diagnosed Problem (Root Cause) | Tidak adanya sistem cerdas yang mampu memetakan dan menghubungkan kemiripan pola kesukaan (rating) antar sesama wisatawan secara otomatis. |
| Researchable Problem | Seberapa akurat pendekatan Collaborative Filtering dalam memprediksi preferensi wisata pengguna berdasarkan data matriks rating historis? |
| Measurable Variable | Nilai selisih antara rating asli dan rating prediksi yang diukur melalui metrik Mean Absolute Error (MAE). |

**Apakah terjebak solution-first thinking?** [ ] Ya / [x] Tidak
> Jika ya, kembali ke tahap mana? ________________________

---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input | Dataset berupa daftar pengguna (User ID), daftar tempat wisata (Item ID), dan nilai rating (1-5) yang diberikan pengguna. |
| Process | Komputasi algoritma Collaborative Filtering untuk menghitung jarak kemiripan (similarity) antar pengguna dan melakukan perhitungan prediksi rating. |
| Output | Hasil prediksi berupa angka estimasi rating untuk tempat wisata yang belum pernah dikunjungi oleh pengguna target. |
| Outcome | Wisatawan lebih cepat dan tepat dalam menemukan destinasi, serta potensi peningkatan kunjungan ke lokasi wisata tersembunyi (hidden gem) yang relevan. |
| Constraints | Kualitas hasil prediksi sangat bergantung pada kelengkapan data (terancam oleh data sparsity). |
| Stakeholders | Pengguna aplikasi rekomendasi (wisatawan) dan pengembang perangkat lunak (software developer). |

**Komponen mana yang paling relevan dengan masalah riset?** Process (karena metode komputasi dievaluasi di sini) dan Output (karena akurasi hasil dari metode akan diukur kelayakannya).

---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity | 4 | Subjek penelitian (tempat wisata Semarang) dan metode (Collaborative Filtering) sudah jelas, walau bisa ditambahkan detail jumlah dataset yang digunakan. |
| Measurability |5| Sangat dapat diukur. Perbandingan antara prediksi algoritma dengan nilai aktual pengguna dapat dihitung secara presisi menggunakan MAE. |
| Relevance |5| Sangat relevan di era smart tourism di mana personalisasi pengalaman pengguna adalah fokus utama industri pariwisata. |
| Testability |5| Hipotesis bisa gagal; ada kemungkinan bahwa Collaborative Filtering justru menghasilkan tingkat eror (MAE) yang sangat tinggi jika matriks datanya terlalu kosong (sparse). |
| Impact |4| Memberikan validasi empiris kelayakan Collaborative Filtering untuk studi kasus pariwisata lokal di Semarang. |

**Skor total:** 23 / 25

**Problem statement versi final (1 paragraf):**
> Wisatawan yang berkunjung ke Kota Semarang kerap mengalami kesulitan dalam memilih destinasi akibat kelebihan informasi dan banyaknya pilihan tempat wisata yang ada (information overload). Masalah ini berakar dari kurangnya sistem rekomendasi terpersonalisasi yang mampu menyaring pilihan berdasarkan selera unik masing-masing individu, bukan sekadar popularitas tempat wisata secara umum. Meskipun data riwayat kunjungan dan rating dari wisatawan lain tersedia, data tersebut belum dimanfaatkan secara optimal untuk memprediksi preferensi pengguna secara komputasional. Oleh karena itu, penelitian ini bertujuan mengimplementasikan dan mengukur tingkat akurasi metode Collaborative Filtering dalam memprediksi rating destinasi wisata di Kota Semarang, sehingga dapat menghasilkan rekomendasi yang secara spesifik relevan dengan preferensi masing-masing wisatawan.

---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

##Jawaban

> ​Perbedaan paling mendasar ada pada sifat ketidaktahuan (unknowns) dan tujuan akhir.
​> Saat menemukan masalah coding (bug), kita tahu bahwa sistem seharusnya bisa berjalan. Pendekatannya adalah troubleshooting: kita mencari letak kesalahan sintaks atau logika agar program kembali berfungsi sesuai spesifikasi. Tujuannya murni perbaikan rekayasa (engineering).
> ​Sebaliknya, masalah riset mendefinisikan hal yang memang belum diketahui atau belum terbukti kebenarannya oleh komunitas ilmiah. Misalnya, kita tidak tahu apakah algoritma A akan efektif di studi kasus B. Pendekatannya adalah investigasi sistematis: merancang eksperimen, mengumpulkan data, dan menguji variabel (seperti menghitung MAE) untuk mengisi knowledge gap. Tujuannya adalah menghasilkan temuan baru yang valid dan dapat dipertanggungjawabkan, bukan sekadar membuat program berjalan tanpa eror.
