# Implementasi Autentikasi & Keamanan Sistem

## 1. Konsep

Mengikuti pola backend modular, autentikasi dapat ditempatkan pada middleware/dependency FastAPI apabila sistem membutuhkan akun administrator.

## 2. Hak Akses

```text
User
 └── Melihat berita
 └── Melakukan filter
 └── Melihat statistik
 └── Export data sesuai hak akses

Admin
 └── Seluruh hak User
 └── Menjalankan scraping
 └── Mengelola sumber berita
 └── Melihat log proses
```

## 3. Password

Password pengguna tidak disimpan dalam bentuk plaintext. Sistem menggunakan password hashing dengan algoritma yang sesuai, misalnya bcrypt.

## 4. Token

Jika API menggunakan JWT, token digunakan untuk mengidentifikasi sesi/akses endpoint yang membutuhkan autentikasi. Secret key disimpan melalui environment variable.

## 5. Endpoint Terproteksi

Contoh endpoint yang dapat membutuhkan autentikasi:

- `POST /api/scrape`
- pengelolaan sumber berita;
- pengelolaan model;
- endpoint administrasi.

Endpoint baca seperti `GET /api/news` dapat dibuat publik sesuai kebutuhan aplikasi.

## 6. Catatan Implementasi

Autentikasi bukan inti metode scraping dan analisis sentimen. Fitur ini merupakan lapisan keamanan aplikasi yang mengikuti pola arsitektur backend modular dari repository referensi.
