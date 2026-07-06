# WS-16: Presentation & Defense (UAS)

> **Bab 16 — Presentasi & Pertahanan Ilmiah**

---

## Ringkasan Materi

### Scientific Defense Model

```
Research Work → Presentation → Questioning → Defense → Evaluation → Acceptance
```

### Presentasi ≠ Ringkasan Paper

| Paper | Presentasi |
|-------|-----------|
| Dibaca (self-paced) | Didengar (presenter-paced) |
| Detail lengkap | Ide kunci + highlight |
| Tabel numerik detail | Grafik visual + angka kunci |
| Pembaca bisa re-read | Audiens dengar sekali |

**Prinsip:** Presentasi membutuhkan **reformulasi**, bukan kompresi. Medium berbeda = pendekatan berbeda.

### Claim-Evidence-Reasoning (CER)

Setiap jawaban defense harus memiliki:
1. **Claim** — Pernyataan yang dijawab
2. **Evidence** — Data/fakta pendukung
3. **Reasoning** — Logika yang menghubungkan evidence ke claim

**Contoh:**
| Pertanyaan | Bad Answer | Good Answer (CER) |
|-----------|-----------|-------------------|
| "Kenapa hanya 3 dataset?" | "Tiga sudah cukup" | "3 dataset mewakili variasi: small-clean, medium-clean, medium-noisy [E]. Generalisasi perlu validasi lanjut — listed as limitation [R]" |
| "Hasil DS-3 menurun?" | "Itu outlier" | "Ya, karena distribusi heavy-tail melanggar asumsi Gaussian [E]. Ini menunjukkan boundary condition metode [R]" |
| "Effect size?" | "p=0.003, jadi signifikan" | "Cohen's d=1.2 (large effect) [E] — bukan hanya signifikan tapi substansial [R]" |

### Slide Design — One Slide, One Message

**Optimal 9-Slide Plan (15 menit):**

| # | Slide | Waktu | Pesan |
|---|-------|-------|-------|
| 1 | Title + context | 1 min | Apa ini tentang apa |
| 2 | Problem + motivation | 2 min | Mengapa penting |
| 3 | Gap + RQ | 1.5 min | Apa yang belum terjawab |
| 4 | Method overview | 2 min | Bagaimana dijawab (diagram) |
| 5 | Key result — tabel | 2 min | Temuan utama |
| 6 | Key result — grafik | 2 min | Pola visual |
| 7 | Interpretation + failure | 2 min | Apa artinya |
| 8 | Limitation + future | 1.5 min | Batasan & arah |
| 9 | Conclusion + contribution | 1 min | Closing message |

### Anticipatory Defense

Prediksi pertanyaan berdasarkan kategori:

| Kategori | Contoh Pertanyaan |
|---------|------------------|
| Problem | "Mengapa masalah ini penting?" |
| Gap | "Bagaimana dengan studi X yang sudah menjawab ini?" |
| Method | "Mengapa metode ini, bukan Y?" |
| Results | "Bagaimana menjelaskan anomali di DS-3?" |
| Generalization | "Apakah bisa diterapkan di domain lain?" |

### Tiga Prinsip Jawaban

1. **Direct** — Jawab dulu, elaborasi kemudian
2. **Data-based** — Tunjuk evidence spesifik
3. **Honest** — Akui limitasi jika memang ada

### Jebakan Kognitif

1. "Presentasi = semua yang ada di paper" → terlalu padat
2. "Slide cantik = presentasi bagus" → konten > estetika
3. "Tidak bisa jawab = gagal" → "I don't know, but..." menunjukkan kejujuran
4. "Tidak perlu latihan — saya paham riset saya" → latihan = menemukan celah

---

## Template A.16 — Defense Preparation Sheet

DEFENSE PREPARATION

Slide Deck Plan:
> Total slides   : 9 slides utama + 1 Title + 1 Closing (Total 11)
> Time per slide : ~1.5 menit
> Total time     : 15 menit

Slide Outline:
| # | Pesan Utama | Visual | Waktu |
|---|-------------|--------|-------|
| 1 | Title       | Judul, NIM (240202892), dan Nama (Abu Zaki) | 30s   |
| 2 | Problem     | Ilustrasi rute wisata Semarang yang tidak logis | 2min  |
| 3 | Gap + RQ    | Tabel perbandingan algoritma CF biasa vs Context-Aware | 1.5min|
| 4 | Method      | Diagram alir K-Fold & Dataset (4.362 records) | 2min  |
| 5 | Key Result 1| Tabel komparasi MAE & RMSE | 2min  |
| 6 | Key Result 2| Bar chart / Box plot error rate | 2min  |
| 7 | Interpretasi| Dampak praktis bagi UX turis di Semarang | 2min  |
| 8 | Limitasi    | Faktor kemacetan dan topografi yang belum masuk | 1.5min|
| 9 | Conclusion  | Ringkasan hipotesis terbukti & Future Work | 1.5min|

