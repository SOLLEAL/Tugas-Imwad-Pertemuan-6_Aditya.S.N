# PTM-06 Prompt Log

## Prompt 01 — Analisis Kebutuhan

**Tujuan:** Mengidentifikasi kebutuhan sistem web scraping dan analisis sentimen berita Kabupaten Jombang.

**Hasil:** Sistem membutuhkan scraping berita, filter relevansi, ekstraksi metadata, preprocessing, klasifikasi sentimen, dashboard, filter, statistik, dan export CSV.

## Prompt 02 — Arsitektur

**Tujuan:** Membentuk arsitektur modular dengan pola Router → Service → Repository → Database.

**Hasil:** Modul dipisahkan menjadi API, scraper, NLP, database, dan export.

## Prompt 03 — NLP

**Tujuan:** Menentukan pipeline pemrosesan teks.

**Hasil:** Case folding → pembersihan → tokenisasi → stopword removal → TF-IDF → Multinomial Naive Bayes.

## Prompt 04 — API

**Tujuan:** Menentukan kontrak endpoint.

**Hasil:** `GET /api/news`, `POST /api/scrape`, `GET /api/sentiment/summary`, dan `GET /api/export`.

## Prompt 05 — Keamanan

**Tujuan:** Mengadaptasi praktik keamanan backend modular.

**Hasil:** Validasi input, pembatasan sumber scraping, rate limit, parameterized query, environment variables, HTTPS, dan autentikasi admin.

## Prompt 06 — Dokumentasi

**Tujuan:** Menyusun dokumentasi dengan pola repository tugas yang terstruktur.

**Hasil:** Dokumentasi dibagi menjadi scaffold arsitektur, keamanan, autentikasi, prompt log, dan laporan.
