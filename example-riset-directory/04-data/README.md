# 04-data

Folder ini berisi dataset penelitian — raw dan clean.

---

## Struktur

```
04-data/
├── raw/                          # Dataset mentah dari scraping
│   └── google_maps_reviews_raw.csv  (5.123 records)
├── clean/                        # Dataset setelah cleaning
│   ├── reviews_clean.csv         (4.362 records)
│   └── places_metadata.csv       (78 places)
└── README.md                     # Dokumentasi ini
```

---

## Dataset Raw

**File:** `raw/google_maps_reviews_raw.csv`

**Sumber:** Google Maps Reviews API  
**Periode Scraping:** 2024-02-05  
**Total Records:** 5.123 ulasan  
**Destinasi:** 87 tempat wisata di Kota Semarang

**Schema:**
```
user_id       : string  (hashed Google Account ID)
place_id      : string  (Google Place ID)
rating        : float   (1.0 - 5.0)
latitude      : float   (koordinat destinasi)
longitude     : float   (koordinat destinasi)
timestamp     : datetime (waktu review dibuat)
review_text   : string  (teks ulasan, optional)
```

---

## Dataset Clean

**File:** `clean/reviews_clean.csv`

**Total Records:** 4.362 ulasan  
**User Unique:** 892  
**Place Unique:** 78  
**Missing Values:** 0

**Cleaning Pipeline:**
1. Hapus duplikat (UserID, PlaceID): 5.123 → 4.897
2. Validasi range rating [1, 5]: 4.897 → 4.897 (0 outlier)
3. Validasi geolokasi (bounding box Semarang): 4.897 → 4.673
4. Filter user dengan < 3 rating: 4.673 → 4.362
5. Deteksi bot/spam: 0 user suspicious

**Schema:**
```
user_id       : string  (U001, U002, ..., U892)
place_id      : string  (P001, P002, ..., P078)
rating        : float   (1.0 - 5.0)
latitude      : float   (-7.05 hingga -6.95)
longitude     : float   (110.35 hingga 110.50)
timestamp     : datetime (2020-07-15 hingga 2023-11-28)
```

**File:** `clean/places_metadata.csv`

**Total Records:** 78 destinasi

**Schema:**
```
place_id      : string  (P001, P002, ..., P078)
place_name    : string  (nama destinasi)
category      : string  (alam, religi, kuliner, sejarah, budaya)
latitude      : float
longitude     : float
avg_rating    : float   (rata-rata rating)
n_reviews     : int     (jumlah ulasan)
```

---

## Statistik Dataset Clean

| Metrik | Nilai |
|--------|-------|
| Total Records | 4.362 |
| User Unique | 892 |
| Place Unique | 78 |
| Sparsity | 93,73% |
| Periode | 2020-07-15 hingga 2023-11-28 (3,5 tahun) |
| Missing Values | 0 |
| Distribusi Rating | 1★: 2% \| 2★: 4% \| 3★: 15% \| 4★: 40% \| 5★: 39% |

---

## Catatan Privacy

- User ID sudah di-hash (tidak dapat di-trace ke akun riil)
- Geolokasi hanya untuk destinasi publik (bukan lokasi user)
- Review text tidak disertakan di dataset clean (hanya rating numerik)
- Sesuai dengan etika penelitian data sekunder

---

## Cara Akses

Dataset clean tersedia untuk reproducibility:

```python
import pandas as pd

# Load dataset
df = pd.read_csv('04-data/clean/reviews_clean.csv')
places = pd.read_csv('04-data/clean/places_metadata.csv')

print(f"Total reviews: {len(df)}")
print(f"Total places: {len(places)}")
print(f"Date range: {df['timestamp'].min()} to {df['timestamp'].max()}")
```

---

**Last Updated:** 2024-02-15
