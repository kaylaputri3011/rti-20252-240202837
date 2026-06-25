# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi

### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

**Perbandingan pendekatan Author-centric vs Concept-centric:**

| Aspek | Author-centric (Hindari) | Concept-centric (Gunakan) |
|-------|--------------------------|---------------------------|
| Struktur | Per penulis/paper ("Rahman et al. menyatakan...") | Per konsep/metode ("Pendekatan berbasis transformer") |
| Tujuan | Ringkasan isi paper | Perbandingan metode & identifikasi gap |
| Contoh paragraph | "Rahman (2023) pakai CNN. Lee (2022) pakai LSTM. Zhang (2021) pakai RF." | "Tiga pendekatan dominan: CNN digunakan oleh 4 paper untuk representasi fitur visual; LSTM untuk data sekuensial; RF sebagai baseline klasik." |
| Hasil akhir | Daftar paper | Peta pengetahuan + gap yang teridentifikasi |

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database utama**: IEEE Xplore, ACM DL, Scopus
   - Akses IEEE/ACM melalui jaringan kampus atau VPN institusi
   - Alternatif bebas biaya: Google Scholar, ResearchGate ([researchgate.net](https://www.researchgate.net)), arXiv ([arxiv.org](https://arxiv.org))
2. **Boolean query** yang terdokumentasi eksplisit
   - Contoh: `("anomaly detection" OR "intrusion detection") AND ("deep learning" OR "neural network") NOT ("medical imaging")`
   - Gunakan tanda kutip untuk frasa eksak; AND/OR/NOT mengontrol scope
3. **Snowballing** — dua arah:
   - **Backward snowballing**: buka daftar referensi di paper kunci → telusuri paper yang dikutip
   - **Forward snowballing**: di Google Scholar, klik "Cited by" di bawah paper kunci → temukan paper yang mengutipnya
   - Ulangi 1–2 tingkat untuk membangun cakupan komprehensif
4. Klaim "belum ada penelitian" harus didukung **bukti pencarian**

### Baseline Selection — 3 Kriteria

| Kriteria | Pertanyaan |
|----------|-----------|
| **Relevan** | Apakah menyelesaikan masalah yang sama? |
| **Representatif** | Apakah mewakili common practice? |
| **State-of-the-Art** | Apakah terbaru/terbaik? |

Membandingkan deep learning 2024 dengan decision tree sederhana tanpa justifikasi = **straw man comparison** (perbandingan tidak jujur).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan baca literatur | Mencari solusi yang sudah ada | Memahami apa yang belum terjawab |
| Cara membaca paper | Tutorial, how-to | Metode, limitasi, gap |
| Baseline | Framework terpopuler | State-of-the-art yang rigorous |
| Dokumentasi pencarian | Tidak diperlukan | Wajib (reproducible) |

### Istilah Penting

- **Concept-centric** — Organisasi literatur berdasarkan konsep/metode, bukan per penulis
- **Snowballing** — Backward (telusuri referensi) + Forward (cari yang mengutip paper kunci)
- **Research Position** — Pernyataan eksplisit posisi riset terhadap studi sebelumnya
- **Straw man comparison** — Memilih baseline lemah agar metode sendiri terlihat lebih baik

---

## Template A.3 — Literature Mapping & Gap Identification

```
LITERATURE MAPPING

Topik      : Sistem Rekomendasi Pariwisata Berbasis Collaborative Filtering
Database   : Google Scholar, IEEE Xplore
Query      : "sistem rekomendasi" AND "tempat wisata" AND ("collaborative filtering" OR "sistem pakar")
Tahun      : 2020 - 2023
Hasil awal : 145 paper → Screening → 5 paper final

Literature Matrix (concept-centric):

| Study | Tahun | Method | Data | Result | Limitation |
|-------|-------|--------|------|--------|------------|
| Cholil et al. | 2023 | User-based CF | 315 Rating (Semarang) | MAE 0.85 | Masalah *data sparsity* |
| Pratama et al. | 2022 | Item-based CF | Data Google Maps (Bali) | RMSE 0.92 | *Cold-start problem* pada tempat baru |
| Wijaya & Sari | 2021 | CF + K-Nearest Neighbor | 500 Rating (Yogyakarta) | Akurasi 82% | Tidak memperhitungkan jarak tempuh |
| Kusuma dkk. | 2023 | Hybrid (CF + Content) | Dataset Tripadvisor | RMSE 0.75 | Komputasi terlalu berat untuk *real-time* |
| Santoso | 2020 | CF (Pearson Correlation) | 200 Rating (Bandung) | Presisi 78% | Rating *fake/spam* tidak disaring |

Pola yang ditemukan:
  Metode dominan     : User-based Collaborative Filtering dengan Pearson Correlation.
  Dataset umum       : Data sekunder hasil *crawling* ulasan dari Google Maps atau Tripadvisor.
  Limitasi berulang  : *Cold-start problem* (kesulitan merekomendasikan pengguna baru) dan *Sparsity* (matriks data yang terlalu banyak kosong).
GAP IDENTIFICATION

Gap 1: [Jenis: Method Gap & Data Gap]
  Deskripsi    : Sebagian besar penelitian CF hanya mengandalkan matriks angka rating 1-5, tanpa menginkorporasikan data spasial (lokasi pengguna saat ini).
  Bukti        : Wijaya (2021) dan Santoso (2020) mencatat rekomendasi sering kali tidak logis secara geografis karena merekomendasikan tempat yang terlalu jauh dari lokasi pengguna.
  Signifikansi : Memasukkan variabel *Location-Based Service (LBS)* ke dalam algoritma CF akan membuat sistem dapat digunakan secara *real-time* saat wisatawan sedang di jalan.

Gap 2: [Jenis: Perfomance Gap]
  Deskripsi    : Tingkat akurasi metode CF murni menurun drastis ketika dihadapkan pada tempat wisata yang baru saja buka (*cold-start item*).
  Bukti        : Pratama (2022) dan Cholil (2023) sama-sama mendokumentasikan ketidakmampuan sistem memberikan rekomendasi jika item belum memiliki minimal interaksi rating.
  Signifikansi : Menyelesaikan ini krusial untuk membantu UMKM pariwisata baru agar mendapatkan visibilitas yang setara dengan tempat wisata populer.

Baseline Selection:
| Baseline | Relevansi | Representatif | Source |
|----------|-----------|---------------|--------|
| User-based CF (Pearson) | Sama-sama merekomendasikan wisata. | Sangat representatif (standar mayoritas paper). | Cholil et al., 2023 |
| Item-based CF (Cosine) | Metodologi komparasi klasik dalam CF. | Merupakan *common practice* dalam evaluasi algoritma dasar. | Pratama et al., 2022 |
```

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan database akademik.

> **Panduan pencarian:**
> - Database: IEEE Xplore, ACM DL, Google Scholar, atau ResearchGate
> - Tulis query Boolean yang digunakan: contoh `("object detection" OR "image classification") AND ("edge computing") NOT ("medical")`. Dokumentasikan query secara eksplisit.
> - Akses gratis: buka Google Scholar → cari judul paper → klik [PDF] jika tersedia, atau akses lewat campus VPN

**Topik riset:** Sistem Rekomendasi Pariwisata Berbasis Collaborative Filtering
**Query pencarian:** intitle:"sistem rekomendasi wisata" AND "collaborative filtering"
**Database:** Google Scholar

| # | Study | Tahun | Method | Dataset | Result | Limitasi |
|---|-------|-------|--------|---------|--------|----------|
| 1 | Cholil et al. | 2023 | User-Based CF | Rating dari web reviu (Semarang) | Sistem berfungsi optimal memprediksi rating. | Terbatas pada masalah kelangkaan data (sparsity). |
| 2 | Pratama et al. | 2022 | Item-Based CF | Data crawling Google Maps (Bali) | RMSE 0.92 | Kesulitan pada item baru (cold-start item). |
| 3 | Wijaya & Sari | 2021 | CF + KNN | Kuesioner wisatawan (Yogyakarta) | Akurasi 82% | Mengabaikan konteks cuaca dan jarak fisik. |
| 4 | Kusuma dkk. | 2023 | Hybrid CF | Dataset publik Tripadvisor (Surabaya) | RMSE 0.75 | Kompleksitas komputasi menghambat kinerja real-time. |
| 5 | Santoso | 2020 | CF Klasik | Rating aplikasi lokal (Bandung) | Presisi 78% | Rentan terhadap noise data (rating palsu). |

**Pola yang terlihat — Metode dominan:** Penggunaan CF tradisional (User-based atau Item-based) dengan pengukuran kemiripan berbasis Pearson atau Cosine.
**Limitasi yang berulang:** Ketidakmampuan algoritma beradaptasi dengan pengguna baru (cold-start) dan banyaknya sel kosong dalam matriks data (sparsity).

---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
| Performance Gap | [x] Ya / [ ] Tidak | Penurunan presisi saat matriks data memiliki persentase sparsity di atas 90%. |
| Method Gap | [x] Ya / [ ] Tidak | Jarangnya integrasi antara CF dengan pemrosesan Location-Based Service secara simultan. |
| Data Gap | [x] Ya / [ ] Tidak | Penggunaan data crawling yang tidak memverifikasi apakah pemberi rating benar-benar mengunjungi lokasi. |
| Context Gap | [x] Ya / [ ] Tidak | Sistem tidak mempertimbangkan konteks temporal (jam buka, siang/malam, musim hujan/kemarau). |

**Gap utama yang dipilih:** Context Gap + Method Gap (Pengembangan Collaborative Filtering dengan pembobotan Context-Aware berbasis Waktu dan Lokasi).
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
> Karena di dunia nyata, preferensi wisata sangat bergantung pada konteks saat itu. Menggunakan matriks statis (rating historis saja) berisiko menghasilkan rekomendasi absurd—misalnya sistem merekomendasikan "Taman Bunga" dengan akurasi tinggi pada pukul 9 malam saat sedang hujan badai. Menambahkan variabel ini akan menjembatani jurang antara keandalan matematis dengan kegunaan praktis di lapangan.

---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
| 1 | User-Based CF | Menyelesaikan tugas prediksi nilai rating user ke tempat wisata target. | Merupakan gold standard tradisional yang paling sering dijadikan tolok ukur. | Bukan SOTA terbaru, namun fondasi dasar. | Cholil et al. (2023) |
| 2 | Hybrid CF | Mengombinasikan pendekatan CF untuk mencoba mengatasi cold-start problem. | Mewakili praktik pengembangan metode rekomendasi level menengah. | Ya, untuk level implementasi konvensional. | Kusuma dkk. (2023) |

**Apakah pemilihan baseline ini bisa dianggap straw man?** [ ] Ya / [x] Tidak
> Justifikasi: Baseline yang dipilih adalah metode common practice yang diterbitkan dalam 3 tahun terakhir dan digunakan di domain yang identik (pariwisata lokal di Indonesia). Kita tidak membandingkan metode CF canggih (2024) dengan algoritma random guess murni. Membandingkan algoritma kita nanti dengan User-Based CF standar (Cholil et al.) adalah perbandingan apple-to-apple untuk membuktikan apakah modifikasi (novelty) kita benar-benar memberikan peningkatan performa atau tidak.
---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> Klaim "belum ada yang meneliti ini" sering kali bermula dari kemalasan peneliti mencari literatur secara mendalam, dan hal yang belum diteliti belum tentu berguna (bisa jadi memang tidak relevan). Sementara itu, research gap yang valid adalah argumen terstruktur yang mengakui keberadaan penelitian sebelumnya, namun menunjukkan batasan eksplisit dari penelitian tersebut (limitation).
> Cara membuktikan sebuah gap benar-benar ada adalah melalui Literature Mapping (seperti matriks di atas). Bukti dihadirkan dengan cara mensitasi secara langsung kalimat pada bagian Limitation atau Future Work dari paper state-of-the-art, yang secara tertulis menyatakan bahwa "metode ini memiliki kelemahan X" atau "penelitian masa depan harus mengakomodasi variabel Y." Bukti gap bersumber dari data historis penelitian, bukan sekadar opini subjektif penulis proposal.
