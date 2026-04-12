# WS-01: Distorsi & Paradigma

> **Bab 1 — Research Mindset in IT**

---

## Ringkasan Materi

### Research Trust Model

Pengetahuan ilmiah tidak muncul langsung dari kenyataan. Ia melewati **6 tahap transformasi** yang masing-masing rawan distorsi:

```
Reality → Data → Processing → Analysis → Inference → Knowledge
```

Etika mencegah distorsi yang disengaja (fabrikasi, cherry-picking). Validitas mendeteksi distorsi yang tidak disengaja (confounding variable, sampling bias).

### Tiga Jenis Validitas

| Jenis | Pertanyaan | Contoh Ancaman |
|-------|-----------|----------------|
| **Internal Validity** | Apakah hubungan kausal benar ada? | Confounding variable |
| **External Validity** | Apakah bisa digeneralisasi? | Dataset terlalu homogen |
| **Construct Validity** | Apakah mengukur hal yang benar? | Metrik tidak sesuai klaim |

### Paradigma Riset

Mata kuliah ini menggunakan pendekatan **Positivist** (fenomena TI bisa diukur objektif melalui eksperimen terkontrol) diperkuat **Design Science Research** (artefak dibuat sebagai instrumen pengujian hipotesis, bukan tujuan akhir).

### Mode Berpikir Peneliti

**Curious** (mempertanyakan fenomena) → **Critical** (mengevaluasi klaim berdasarkan bukti) → **Systematic** (merancang investigasi terstruktur dan reproducible).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Membuat sistem yang bekerja | Menghasilkan pengetahuan yang valid |
| Pertanyaan khas | "Bagaimana membuatnya jalan?" | "Apakah klaim ini benar?" |
| Ukuran sukses | Sistem berfungsi, client puas | Hipotesis terjawab, temuan tervalidasi |
| Kegagalan | Harus dihindari | Harus dilaporkan (negative result = kontribusi) |

### Istilah Penting

- **Research Mindset** — Pola pikir yang menuntut bukti dan mempertanyakan asumsi
- **Research Ethics** — Prinsip perilaku: kejujuran, objektivitas, keterbukaan, akuntabilitas
- **HARKing** — Hypothesizing After Results are Known — merumuskan hipotesis setelah melihat data
- **Falsifiability** — Hipotesis harus bisa dibuktikan salah

---

## Template A.1 — Research Mindset Self-Assessment

```
Nama Peneliti    : Kayla Putri Arsonisr
Tanggal          : 12 April 2026

1. Ketika membaca klaim "Metode Collaborative Filtering memiliki akurasi prediksi 90%":
   - Pertanyaan pertama saya: Apakah akurasi ini dapat diukur dari pengguna aktif yang telah memberikan banyak ulasan? Selain itu, bagaimana algoritma berfungsi saat berhadapan dengan pengguna baru (masalah pembukaan dingin)?
   - Data yang dibutuhkan untuk verifikasi: Dataset mentah dari matriks penilaian item pengguna, skenario pembagian data (train/test split), dan metrik evaluasi seperti MAE atau RMSE.

2. Posisi paradigma:
   - Pendekatan: [x] Positivis  [ ] Interpretivis  [ ] Design Science  [ ] Mixed
   - Alasan: Studi ini menguji fenomena yang objektif dan terukur, yaitu mengevaluasi tingkat *error* numerik (RMSE) algoritma komputasi untuk memprediksi ketertarikan pengguna dengan data kuantitatif.

3. Identifikasi distorsi:
   - Asumsi tersembunyi: Berasumsi bahwa skor pengguna, yang terdiri dari 1-5 bintang, hanya menunjukkan kualitas tempat wisata.
   - Sumber bias potensial: *Self-selection bias*—hanya wisatawan yang sangat puas (bintang 5) atau sangat kecewa (bintang 1) yang mau repot-repot memberikan rating, sementara pengguna netral jarang mengumpulkan datanya.
   - Langkah mitigasi: Untuk memastikan konteks rating valid, gabungkan data kuantitatif (rating) dengan analisis sentimen dari ulasan teks.

4. Komitmen etika:
   - Data yang tidak akan dimanipulasi: Mempertahankan "titik data" pengguna yang pola penilaiannya aneh atau sulit diprediksi oleh algoritma daripada menghapusnya agar nilai RMSE terlihat kecil atau bagus.
   - Batasan yang diakui sejak awal: Algorithm hanya memperkirakan preferensi berdasarkan kedekatan pengguna, bukan kualitas fasilitas tempat wisata.
```

---

## Latihan 1 — Identifikasi Distorsi

Pilih satu paper riset di bidang TI yang mengklaim "metode X meningkatkan performa." Telusuri setiap tahap Research Trust Model.

**Paper yang dipilih:**
> Judul: Sistem Rekomendasi Tempat Wisata Di Kota Semarang Menggunakan Metode Collaborative Filtering
> Penulis (Tahun): S. R. Cholil, N. A. Rizki, T. F. Hanifah (2023)