Anticipatory Defense Matrix:
| Kategori | Pertanyaan Potensial | Jawaban (CER) |
|----------|---------------------|---------------|
| Problem  | Mengapa jarak jadi fokus utama? | Bukti: CF standar sering merekomendasikan tempat bagus tapi terpisah 30km. Alasan: Jarak adalah batasan fisik absolut dalam UX pariwisata. |
| Gap      | Apa bedanya dengan riset sebelumnya? | Bukti: Studi LBS lokal jarang memakai Google Maps Data riil sebesar ini. Alasan: Kami memadukan ulasan riil (4.362 data) dengan algoritma spasial. |
| Method   | Yakin tidak ada data leakage? | Bukti: Perhitungan `item_means` murni dari `train_idx`. Alasan: Isolasi ketat K-Fold menjamin data uji 100% tidak pernah dilihat model. |
| Results  | Beda MAE cuma 0.021, apa penting? | Bukti: Effect size besar & Paired t-test p<0.05. Alasan: Secara dunia nyata, beda skor error ini menyeleksi rute 1 jam perjalanan menjadi 15 menit. |
| Generalization | Bisa dipakai di kota lain? | Bukti: Algoritma menggunakan Haversine absolut. Alasan: Bisa, namun parameter bobot jarak harus disesuaikan ulang dengan kepadatan tata kota tujuan. |

Latihan:
> Latihan 1: H-3 UAS — Fokus pada kelancaran transisi antar slide (target 15 menit).
> Latihan 2: H-2 UAS — Fokus pada intonasi dan penekanan pada slide Results (Tabel MAE).
> Latihan 3: H-1 UAS — Mock-up Q&A (Latihan menjawab langsung ke poin Claim-Evidence-Reasoning).

---

## Latihan 1 — Slide Outline

Rencanakan presentasi 15 menit untuk riset Anda.

