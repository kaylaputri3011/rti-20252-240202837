# 05-kode

Folder ini berisi source code penelitian: implementasi algoritma, eksperimen, dan analisis.

---

## Struktur

```
05-kode/
├── src/                          # Source code utama
│   ├── data/
│   │   ├── loader.py             # Load & preprocess dataset
│   │   └── splitter.py           # 5-Fold Cross Validation
│   ├── models/
│   │   ├── base_cf.py            # Abstract class untuk CF
│   │   ├── baseline_cf.py        # Baseline User-Based CF
│   │   └── context_aware_cf.py   # Context-Aware CF + Spatial
│   ├── utils/
│   │   ├── similarity.py         # Pearson Correlation
│   │   ├── distance.py           # Haversine formula
│   │   └── metrics.py            # MAE, RMSE
│   ├── experiment.py             # Main experiment script (5-Fold CV)
│   └── config.py                 # Hyperparameters
├── notebooks/                    # Jupyter notebooks
│   ├── 01_eda.ipynb              # Exploratory Data Analysis
│   ├── 02_baseline_validation.ipynb
│   ├── 03_grid_search_radius.ipynb
│   └── 04_analysis.ipynb         # Analisis hasil eksperimen
├── tests/                        # Unit tests
│   ├── test_similarity.py
│   ├── test_distance.py
│   └── test_models.py
├── requirements.txt              # Python dependencies
└── README.md                     # Dokumentasi ini
```

---

## Setup Environment

### 1. Install Dependencies

```bash
cd 05-kode
pip install -r requirements.txt
```

**Requirements:**
```
pandas==1.5.3
numpy==1.24.3
scikit-learn==1.2.2
scipy==1.10.1
geopy==2.3.0
matplotlib==3.7.1
seaborn==0.12.2
jupyter==1.0.0
```

### 2. Verifikasi Instalasi

```python
python -c "import pandas, numpy, sklearn, geopy; print('Setup OK')"
```

---

## Cara Menjalankan

### Tahap 1: Exploratory Data Analysis

```bash
cd notebooks
jupyter notebook 01_eda.ipynb
```

Output: Visualisasi distribusi rating, sparsity matrix, geographic distribution

### Tahap 2: Grid Search Threshold Jarak

```bash
jupyter notebook 03_grid_search_radius.ipynb
```

Output: Radius optimal = 10 km (MAE terendah)

### Tahap 3: Eksperimen 5-Fold CV

```bash
cd ..
python src/experiment.py
```

Output: `../06-output/results/experiment_results.json`

**Expected Runtime:** ~15 menit (tergantung spesifikasi mesin)

### Tahap 4: Analisis Hasil

```bash
cd notebooks
jupyter notebook 04_analysis.ipynb
```

Output:
- Tabel agregasi MAE/RMSE
- Uji statistik (Paired T-Test)
- Visualisasi (boxplot, scatter, improvement)

---

## Implementasi Algoritma

### Baseline User-Based CF

**File:** `src/models/baseline_cf.py`

**Fitur:**
- Similarity metric: Pearson Correlation
- K-nearest neighbors: 30
- Prediction: Weighted average dengan mean-centering

**Cara Pakai:**
```python
from src.models.baseline_cf import BaselineCF
import pandas as pd

# Load data
train = pd.read_csv('../04-data/clean/reviews_clean.csv')

# Train model
model = BaselineCF(k_neighbors=30)
model.fit(train)

# Predict
prediction = model.predict(user_id='U001', item_id='P042')
print(f"Predicted rating: {prediction:.2f}")
```

### Context-Aware CF

**File:** `src/models/context_aware_cf.py`

**Fitur:**
- Spatial pre-filtering: Haversine (radius 10 km)
- Reference location: centroid item yang pernah dirating user
- Fallback: user mean jika item di luar radius

**Cara Pakai:**
```python
from src.models.context_aware_cf import ContextAwareCF

# Train model
model = ContextAwareCF(k_neighbors=30, radius_km=10.0)
model.fit(train)

# Predict dengan context location
prediction = model.predict(
    user_id='U001', 
    item_id='P042',
    context_location=(-6.9932, 110.4203)  # Simpang Lima
)
print(f"Predicted rating: {prediction:.2f}")
```

---

## Unit Tests

Jalankan semua unit tests:

```bash
cd tests
python -m pytest test_*.py -v
```

**Test Coverage:**
- Pearson Correlation computation
- Haversine distance accuracy
- Baseline CF prediction consistency
- Context-Aware CF spatial filtering
- Edge cases (cold-start, missing data)

**Expected Output:**
```
test_similarity.py::test_pearson_correlation PASSED
test_distance.py::test_haversine PASSED
test_models.py::test_baseline_prediction PASSED
test_models.py::test_context_aware_filtering PASSED
...
12 passed in 2.34s
```

---

## Reproducibility

Semua eksperimen menggunakan **random seed = 42** untuk reproducibility:

```python
# Di src/experiment.py
np.random.seed(42)
skf = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
```

Hasil eksperimen dapat direproduksi identik di mesin lain dengan environment yang sama.

---

## Hyperparameters

**File:** `src/config.py`

```python
# Baseline CF
K_NEIGHBORS = 30
SIMILARITY_METRIC = 'pearson'

# Context-Aware CF
RADIUS_KM = 10.0
REFERENCE_MODE = 'centroid'  # 'centroid' | 'last_location'

# Validation
N_FOLDS = 5
RANDOM_SEED = 42

# Metrics
PRIMARY_METRIC = 'mae'
SECONDARY_METRIC = 'rmse'
```

---

## Performance

**Baseline CF:**
- Training time: ~2 menit (4.362 records)
- Prediction time: ~0.015 detik per prediksi
- Memory usage: ~150 MB

**Context-Aware CF:**
- Training time: ~2.5 menit (termasuk build spatial index)
- Prediction time: ~0.012 detik per prediksi (lebih cepat karena filtered candidates)
- Memory usage: ~180 MB

---

## Troubleshooting

**Error: `ModuleNotFoundError: No module named 'geopy'`**
```bash
pip install geopy
```

**Error: Jupyter kernel not found**
```bash
python -m ipykernel install --user
```

**Error: Out of memory during experiment**
- Reduce K_NEIGHBORS dari 30 ke 20
- Atau gunakan mesin dengan RAM ≥ 8 GB

---

**Last Updated:** 2024-03-01
