# WS-15: Scientific Writing

> **Bab 15 — Penulisan Ilmiah**

---

## Ringkasan Materi

### Scientific Argument Flow

```
Problem → Gap → RQ → Method → Result → Analysis → Conclusion → Contribution
```

Paper ilmiah adalah **satu argumen utuh** dari masalah ke kontribusi. Setiap node harus terhubung logis ke node sebelum dan sesudahnya.

### Struktur IMRAD

| Section | Peran | Pertanyaan Kunci |
|---------|-------|-----------------|
| **Introduction** | Motivasi + frame | Why is this needed? |
| **Method** | Deskripsi (reproducible) | How was it done? |
| **Results** | Laporan objektif | What was found? |
| **Discussion** | Interpretasi + refleksi | What does it mean? |
| **Conclusion** | Ringkasan + kontribusi | So what? |

### Logical Flow — "Red Thread"

Setiap paragraf menjawab satu pertanyaan dan memicu pertanyaan berikutnya. Alur logis ini harus terasa di tiga level:
1. **Antar-kalimat** dalam paragraf
2. **Antar-paragraf** dalam section
3. **Antar-section** dalam paper

### Internal Consistency

Setiap elemen yang dijanjikan di Introduction harus hadir di Discussion/Conclusion.

**Consistency Matrix:**
```
           Intro  Method  Result  Discuss  Conclude
RQ1          ✓      ✓       ✓       ✓        ✓
RQ2          ✓      ✓       ✓       ✗ ←      ✓
Metrik-X     ✗      ✗       ✓ ←     ✗        ✗
```
**Masalah:** RQ2 dibahas di semua bagian kecuali Discussion. Metrik-X muncul di Result tapi tidak diperkenalkan di Method.

### Writing Quality Triad

| Kualitas | Deskripsi | Contoh Buruk → Baik |
|----------|----------|---------------------|
| **Clarity** | Dipahami sekali baca | "Performa meningkat" → "Accuracy meningkat dari 85.3% ke 89.7%" |
| **Precision** | Istilah eksak, tanpa ambiguitas | "signifikan" → "signifikan secara statistik (p=0.003, d=1.2)" |
| **Conciseness** | Setiap kata menambah informasi | Hapus kalimat redundan, filler words |

### Urutan Penulisan yang Disarankan

1. **Method & Results** — paling stabil, tulis pertama
2. **Discussion** — interpretasi berdasarkan hasil
3. **Introduction** — frame sesuai temuan aktual
4. **Abstract & Conclusion** — terakhir

### Target Jumlah Kata

| Section | Target |
|---------|--------|
| Introduction | 500–700 |
| Related Work | 700–1000 |
| Method | 800–1200 |
| Results | 500–800 |
| Discussion | 600–900 |
| Conclusion | 200–400 |

### Jebakan Kognitif

1. "Lebih panjang = lebih lengkap" → conciseness lebih berharga
2. "Introduction harus ditulis pertama" → justru ditulis terakhir
3. "Jargon teknis = lebih ilmiah" → clarity lebih penting
4. "Discussion = ringkasan Results" → Discussion = interpretasi + konteks

---

## Template A.15 — Paper Structure Checklist

```
PAPER STRUCTURE CHECKLIST

Title   : Peningkatan Akurasi Sistem Rekomendasi Pariwisata Semarang Menggunakan Algoritma *Context-Aware Collaborative Filtering*
Target  : [x] Jurnal  [ ] Konferensi  [x] Laporan

Section Check:
  [x] Abstract — masalah, metode, hasil utama, kontribusi (max 250 kata)
  [x] Introduction — konteks → gap → RQ → kontribusi → struktur paper
  [x] Related Work — concept-centric, gap positioning
  [x] Method — reproducible: desain, variabel, metrik, setup, prosedur
  [x] Results — tabel + grafik + observasi (tanpa interpretasi)
  [x] Discussion — interpretasi, perbandingan, implikasi, limitation
  [x] Conclusion — jawaban RQ, kontribusi, future work

Consistency Matrix:
  [x] RQ di Introduction = RQ di Method = RQ di Conclusion
  [x] Variabel di Method = variabel di Results
  [x] Klaim di Discussion didukung data di Results
  [x] Limitasi di Discussion di-address di Conclusion/Future Work

Writing Quality:
  [x] Clarity — mudah dipahami tanpa re-read
  [x] Precision — tidak ada istilah ambigu
  [x] Conciseness — tidak ada kalimat redundan

```

