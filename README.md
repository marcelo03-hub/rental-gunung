# Bug Hunter TRPL — Sistem Peminjaman Perlengkapan (Rental Gear)

[![Laravel](https://img.shields.io/badge/Laravel-13.x-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)](https://laravel.com)
[![PHP](https://img.shields.io/badge/PHP-8.3%2B-777BB4?style=for-the-badge&logo=php&logoColor=white)](https://php.net)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-v4-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)](https://tailwindcss.com)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

Aplikasi web berbasis **Laravel** untuk manajemen distribusi dan pencatatan peminjaman perlengkapan kelompok (*Posko Perlengkapan Domestic Backpacker / Edurace Paddock Equipment*). Aplikasi ini juga dirancang sebagai materi studi kasus troubleshooting dan *bug hunting* untuk mahasiswa Teknologi Rekayasa Perangkat Lunak (TRPL).

---

## 📌 Fitur Utama

- **📦 Katalog Perlengkapan (*Technical Inventory*)**  
  Menampilkan daftar perlengkapan yang tersedia di posko lengkap dengan foto unit, kode gear, dan status kesiapan unit.

- **📝 Formulir Peminjaman (*Requisition Form*)**  
  Memungkinkan perwakilan kelompok untuk mengajukan peminjaman alat dengan validasi nama kelompok serta kuantitas unit yang dipinjam.

- **📊 Log & Riwayat Peminjaman Real-Time (*Live Dispatch Log*)**  
  Mencatat setiap transaksi peminjaman secara berurutan dan transparan untuk memudahkan pelacakan peralatan.

- **📈 Ringkasan Statistik (*Spec Bar Metrics*)**  
  Menyajikan ringkasan cepat berupa jumlah katalog perangkat, total log peminjaman, dan akumulasi unit yang sedang dipinjam.

- **🎨 Modern Visual Design System**  
  Mengusung antarmuka bertema gelap (*Dark Canvas*) yang elegan dengan aksen Rosso Corsa yang responsif di berbagai ukuran layar.

---

## 🛠️ Tumpukan Teknologi (Tech Stack)

- **Backend:** PHP ^8.3, Laravel ^13.x
- **Frontend:** Blade Templating, Tailwind CSS v4, Inter Typography
- **Database:** SQLite / MySQL (didukung Eloquent ORM)
- **Asset Bundler:** Vite 8
- **Testing Suite:** PHPUnit / Laravel Testing Tools

---

## 📋 Persyaratan Sistem

Sebelum menjalankan proyek ini, pastikan sistem Anda telah terpasang:

- **PHP** >= 8.3 (dengan ekstensi `pdo`, `sqlite3` atau `pdo_mysql`, `mbstring`, `openssl`, `tokenizer`, `xml`)
- **Composer** >= 2.x
- **Node.js** >= 18.x dan **npm**
- **Git**

---

## 🚀 Panduan Instalasi & Menjalankan Proyek

Ikuti langkah-langkah berikut untuk mengatur dan menjalankan aplikasi di komputer lokal:

### 1. Klon Repositori
```bash
git clone https://github.com/marcelo03-hub/rental-gunung.git
cd rental-gunung
```

### 2. Pasang Dependensi Composer (PHP)
```bash
composer install
```

### 3. Salin Berkas Konfigurasi Lingkungan (`.env`)
Salin file `.env.example` menjadi `.env`:

**Linux / macOS:**
```bash
cp .env.example .env
```

**Windows (PowerShell / Command Prompt):**
```bash
copy .env.example .env
```

### 4. Buat Application Key
```bash
php artisan key:generate
```

### 5. Konfigurasi Database & Jalankan Migrasi

#### Menggunakan SQLite (Rekomendasi Cepat):
Pastikan di file `.env`:
```env
DB_CONNECTION=sqlite
```
Buat file database kosong (jika belum ada):
```bash
# Windows PowerShell
New-Item -ItemType File -Path database/database.sqlite -Force

# Linux / macOS / Git Bash
touch database/database.sqlite
```

#### Menggunakan MySQL:
Sesuaikan konfigurasi pada file `.env`:
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=bug-hunter
DB_USERNAME=root
DB_PASSWORD=
```

#### Jalankan Migrasi dan Seeder Awal:
```bash
php artisan migrate --seed
```

> **Catatan:** Seeder akan mengisi data awal berupa perlengkapan: *Power Bank*, *Jas Hujan*, *Senter*, dan *Backpack*.

### 6. Pasang Dependensi Frontend & Build Aset
```bash
npm install
npm run build
```

Jika dalam tahap pengembangan (mode watch/HMR):
```bash
npm run dev
```

### 7. Jalankan Server Lokal Laravel
```bash
php artisan serve
```

Aplikasi dapat diakses melalui peramban web di:
```text
http://127.0.0.1:8000
```

---

## 📁 Struktur Direktori Penting

```plaintext
Bug-Hunter-TRPL/
├── app/
│   ├── Http/Controllers/
│   │   └── BorrowingController.php   # Logika katalog & transaksi peminjaman
│   └── Models/
│       ├── Equipment.php             # Model data master perlengkapan
│       └── Borrowing.php             # Model transaksi peminjaman
├── database/
│   ├── migrations/                   # Skema tabel equipments & borrowings
│   └── seeders/
│       └── DatabaseSeeder.php        # Data awal perlengkapan posko
├── public/
│   └── images/                       # Aset gambar peralatan posko
├── resources/
│   └── views/
│       ├── layouts/app.blade.php     # Layout utama & Ferrari design tokens
│       └── borrowings/
│           ├── index.blade.php       # Tampilan katalog & riwayat peminjaman
│           └── create.blade.php      # Formulir peminjaman perlengkapan
├── routes/
│   └── web.php                       # Definisi rute web aplikasi
└── tests/
    └── Feature/ExampleTest.php       # Uji coba fitur & endpoint
```

---

## 🧪 Menjalankan Pengujian (Testing)

Proyek ini telah dilengkapi uji otomatis menggunakan PHPUnit. Untuk menjalankan seluruh rangkaian test:

```bash
php artisan test
```

Untuk menjalankan file test tertentu:
```bash
php artisan test --filter=ExampleTest
```

---

## 🔍 Catatan & Troubleshooting Kasus Bug Hunting

Sebagai bagian dari latihan *Bug Hunting TRPL*, beberapa potensi isu umum dan penanganannya antara lain:

1. **Rute Tidak Ditemukan (`Route [xxx] not defined`)**:
   Pastikan penamaan rute pada `routes/web.php` sinkron dengan pemanggilan fungsi `route(...)` di file Blade view maupun Controller (`borrowing.index` vs `borrowings.index`).
2. **Gambar Peralatan Tidak Muncul**:
   Periksa path gambar pada atribut `image` di tabel `equipments` (atau seeder) dan pastikan file gambar fisik tersedia di direktori `public/images/`.
3. **Sintaks Blade Error (`ParseError`)**:
   Perhatikan kurung kurawal ganda Blade `{{ ... }}` pada template tampilan agar tidak terjadi nesting kurung kurawal ganda yang tidak valid.
4. **Cache Konfigurasi Lingkungan**:
   Jika perubahan file `.env` tidak diterapkan, bersihkan cache konfigurasi melalui:
   ```bash
   php artisan config:clear
   php artisan cache:clear
   ```

---

## 📄 Lisensi

Proyek ini didistribusikan di bawah lisensi [MIT License](LICENSE).
