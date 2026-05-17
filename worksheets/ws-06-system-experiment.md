# WS-06: System-Experiment Mapping

> **Bab 6 — System Design sebagai Experimental Artifact**

---

## Ringkasan Materi

### Sistem = Instrumen Pengujian, Bukan Produk

Seorang engineer bertanya "apakah sistem bekerja?" — seorang peneliti bertanya "apa yang bisa dibuktikan sistem ini?" Sistem dalam riset adalah **artifact** — objek yang sengaja dibuat untuk menguji klaim spesifik.

### System as Experiment Model

```
RQ → Variable → System Component → Experimental Setup → Output
```

Setiap komponen sistem harus bisa ditelusuri ke variabel riset (top-down), dan setiap pengukuran harus menjawab RQ (bottom-up).

### Mapping Variabel ke Komponen

| Tipe Variabel | Peran di Sistem | Contoh |
|---------------|----------------|--------|
| **IV** (Independent) | Modul yang bisa di-toggle/swap | Algoritma A vs B |
| **DV** (Dependent) | Modul pengukuran | Logger, metrics collector |
| **CV** (Control) | Config yang dikunci | Dataset, parameter tetap |

Jika variabel tidak bisa di-map ke komponen apapun → arsitektur perlu didesain ulang.

### 4 Prinsip Desain Eksperimental

| Prinsip | Pertanyaan Kunci |
|---------|-----------------|
| **Traceability** | Komponen ini melayani variabel yang mana? |
| **Modularity** | Bisakah IV diubah tanpa memengaruhi yang lain? |
| **Controllability** | Apakah CV dieksternalisasi ke config file? |
| **Measurability** | Apakah sistem otomatis menghasilkan data yang dibutuhkan? |

### Variable Isolation melalui Arsitektur

- **Modular architecture** — Pisahkan berdasarkan variabel
- **Configuration-driven** — Ubah config (YAML/JSON), bukan code
- **Feature toggles** — On/off flag untuk ablation study

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan sistem | Memenuhi kebutuhan user | Menguji hipotesis, menghasilkan bukti |
| Arsitektur | Optimasi performa & skalabilitas | Optimasi isolasi variabel & reprodusibilitas |
| Konfigurasi | Sering hardcoded | Dieksternalisasi ke config file |
| Fitur tambahan | Menambah nilai user | Menambah noise jika tidak terkait RQ |

### Istilah Penting

- **Artifact** — Objek yang sengaja dibuat untuk memecahkan masalah atau menguji proposisi
- **Traceability** — Kemampuan menelusuri hubungan RQ → variabel → komponen → output
- **Variable Isolation** — Mengubah hanya satu variabel sambil menahan yang lain konstan
- **Ablation Study** — Menguji kontribusi tiap komponen dengan melepasnya satu per satu
- **Configuration-driven Execution** — Semua parameter di config file, bukan hardcoded

---

## Template A.6 — Mapping RQ ke Arsitektur Sistem

```
SYSTEM-EXPERIMENT MAPPING

Research Question: Sejauh mana integrasi variabel Context-Aware (jarak dan waktu) pada algoritma User-Based Collaborative Filtering mampu menghasilkan skor Mean Absolute Error (MAE) yang lebih rendah dibandingkan performa User-Based CF standar milik Cholil dkk. (2023) pada dataset rating pariwisata Semarang?
```
Variable → Component Mapping:

| Variabel | Tipe | Komponen Sistem | Cara Manipulasi/Pengukuran |
| :--- | :--- | :--- | :--- |
| Algoritma Context-Aware | IV | `Recommendation Engine` (Modul Algoritma) | Diubah melalui flag di file `config.yaml` (`enable_context: true/false`). |
| Nilai Akurasi (MAE) | DV | `Evaluation Metric Logger` (Modul Evaluasi) | Skrip otomatis membandingkan matriks *output* dengan matriks data uji (*test set*) dan menyimpan skor MAE ke file CSV. |
| Dataset & Split | CV | `Data Loader & Preprocessor` (Modul Data) | Membaca file CSV statis yang sama dan menggunakan `random_seed` konstan untuk membagi data K-Fold agar iterasi selalu identik. |

```
4 Prinsip Desain:
  [x] Traceability — Setiap komponen bisa ditelusuri ke variabel
  [x] Variable Isolation — IV bisa diubah tanpa mengubah CV
  [x] Measurement Integration — Pengukuran DV built-in
  [x] Reproducibility — Setup bisa direkonstruksi
Experimental Setup:
  Input data     : Dataset interaksi wisatawan Semarang (rating, timestamp, latitude, longitude target & user).
  Parameter      : `k_neighbors=20`, `distance_threshold=10km`, `k_fold=5`.
  Output format  : File `.csv` berisi log eksperimen (Epoch, Algoritma, MAE Score, RMSE Score, Waktu Eksekusi).

```

---

## Latihan 1 — Variable-to-Component Mapping

Gunakan RQ dan variabel dari WS-05. Petakan ke komponen sistem.

**RQ:** Sejauh mana integrasi variabel Context-Aware (jarak dan waktu) pada algoritma User-Based Collaborative Filtering mampu menghasilkan skor Mean Absolute Error (MAE) yang lebih rendah dibandingkan performa User-Based CF standar pada dataset rating pariwisata Semarang?