---

## Latihan 1 — Paper Outline

Buat outline paper untuk riset Anda menggunakan struktur IMRAD.

| Section | Konten Utama (2-3 kalimat) | Target Kata |
|---------|---------------------------|------------|
| Abstract | Konteks: Rekomendasi pariwisata seringkali tidak logis secara jarak tempuh. Studi ini mengintegrasikan filter geospasial pada *Collaborative Filtering* (CF) menggunakan 4.362 ulasan destinasi di Semarang. Hasilnya, algoritma *Context-Aware* sukses menurunkan *error* secara signifikan (MAE 0.651 vs 0.672). | 200-250 |
| Introduction | Konteks: Pentingnya relevansi lokasi dalam UX pariwisata. Gap: CF standar hanya fokus pada kemiripan *rating* dan mengabaikan hambatan jarak fisik. RQ: Apakah integrasi informasi geospasial (*Context-Aware*) mampu meningkatkan akurasi rekomendasi? | 500-700 |
| Related Work | Tinjauan pustaka mengenai limitasi CF konvensional (*sparsity* dan *cold start*). Eksplorasi studi terdahulu terkait *Location-Based Services* (LBS) dan kalkulasi jarak geospasial menggunakan formula *Haversine*. | 700-1000 |
| Method | Desain eksperimen kuantitatif dengan pendekatan komputasional. Pemrosesan matriks *rating* dari 4.362 sampel ulasan riil. Validasi silang menggunakan *5-Fold Cross Validation*, dan penetapan parameter metrik evaluasi MAE serta RMSE. | 800-1200 |
| Results | Penyajian obyektif tabel performa hasil komputasi (5 iterasi K-Fold). Tabel menunjukkan *Context-Aware CF* meraih rata-rata MAE 0.651, sedangkan *Baseline CF* sebesar 0.672. Visualisasi selisih ketimpangan menggunakan *Box Plot*. | 500-800 |
| Discussion | Uji-t berpasangan (*Paired t-test*) mengonfirmasi signifikansi statistik dari perbaikan akurasi. Secara praktis, penurunan nilai *error* ini berdampak pada rute rekomendasi yang lebih masuk akal bagi turis. Pembahasan *limitasi* terkait kepekaan radius jarak di area macet. | 600-900 |
| Conclusion | Rumusan masalah terjawab: penambahan konteks spasial sukses meminimalisasi tingkat *error*. Kontribusi riset memberikan landasan metode baru bagi pengembang aplikasi wisata lokal. Saran eksplorasi *hybrid filtering* di masa depan. | 200-400 |

---

## Latihan 2 — Consistency Matrix

Buat consistency matrix untuk memverifikasi internal consistency paper Anda.

| Elemen Kunci | Intro | Method | Result | Discussion | Conclusion |
|--|-------|--------|--------|-----------|-----------|
| RQ (Efektivitas filter spasial) | ✓ | ✓ | ✓ | ✓ | ✓ |
| Metrik utama (MAE & RMSE) | ✓ | ✓ | ✓ | ✓ | ✓ |
| Variabel IV (Baseline vs Intervensi)| ✓ | ✓ | ✓ | ✓ | ✓ |
| Variabel DV (Tingkat Error) | ✓ | ✓ | ✓ | ✓ | ✓ |
| Dataset (4.362 sampel Semarang) | ✓ | ✓ | ✓ | ✓ | ✓ |
| Klaim kontribusi penurunan error| ✓ | ✓ | ✓ | ✓ | ✓ |