| # | Pesan Utama | Visual yang Digunakan | Waktu |
|---|-------------|----------------------|-------|
| 1 | Judul & Konteks: Sistem Rekomendasi Pariwisata Semarang (Context-Aware). | Title slide, logo Universitas Putra Bangsa, nama Abu Zaki. | 1 min |
| 2 | Problem: CF standar mengabaikan jarak (merekomendasikan wisata beda ujung kota). | Peta Semarang dengan titik wisata yang saling berjauhan (Visualisasi jarak). | 2 min |
| 3 | Gap + RQ: Integrasi filter geospasial pada CF untuk menurunkan *error* rekomendasi. | *Bullet points* singkat (Rumusan Masalah). | 1.5 min |
| 4 | Method: Penggunaan 4.362 data ulasan riil Google Maps, *Haversine formula*, & 5-Fold CV. | Diagram *Pipeline Preprocessing* & *Dataset Snapshot*. | 2 min |
| 5 | Results (Tabel): *Context-Aware* sukses mencatat MAE 0.651, mengungguli *Baseline* (0.672). | Tabel bersih (*Clean Table*) perbandingan metrik dengan cetak tebal pada skor terbaik. | 2 min |
| 6 | Results (Grafik): Stabilitas metode intervensi di setiap putaran (*runs*). | *Box Plot* sebaran MAE hasil pengujian Python. | 2 min |
| 7 | Interpretation: Hipotesis diterima, efek ukuran (Cohen's d) besar. | Teks singkat tentang *practical significance* di lapangan. | 2 min |
| 8 | Limitation: Hanya menghitung metrik jarak lurus (Km), bukan waktu tempuh riil (kemacetan/topografi). | Ikon limitasi (jam pasir / ikon jalan macet). | 1.5 min |
| 9 | Conclusion: Algoritma *Context-Aware* siap diaplikasikan untuk *smart tourism* Semarang. | Teks kesimpulan yang kuat (1 kalimat puncak). | 1 min |

**Total waktu estimasi:** 15 menit

---

## Latihan 2 — Anticipatory Defense

Prediksi 5 pertanyaan yang mungkin diajukan penguji, lalu siapkan jawaban CER.

| # | Kategori | Pertanyaan | Claim | Evidence | Reasoning |
|---|----------|-----------|-------|----------|-----------|
| 1 | *Problem* | Mengapa tidak menggunakan variabel kepuasan pengguna saja alih-alih jarak? | Jarak adalah hambatan fisik absolut bagi wisatawan. | CF standar sering memunculkan RMSE bagus tapi rute rekomendasinya tidak masuk akal (beda ujung kota). | Tanpa filter spasial, rekomendasi seakurat apa pun tidak akan dieksekusi oleh turis karena kendala logistik. |
| 2 | *Method* | Mengapa Anda sangat yakin tidak terjadi *data leakage*? | Metodologi di-*coding* dengan prinsip isolasi K-Fold yang ketat. | Variabel `item_means` (rata-rata rating item) dihitung murni hanya dari indeks *training set*, bukan seluruh data. | Proses normalisasi parameter secara terpisah ini memastikan model benar-benar "buta" terhadap *test set*. |
| 3 | *Results* | Selisih nilai MAE (0.021) terlihat kecil. Apakah ini signifikan secara praktis? | Ya, dampaknya sangat signifikan di dunia nyata. | Uji *Paired t-test* menunjukkan p<0.05 dan *Cohen's d* bervolume besar. | Penurunan *error* kecil pada algoritma agregasi berskala 4.000+ matriks berdampak drastis pada perangkingan (Top-N) yang akan dilihat pengguna. |
| 4 | *Method* | Mengapa Anda tidak menghapus data yang jauh dari pusat kota (*outlier*)? | Data yang tersebar mencerminkan realita pariwisata Semarang. | File CSV menunjukkan 4.362 data utuh (0 *missing values*). | Menghapus destinasi terpencil (*outlier*) justru memanipulasi data riil dan merusak tujuan algoritma *Context-Aware* itu sendiri. |
| 5 | *Limitation* | Apa kelemahan terbesar dari algoritma yang Anda bangun ini? | Tidak mempertimbangkan *real-time traffic* (kemacetan). | Metode menggunakan *Haversine* (jarak melintang udara/lurus). | Di kota bersudut pandang topografi miring seperti Semarang, jarak lurus 2 Km bisa memakan waktu 30 menit jika rutenya menanjak dan macet. |

---

## Latihan 3 — Simulasi Q&A

Minta teman/kolega mengajukan 3 pertanyaan tentang riset Anda. Catat pertanyaan dan evaluasi jawaban Anda.

| # | Pertanyaan | Jawaban Saya | Evaluasi |
|---|-----------|-------------|---------|
| 1 | "Berapa banyak data yang di-*drop* saat *preprocessing*?" | "Nol. Dataset awal terverifikasi 4.362 baris yang sudah lengkap dengan koordinat Lat/Lon, sehingga tidak ada *listwise deletion*." | [x] Direct [x] Data-based [x] Honest |
| 2 | "Mengapa tidak pakai algoritma *Deep Learning* sekalian?" | "Karena riset ini fokus mengukur dampak penambahan *Context-Aware* pada struktur dasar CF (*Baseline*). *Deep Learning* terlalu *black-box* dan rentan *overfitting* untuk ukuran data ini." | [x] Direct [x] Data-based [x] Honest |
| 3 | "Apakah algoritma ini bisa mendeteksi preferensi *backpacker* yang suka jalan jauh?" | "Untuk saat ini belum. Batasan radius geografisnya masih statis. Di *future work*, fitur radius ini harusnya bisa diatur (*toggle*) secara dinamis oleh tipe pengguna." | [x] Direct [x] Data-based [x] Honest |

**Pertanyaan yang paling sulit dijawab:**
> Menjelaskan mengapa selisih skor MAE (0.672 ke 0.651) disebut "signifikan". Terkadang penguji awam mengira perbedaan baru dibilang bagus kalau angkanya turun setengahnya.

**Apa yang perlu disiapkan lebih baik:**
> Berlatih analogi (*practical significance*). Mempersiapkan penjelasan bahasa manusia bahwa dalam sistem rekomendasi, pergeseran persentase desimal (*error rate*) memengaruhi urutan destinasi di layar HP pengguna secara masif.

---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-16 — dari paradigma riset hingga presentasi — bagian mana yang paling mengubah cara Anda berpikir tentang riset? Apa satu hal yang akan selalu Anda terapkan di riset berikutnya?

**Insight terbesar:**
> Bagian yang paling mengubah pola pikir saya adalah pemahaman mengenai **Data Leakage (Kebocoran Data)** dan **Failure Analysis**. Sebelumnya, saya mengira riset komputasi itu sekadar "menulis kode Python, di-*run*, lalu angkanya dimasukkan di laporan". Kini saya paham bahwa setiap langkah *preprocessing*, peletakan indeks *K-Fold*, hingga kejujuran tidak memanipulasi *outlier* adalah inti dari sains yang sebenarnya. Hipotesis yang ditolak pun bukanlah sebuah "kiamat", melainkan temuan *boundary condition* yang valid.

**Yang akan selalu diterapkan:**
> Saya akan selalu menerapkan prinsip **"Writing Method & Results First"** dan **"Pipeline Evaluation Logis"**. Daripada terjebak berbulan-bulan di Bab 1 (Pendahuluan), saya akan selalu fokus memastikan bahwa data riil berhasil di-*crawling*, dibersihkan (tanpa bocor), dan dieksekusi secara matematis terlebih dahulu, barulah menyusun argumen laporannya secara mundur (IMRAD).