| Variabel | Tipe | Komponen Sistem | Cara Manipulasi / Pengukuran |
|----------|------|-----------------|---------------------------|
| Metode Rekomendasi | IV | *Modul Filtering (Tukar CF Standar ↔ CF Context-Aware) * | Mengubah routing eksekusi fungsi algoritma melalui parameter konfigurasi sebelum script dijalankan. |
| Error Rate (MAE) | DV | *Modul Evaluator* | Mengkalkulasi nilai absolut dari (prediksi - aktual) dan menyimpannya di file log. |
| Data Lingkungan Uji | CV | Modul Dataset Splitter | Mengunci nilai K-Fold dan menggunakan pembagian train/test set yang identik pada kedua algoritma. |

**Apakah semua variabel bisa di-map?** [x] Ya / [ ] Tidak
> Jika tidak, komponen apa yang perlu ditambahkan? -
> (Sistem sudah memisahkan antara penyuplai data, pemroses data, dan penilai data).

---

## Latihan 2 — 4 Prinsip Desain

Evaluasi desain sistem terhadap 4 prinsip.

| Prinsip | Status | Bukti / Penjelasan |
|---------|--------|-------------------|
| Traceability | ✅ | Sangat jelas. Recommendation Engine murni mewakili IV, Evaluator murni mewakili DV. Tidak ada modul yang melayani fungsi ganda secara rancu. |
| Modularity | ✅ | Algoritma Context-Aware dan CF Standar diletakkan di file/class Python yang berbeda. Modul Data Loader tidak peduli algoritma mana yang memanggilnya. |
| Controllability | ✅ | Semua hyperparameter (N-neighbors, ambang batas jarak, rasio split data) diatur secara terpusat melalui satu file config.yaml. Tidak ada nilai hardcoded di dalam logika kode. |
| Measurability | ✅ | Sistem secara otomatis mencetak hasil MAE di terminal dan menambahkannya (append) ke file CSV di folder /results setiap kali eksekusi selesai. |

**Prinsip mana yang paling sulit dipenuhi?** 
> Controllability

**Strategi untuk mengatasinya:**
> Godaan terbesar saat coding adalah melakukan hardcode nilai variabel di tengah-tengah fungsi agar program cepat berjalan. Strateginya adalah menggunakan kerangka eksperimen (seperti Hydra di Python) agar sistem menolak untuk dieksekusi jika parameter eksperimen di file konfigurasi belum terdefinisi secara lengkap.

---

## Latihan 3 — Ablation Study Planning

Jika sistem memiliki 3 komponen utama, rencanakan ablation study.

| Kondisi | Komponen A | Komponen B | Komponen C | Hasil yang Diharapkan |
|---------|-----------|-----------|-----------|----------------------|
| Full (Proposed) | ✅ Aktif | ✅ Aktif | ✅ Aktif | MAE Paling Rendah (Performa terbaik/ Skenario riil) |
| – B ( Tanpa Jarak) | ✅ Aktif | ❌ Mati (Bypass jarak) | ✅ Aktif | Membuktikan seberapa besar pengaruh variabel lokasi terhadap akurasi sistem. |
| – C (Tanpa Waktu) | ✅ Aktif | ✅ Aktif | ❌ Mati (Bypass waktu) | Membuktikan seberapa besar pengaruh variabel jam buka terhadap akurasi sistem. |
| – B dan C (Baselin) | ✅ Aktif | ❌ Mati | ❌ Mati | Berperilaku persis seperti User-Based CF tradisional (algoritma paper Cholil dkk). |

**Komponen mana yang diprediksi paling berkontribusi?** 
> Komponen B (Spatial/Jarak Filter).

**Mengapa?**
> Secara logika domain pariwisata, preferensi jarak (kemacetan, lokasi hotel ke tempat wisata) adalah batasan mutlak (hard constraint). Seorang wisatawan di Semarang Bawah sangat kecil kemungkinannya akan mengunjungi rekomendasi wisata di area Bandungan (Semarang Atas/Kab. Semarang) jika waktunya mepet, sebaik apa pun rating tempat tersebut. Oleh karena itu, memfilter rekomendasi berdasarkan geolokasi akan memangkas banyak error prediksi.

---

## Refleksi

> Apa risiko jika sistem dibangun seperti produk (monolitik, fitur lengkap) lalu baru dilakukan eksperimen? Mengapa arsitektur modular penting untuk riset?

**Jawaban:**
> Membangun sistem riset seperti produk komersial (monolithic) sangat berbahaya karena akan menghasilkan Confounding Variables (variabel perancu). Misalnya, kita membuat aplikasi mobile pariwisata yang lengkap dengan caching memori, optimasi query database, dan UI yang cantik, lalu kita ukur kecepatan responsnya untuk membuktikan algoritma kita "lebih efisien". Kita tidak akan tahu apakah performa tersebut berasal dari kehebatan matematika algoritma kita (IV yang sah), atau murni karena teknologi caching database-nya.
> Arsitektur modular mutlak diperlukan dalam riset untuk mengisolasi variabel. Dengan modul yang terpisah, kita mematikan segala fitur yang tidak relevan dengan hipotesis (UI, database server, network) dan hanya membandingkan logika komputasi A melawan logika komputasi B secara adil. Sistem dalam riset adalah instrumen pengukur, bukan alat untuk memuaskan pengguna akhir.