**Isi setiap sel:** ✓ (ada & konsisten), ✗ (missing), ~ (ada tapi inkonsisten)

**Inkonsistensi yang ditemukan:**
> Tidak ada inkonsistensi. Alur *Red Thread* (benang merah) dari awal pengajuan hipotesis hingga pembuktian angka dari *script* Python telah tersambung secara presisi.

**Tindakan perbaikan:**
> Tetap mempertahankan struktur *outline* yang ada saat mem-*(draft)* laporan akhir.

---

## Latihan 3 — Writing Quality Check

Ambil satu paragraf dari tulisan Anda (atau tulis paragraf baru) dan evaluasi kualitasnya.

**Paragraf asli (Contoh draft awal yang buruk):**
> Sistem rekomendasi yang dibuat performanya lumayan bagus dan peningkatannya cukup signifikan. Setelah diuji pakai banyak data yang diekstrak dari peta, *error*-nya lebih kecil dari algoritma yang lama. Jadi sistem ini sangat cocok buat turis yang mau jalan-jalan di Semarang biar jalurnya tidak kejauhan.

| Kriteria | Evaluasi | Perbaikan |
|----------|---------|-----------|
| Clarity | Kalimat ambigu dan informal (contoh: "lumayan bagus", "pakai banyak data", "jalurnya tidak kejauhan"). | Mengganti frasa sehari-hari dengan terminologi akademik yang spesifik. |
| Precision | Tidak ada angka ukur yang eksak. Kata "signifikan" dipakai secara sembarangan tanpa data statistik pendukung. | Memasukkan angka presisi (4.362 data ulasan, nilai MAE, parameter lokasi). |
| Conciseness | Kalimat terlalu bertele-tele dan repetitif. | Memadatkan informasi agar langsung menuju poin hasil komparasi algoritma. |

**Paragraf setelah perbaikan:**
> Integrasi filter geospasial pada algoritma *Collaborative Filtering* terbukti mampu meningkatkan akurasi sistem secara signifikan. Berdasarkan uji komputasi terhadap 4.362 data ulasan wisatawan di Semarang, metode *Context-Aware* berhasil menekan rata-rata tingkat *error* (MAE) menjadi 0.651, mengungguli metode standar yang berada di angka 0.672. Penurunan galat ini secara praktis berdampak pada penyajian rekomendasi destinasi yang lebih rasional dan terjangkau secara jarak bagi wisatawan.

---

## Refleksi

> Apa perbedaan antara menulis "tentang" riset dan menulis sebagai "argumen" riset? Bagaimana urutan penulisan (Method → Discussion → Introduction) mengubah kualitas tulisan?

**Jawaban:**

> Menulis "tentang" riset sekadar melaporkan kronologi langkah-langkah yang saya lakukan di depan komputer (layaknya sebuah buku harian teknis). Sebaliknya, menulis sebagai "argumen" riset berarti saya memosisikan setiap data (seperti nilai evaluasi K-Fold) sebagai bukti logis untuk meyakinkan pembaca bahwa hipotesis saya (filter spasial meningkatkan akurasi) adalah benar. 
> 
> Rekomendasi urutan penulisan (*Method* dan *Results* terlebih dahulu, diikuti *Discussion*, lalu *Introduction* di akhir) sangat merevolusi pola pikir saya. Sebelumnya, saya sering menghabiskan waktu berminggu-minggu *stuck* di bagian Pendahuluan. Dengan menulis bagian hasil metodologinya terlebih dahulu, saya menghindari risiko "terlalu banyak berjanji di awal", karena *Introduction* yang saya susun belakangan dapat langsung disesuaikan secara presisi dengan temuan angka riil yang sudah pasti dan terbukti di lapangan.