| Tahap | Apa yang Dilakukan | Potensi Distorsi |
|-------|-------------------|-----------------|
| **Reality → Data** | Mengumpulkan data tentang peringkat lokasi wisata yang diberikan oleh pengguna platform ulasan online. | Pelanggan memberikan rating tinggi karena lokasi wisatanya gratis atau murah, bukan karena mereka benar-benar merekomendasikan kualitas lokasinya, yang dikenal sebagai rating bias. |
| **Data → Processing** | Memfilter data sparse, atau kosong, dan menghapus pengguna dengan hanya 1 atau 2 ulasan. | Kehilangan informasi berharga; sistem rekomendasi mungkin menghilangkan tempat wisata baru yang tidak populer. |
| **Processing → Analysis** | Untuk menghitung kemiripan, atau kemiripan, antara pengguna, gunakan metode jarak statistik. | Cherry-picking: Hanya melaporkan hasil uji coba menggunakan rumus similarity yang paling menguntungkan nilai akurasi (misalnya, korelasi Pearson). |
| **Analysis → Inference** | Perlu diingat bahwa sistem ini sangat efektif dalam merekomendasikan wisata. | Konstruksi validitas ancaman: Metrik yang diukur (RMSE) hanya membuktikan algoritma "menebak angka rating" yang mahir, bukan membuktikan bahwa wisatawan pasti akan pergi. |
| **Inference → Knowledge** | Mengklaim bahwa pengaturan kolaboratif adalah cara terbaik untuk merekomendasikan pariwisata. | Masalah validitas luar: sistem ini mungkin akurat untuk demografi turis di Semarang, tetapi bisa gagal total di Bali, dengan pola turis yang sangat berbeda. |

**Distorsi paling besar di tahap:** ________________________

**Dua distorsi spesifik yang teridentifikasi:**
1. Menganggap keberhasilan prediksi angka (rating) sama dengan kemungkinan kunjungan sebenarnya terjadi.
2.  Mengurangi interaksi pengguna atau item saat pemrosesan data, yang menghilangkan kelemahan utama metode ini (masalah awal dingin).

---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

| Perspektif | Analisis |
|------------|---------|
| **Kejujuran ilmiah** | Agar hipotesis dapat dibuktikan, hasil eksperimen harus menunjukkan kondisi data yang sebenarnya, bukan kondisi buatan. Bentuk manipulasi data adalah penghapusan outlier yang tidak memiliki dasar teori. |
| **Transparansi** | Peneliti harus mengungkapkan kondisi metrik evaluasi dengan dan tanpa outlier. Mereka juga harus memberikan penjelasan yang mendalam tentang fitur tiga data dan alasan logis mengapa mereka dianggap outlier. |
| **Peer review** | Ini memungkinkan pakar lain untuk memastikan apakah ketiga data tersebut hanyalah kesalahan input teknis yang harus diperbaiki atau pola perilaku pengguna baru yang perlu diteliti. |

**Keputusan akhir dan justifikasi:**
> Memasukkan outlier ke dalam analisis dan melaporkan hasil negatif atau tidak signifikan. Anomali data sering kali menunjukkan dinamika dunia nyata dalam sistem rekomendasi machine learning. Sistem akan terlihat bagus di atas kertas, tetapi dapat gagal beradaptasi saat dipublikasikan ke publik jika hasilnya dipaksa menjadi "signifikan" secara statistik.

---

## Latihan 3 — Posisi Paradigma

**Topik riset:** Evaluasi Akurasi Prediksi Rating pada Sistem Rekomendasi Tempat Wisata Menggunakan Pendekatan Collaborative Filtering.

| Kriteria | Positivis | Interpretivis | Design Science |
|----------|-----------|---------------|----------------|
| **Kesesuaian dengan topik (1–5)** | **5 (Sangat Cocok)** | 1 | 3 |
| **Jenis data yang dikumpulkan** | Precision/Recall, nilai tingkat kesalahan (RMSE, MAE), dan penilaian data numerik matriks. | Hasil wawancara serta perasaan dan pengalaman subjektif wisatawan. | Kode algoritma, arsitektur software, dan protokol UI/UX sistem rekomendasi. |
| **Limitasi paradigma** | Fokus hanya pada angka statistik dan abaikan alasan psikologis pelanggan untuk menyukai lokasi tertentu. | Sangat subjektif, dan sampelnya terlalu kecil untuk melatih pembelajaran mesin atau *machine learning*. | Fokus mungkin dialihkan ke rekayasa interface aplikasi daripada kinerja inti algoritma. |

**Paradigma yang dipilih:** Positivis
**Alasan:** Pengujian hipotesis deduktif biasanya digunakan dalam penelitian tentang pengajaran mesin dan analitik data (seperti prediksi peringkat). Tujuannya adalah untuk mengetahui secara matematis dan seobjektif mungkin seberapa dekat hasil prediksi algoritma dengan data historis sebenarnya dalam lingkungan eksperimen yang terkontrol.

---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sebelum ini, saya sering menyamakan "akurasi tinggi di atas kertas" dengan "sistem pasti bekerja sempurna di dunia nyata". Setelah memahami rantai distorsi, pertanyaan paling penting yang akan saya ajukan saat meninjau kertas algoritma adalah: "Apakah dataset yang digunakan untuk mendapatkan akurasi 95% tersebut sudah mewakili seluruh skenario buruk di lapangan (misalnya, data bolong, pengguna iseng, mulai dingin), ataukah datanya sudah "dibersihkan" (cherry-picked) berlebihan agar performa algoritma terlihat menjanjikan?"