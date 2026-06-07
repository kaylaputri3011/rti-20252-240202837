# WS-09: Implementation & Environment

> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**

---

## Ringkasan Materi

### Implementasi Riset ≠ Coding Biasa

Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.

### Reproducible Implementation Model

```
Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result
```

Setiap transisi memiliki syarat:
- Design → Implementation: kode sesuai mapping variabel-ke-komponen
- Implementation → Environment: versi, dependency, seed, path, OS eksplisit
- Environment → Consistency: seed terkunci, urutan deterministik
- Consistency → Reproducibility: dokumentasi lengkap
- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa

### Repeatability vs Reproducibility

| Level | Peneliti | Environment | Hasil |
|-------|---------|-------------|-------|
| **Repeatability** | Sama | Sama | Sama persis |
| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |

Capai **repeatability** dulu, baru **reproducibility**.

### Engineering vs Research Perspective

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |
| Dependency | Update ke terbaru | Lock di versi spesifik |
| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |
| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |
| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |

### Jebakan Kognitif

1. Menunda environment setup → bug sulit dilacak
2. Tidak pakai version control → hasil tidak bisa direkonstruksi
3. Menolak Docker/container → "di laptop saya bisa" saat review
4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)

### Istilah Penting

- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed
- **Dependency** — Komponen eksternal yang harus di-lock versinya
- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode

---

## Template A.9 — Dokumentasi Setup Eksperimen

```
EXPERIMENT SETUP DOCUMENTATION

Hardware:
  CPU     : AMD Ryzen 5 7535HS with Radeon Graphics (3.30 GHz)
  RAM     : 8,00 GB (7,21 GB usable)
  GPU     : AMD Radeon RX 6550M (4 GB)
            AMD Radeon(TM) 660M (483 MB)
  Storage : 349 GB of 477 GB used

Software:
  OS        : Windows 11 Pro
  Runtime   : Python 3.10.12
  Framework : Scikit-learn

  ```


Dependencies:
| Library | Version | Sumber | Hash/Checksum |
|---------|---------|--------|---------------|
|    pandas     |   2.1.0      |    PyPI    |       (otomatis via pip)        |
|   numpy      |   1.26.0      |    PyPI    |     (otomatis via pip)         |
|  scikit-learn  |    1.3.0   |     PyPI    |     (otomatis via pip)     |
|    haversine    |    2.8.0   |   PyPI    |     (otomatis via pip)    |
|    pyyaml    |     6.0.1    |    PyPI    |     (otomatis via pip)     |


```

Konfigurasi:
  Config file     : config.yaml
  Random seed     : 42
  Hyperparameters : K_neighbors=20, max_radius_km=10

Reproducibility Check:
  [x] Dependency terdokumentasi (requirements.txt / lock file)
  [x] Seed ditetapkan di semua level (Python, NumPy, framework)
  [x] Config di version control
  [x] README instruksi reproduksi lengkap
```

---

## Latihan 1 — Environment Specification

Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).

| Komponen | Spesifikasi |
|----------|------------|
| CPU | AMD Ryzen 5 7535HS with Radeon Graphics (3.30 GHz) |
| RAM | 8,00 GB (7,21 GB usable) |
| GPU | AMD Radeon RX 6550M (4 GB)
AMD Radeon(TM) 660M (483 MB) |
| OS | Windows 11 Pro |
| Runtime | Python 3.10.12 |
| Framework | Scikit-learn |
| Random Seed | 42 |

**Dependencies (minimal 5):**

| Library | Version | Alasan Dibutuhkan |
|---------|---------|-------------------|
| pandas | 2.1.0 | Manipulasi dataset dari file CSV, pembersihan data kosong. |
| numpy | 1.26.0 | Kalkulasi operasi matriks berkecepatan tinggi untuk perhitungan rating. |
| scikit-learn | 1.3.0 | Membagi data latih/uji dengan K-Fold dan menghitung metrik MAE/RMSE. |
| haversine | 2.8.0 | Mengkalkulasi jarak geospasial aktual (dalam KM) antara koordinat wisatawan dan destinasi. |
| pyyaml | 6.0.1 | Memisahkan parameter pengaturan (seperti batas K) ke luar kode agar terhindar dari hardcoding. |

---

## Latihan 2 — Repeatability Test Plan

Rancang tes repeatability sederhana: jalankan kode yang sama 3× di environment yang sama.

| Run | Seed | Metrik Utama | Hasil Sama? |
|-----|------|-------------|-------------|
| 1 | 42 | Skor MAE | — |
| 2 | 42 | Skor MAE | [x] Ya / [ ] Tidak |
| 3 | 42 | Skor MAE | [x] Ya / [ ] Tidak |

**Jika hasil berbeda, kemungkinan penyebab:**
> Lupa menetapkan random_state=42 pada fungsi K-Fold split, atau menggunakan tipe data set / dictionary bawaan Python yang urutan iterasinya bisa berubah-ubah setiap kali script dijalankan. Bisa juga karena data baru tidak sengaja ter-load jika API ditarik secara real-time alih-alih membaca dari CSV lokal.

**Checklist kontrol yang sudah diterapkan:**
- [x] Random seed di-set di semua level
- [x] Tidak ada background process yang mengganggu
- [x] Cache dibersihkan antar-run
- [x] Config file yang sama untuk semua run

---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen: Eksperimen Evaluasi Akurasi Context-Aware CF Pariwisata Semarang

## 1. Environment
> OS: Windows 11 Home
Runtime: Python 3.10.12
Hardware: Laptop MSI Bravo 15 B7E (AMD Ryzen 5, RAM 16GB DDR5).

## 2. Installation
> `pip install -r requirements.txt`

## 3. Data
> File `master_wisata_semarang.csv` (berada di folder `/data`). 

## 4. Execution
> Eksekusi pengujian komparatif dengan menjalankan perintah:
`python src/run_experiment.py --config config.yaml`

## 5. Configuration
> Eksperimen diatur melalui `config.yaml`. Parameter kunci yang dipakai:
- random_seed: 42
- k_folds: 5
- neighbors_k: 20
- distance_threshold_km: 10

## 6. Expected Output
> Terminal akan menampilkan progress bar K-Fold. Setelah selesai, program akan menghasilkan file `results/evaluation_metrics.csv` yang memuat tabel komparasi skor MAE dan RMSE antara Baseline (Standard CF) dan Intervensi (Context-Aware CF).
```

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?

**Level saat ini:** [x] Repeatability / [ ] Reproducibility / [ ] Belum keduanya
**Komponen yang belum terdokumentasi:**
> Penggunaan virtual environment (venv). Saat ini script masih berjalan lancar di komputer sendiri (repeatable), tapi rawan error versi library jika dijalankan di komputer orang lain karena file requirements.txt belum di-generate secara bersih dan masih tercampur dengan library dari mata kuliah/proyek Python lainnya.
