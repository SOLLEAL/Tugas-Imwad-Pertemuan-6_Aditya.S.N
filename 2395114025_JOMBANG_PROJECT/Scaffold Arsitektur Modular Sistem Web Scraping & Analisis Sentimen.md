# Scaffold Arsitektur Modular Sistem Web Scraping & Analisis Sentimen

## 1. Tujuan

Sistem digunakan untuk mengumpulkan berita online yang berkaitan dengan Kabupaten Jombang, mengolah teks berita, melakukan klasifikasi sentimen, menyimpan hasil, dan menampilkannya pada dashboard.

## 2. Arsitektur

```text
User/Admin
   ↓
Frontend / Dashboard
   ↓
FastAPI API
   ↓
Router
   ↓
Service Layer
   ├── Scraping Service
   ├── Relevance Filter
   ├── Deduplication Service
   ├── NLP Preprocessing
   ├── TF-IDF Feature Extraction
   ├── Naive Bayes Classifier
   └── Export Service
   ↓
Repository Layer
   ↓
Database
```

## 3. Struktur Backend

```text
app/
├── main.py
├── api/
│   ├── news.py
│   ├── scraping.py
│   └── sentiment.py
├── scraper/
│   ├── base.py
│   ├── sources/
│   └── parser.py
├── nlp/
│   ├── preprocess.py
│   ├── vectorizer.py
│   └── classifier.py
├── database/
│   ├── models.py
│   └── repository.py
└── export/
    └── csv_export.py
```

## 4. Alur Scraping

1. Sistem menerima sumber berita.
2. Backend mengirim HTTP request.
3. HTML halaman diproses menggunakan BeautifulSoup.
4. Sistem mengambil judul, URL, media, tanggal, penulis, lokasi, kategori, dan isi berita jika tersedia.
5. Artikel diperiksa relevansinya terhadap Kabupaten Jombang.
6. Artikel duplikat berdasarkan URL tidak disimpan kembali.

## 5. Preprocessing

```text
Raw Text
   ↓
Case Folding
   ↓
Remove URL
   ↓
Remove Punctuation
   ↓
Normalize Whitespace
   ↓
Tokenization
   ↓
Stopword Removal
   ↓
Clean Text
```

## 6. Klasifikasi Sentimen

```text
Clean Text
   ↓
TF-IDF Vectorizer
   ↓
Multinomial Naive Bayes
   ↓
Class Probability
   ↓
Positive / Neutral / Negative
```

## 7. Repository

Operasi utama:

- `create_article()`
- `get_articles()`
- `get_article_by_id()`
- `find_by_url()`
- `get_sentiment_summary()`

Field minimum artikel:

- media
- title
- url
- content
- published_at
- sentiment

Field opsional:

- subtitle
- author
- location
- category

## 8. API

### GET /api/news

Parameter:

- keyword
- media
- sentiment
- start_date
- end_date
- page
- limit

### POST /api/scrape

```json
{
  "sources": ["source_a", "source_b"],
  "keyword": "Jombang",
  "page_limit": 5
}
```

### GET /api/sentiment/summary

Menghasilkan jumlah berita positif, netral, negatif, dan total.

### GET /api/export

Menghasilkan CSV berdasarkan filter aktif.

## 9. Penanganan Error

- Sumber tidak dapat diakses → dicatat dan proses sumber lain dilanjutkan.
- Selector HTML tidak ditemukan → field dicatat sebagai gagal.
- Artikel kosong → tidak disimpan.
- URL duplikat → tidak disimpan.
- Model gagal → status error dicatat.
- Database gagal → proses penyimpanan dibatalkan dan error dicatat.

## 10. Teknologi

- Python
- FastAPI
- Requests
- BeautifulSoup
- scikit-learn
- SQLite/PostgreSQL
- React/Next.js
- CSV
