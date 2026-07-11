# 06-output

Folder ini berisi hasil eksperimen: tabel dan visualisasi.

---

## Struktur

```
06-output/
├── tables/                       # Tabel hasil eksperimen (CSV)
│   ├── experiment_results.csv    # MAE/RMSE per fold
│   ├── aggregate_results.csv     # Mean ± std
│   ├── statistical_tests.csv     # Paired T-Test results
│   └── error_by_distance.csv     # Analisis tambahan
├── figures/                      # Visualisasi (PNG, 300 DPI)
│   ├── boxplot_mae_comparison.png
│   ├── improvement_per_fold.png
│   └── scatter_pred_vs_actual_fold1.png
└── README.md                     # Dokumentasi ini
```

---

## Tabel Hasil Eksperimen

### 1. experiment_results.csv

**Deskripsi:** MAE dan RMSE untuk setiap fold (5 fold × 2 algoritma)

**Columns:**
```
fold          : int     (1-5)
algorithm     : string  ('baseline' | 'context_aware')
mae           : float   (Mean Absolute Error)
rmse          : float   (Root Mean Square Error)
n_predictions : int     (jumlah prediksi di fold ini)
```

**Sample:**
```csv
fold,algorithm,mae,rmse,n_predictions
1,baseline,0.6720,0.8897,872
1,context_aware,0.6487,0.8634,872
2,baseline,0.6750,0.8923,872
2,context_aware,0.6534,0.8701,872
...
```

### 2. aggregate_results.csv

**Deskripsi:** Agregasi hasil (mean ± std) untuk kedua algoritma

**Columns:**
```
algorithm     : string
mae_mean      : float
mae_std       : float
rmse_mean     : float
rmse_std      : float
improvement   : float  (% improvement vs baseline, hanya untuk context_aware)
```

**Sample:**
```csv
algorithm,mae_mean,mae_std,rmse_mean,rmse_std,improvement
baseline,0.6720,0.0025,0.8896,0.0022,0.0
context_aware,0.6511,0.0021,0.8651,0.0040,3.11
```

### 3. statistical_tests.csv

**Deskripsi:** Hasil uji statistik Paired T-Test

**Columns:**
```
metric        : string  ('mae' | 'rmse')
t_statistic   : float
p_value       : float
significant   : bool    (p < 0.05)
cohens_d      : float   (effect size)
interpretation: string  ('small' | 'medium' | 'large' | 'very large')
```

**Sample:**
```csv
metric,t_statistic,p_value,significant,cohens_d,interpretation
mae,18.7234,0.000067,True,8.37,very large
rmse,15.3421,0.000134,True,7.21,very large
```

### 4. error_by_distance.csv

**Deskripsi:** Analisis error berdasarkan jarak geografis user-item

**Columns:**
```
distance_bin  : string  ('near' | 'medium' | 'far')
distance_range: string  ('<5 km' | '5-10 km' | '>10 km')
baseline_mae  : float
context_mae   : float
improvement   : float   (%)
n_samples     : int
```

**Sample:**
```csv
distance_bin,distance_range,baseline_mae,context_mae,improvement,n_samples
near,<5 km,0.6543,0.6289,3.88,2341
medium,5-10 km,0.6812,0.6587,3.30,1578
far,>10 km,0.7234,0.7198,0.50,443
```

---

## Visualisasi

### 1. boxplot_mae_comparison.png

**Deskripsi:** Boxplot perbandingan distribusi MAE untuk Baseline vs Context-Aware CF (5 fold)

**Insight:**
- Context-Aware CF memiliki median MAE lebih rendah
- Variance lebih kecil (lebih stabil)
- Tidak ada outlier di kedua algoritma

**Ukuran:** 1920×1440 pixels, 300 DPI (print quality)

### 2. improvement_per_fold.png

**Deskripsi:** Bar chart persentase perbaikan MAE per fold

**Insight:**
- Perbaikan konsisten di semua 5 fold (2.82% - 3.47%)
- Rata-rata improvement: 3.11%
- Standar deviasi rendah: perbaikan stabil

**Ukuran:** 2400×1440 pixels, 300 DPI

### 3. scatter_pred_vs_actual_fold1.png

**Deskripsi:** Scatter plot predicted vs actual rating untuk Fold 1 (2 panel: Baseline vs Context-Aware)

**Insight:**
- Context-Aware CF memiliki poin lebih dekat ke diagonal (perfect prediction)
- Baseline CF memiliki dispersi lebih besar (error lebih tinggi)
- Kedua algoritma sedikit underestimate rating tinggi (5★)

**Ukuran:** 3360×1440 pixels (2 panel), 300 DPI

---

## Cara Regenerasi

Jika ingin meregenerasi tabel dan figure:

```bash
cd ../05-kode/notebooks
jupyter notebook 04_analysis.ipynb
```

Atau via script:

```python
from src.analysis import generate_all_outputs

# Baca hasil eksperimen
results = pd.read_json('../06-output/results/experiment_results.json')

# Generate semua tabel dan figure
generate_all_outputs(
    results=results,
    output_dir='../06-output/',
    dpi=300  # High-resolution untuk paper
)
```

---

## Interpretasi Hasil

### Temuan Utama

1. **Context-Aware CF Lebih Akurat:**
   - MAE turun dari 0.6720 → 0.6511 (penurunan 3.11%)
   - Signifikan dengan p < 0.001 (Paired T-Test)

2. **Effect Size Sangat Besar:**
   - Cohen's d = 8.37 (far exceeds threshold 0.8 untuk "large")
   - Perbaikan bukan hanya signifikan statistik, tapi juga praktis

3. **Perbaikan Terbesar pada Destinasi Dekat:**
   - Near (<5 km): improvement 3.88%
   - Medium (5-10 km): improvement 3.30%
   - Far (>10 km): improvement 0.50%
   - Validasi bahwa spatial filtering efektif untuk cluster geografis

4. **Konsistensi Across Folds:**
   - Perbaikan stabil di semua 5 fold (std = 0.24%)
   - Tidak ada fold yang menunjukkan degradasi performa

---

## Citation

Jika menggunakan hasil ini untuk publikasi, mohon sitasi:

```
Arsonisr, K. P. (2024). Peningkatan Akurasi Sistem Rekomendasi Pariwisata 
Semarang Menggunakan Algoritma Context-Aware Collaborative Filtering. 
[Skripsi, Teknik Informatika].
```

---

**Generated:** 2024-03-11  
**Source Experiment:** `../05-kode/src/experiment.py`  
**Analysis Script:** `../05-kode/notebooks/04_analysis.ipynb`
