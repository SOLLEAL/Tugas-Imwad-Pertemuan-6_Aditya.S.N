# Audit Keamanan API & Validasi Sistem Berita Jombang

## 1. Tujuan Audit

Audit dilakukan untuk memastikan API pada sistem scraping dan analisis sentimen dapat menerima permintaan secara terkontrol, memvalidasi input, dan tidak mengekspos data yang tidak diperlukan.

## 2. Validasi Input

API harus memvalidasi:

- format URL sumber berita;
- batas jumlah halaman scraping;
- parameter page dan limit;
- nilai sentiment hanya `positive`, `neutral`, atau `negative`;
- format tanggal;
- keyword pencarian.

## 3. Risiko Utama

### A. Input Tidak Valid

Input yang tidak sesuai dapat menyebabkan error atau proses yang tidak diperlukan. Pencegahan dilakukan melalui schema validation FastAPI/Pydantic.

### B. SSRF pada Sumber Scraping

Jika pengguna dapat memasukkan URL arbitrer, sistem perlu membatasi domain sumber yang diperbolehkan agar server tidak digunakan untuk mengakses alamat internal.

### C. Rate Limit

Endpoint scraping perlu dibatasi untuk mencegah permintaan berlebihan dan beban terhadap server maupun portal berita.

### D. Data Sensitif

Sistem hanya menyimpan data berita publik yang dibutuhkan. Data pribadi pembaca tidak menjadi bagian dari ruang lingkup sistem.

### E. SQL Injection

Repository database harus menggunakan parameterized query/ORM dan tidak menyusun query dari input pengguna secara langsung.

## 4. Prinsip Keamanan

- Validasi seluruh input.
- Gunakan HTTPS pada deployment.
- Jangan menyimpan secret/API key di source code.
- Gunakan environment variables untuk konfigurasi.
- Batasi akses database.
- Catat error tanpa membocorkan credential.
- Terapkan timeout pada request scraping.

## 5. Kesimpulan

Keamanan sistem difokuskan pada validasi API, pembatasan sumber scraping, perlindungan database, pengendalian request, serta pengelolaan konfigurasi rahasia.
