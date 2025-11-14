# SPKHIV - Sistem Pendukung Keputusan HIV

**Sistem Pendukung Keputusan (SPK) untuk Diagnosis HIV berbasis Web**

Aplikasi web berbasis expert system yang membantu dalam proses diagnosis fase HIV menggunakan metode rule-based dengan perhitungan persentase kemiripan gejala. Sistem ini dirancang untuk memberikan informasi awal tentang kemungkinan fase HIV berdasarkan gejala yang dialami pasien.

## 📋 Daftar Isi

- [Fitur Utama](#-fitur-utama)
- [Teknologi yang Digunakan](#-teknologi-yang-digunakan)
- [Persyaratan Sistem](#-persyaratan-sistem)
- [Instalasi](#-instalasi)
- [Konfigurasi](#-konfigurasi)
- [Penggunaan](#-penggunaan)
- [Struktur Proyek](#-struktur-proyek)
- [Algoritma Diagnosis](#-algoritma-diagnosis)
- [Screenshot](#-screenshot)
- [Kontribusi](#-kontribusi)
- [Lisensi](#-lisensi)

## ✨ Fitur Utama

### Frontend (User)
- 🏠 **Halaman Beranda** - Informasi tentang sistem dan HIV
- 📝 **Form Data Diri** - Input nama, usia, dan jenis kelamin
- ❓ **Kuesioner Gejala** - Pertanyaan gejala secara bertahap
- 📊 **Hasil Diagnosis** - Menampilkan persentase kemungkinan untuk setiap fase HIV
- 💊 **Rekomendasi Solusi** - Saran penanganan berdasarkan hasil diagnosis
- 📄 **Export PDF** - Download hasil diagnosis dalam format PDF
- 🔄 **Ulang Diagnosis** - Mulai diagnosis baru

### Backend (Admin)
- 🔐 **Sistem Autentikasi** - Login menggunakan Filament
- 👥 **Manajemen User** - CRUD pengguna dengan role-based access control
- 🦠 **Manajemen Penyakit** - Kelola data fase HIV (Fase 1, 2, 3)
- 🩺 **Manajemen Gejala** - Kelola daftar gejala HIV
- 🔗 **Manajemen Relasi** - Hubungkan gejala dengan penyakit
- 💡 **Manajemen Solusi** - Kelola rekomendasi solusi per penyakit
- 📈 **Riwayat Diagnosis** - Lihat dan kelola semua hasil diagnosis
- 📥 **Export Excel** - Export data ke format Excel
- 🛡️ **Role & Permission** - Sistem hak akses berbasis Spatie Permissions

## 🛠️ Teknologi yang Digunakan

### Backend
- **Laravel 11** - PHP Framework
- **Filament 3.2** - Admin Panel Builder
- **MySQL** - Database Management System
- **Spatie Laravel Permission** - Role & Permission Management
- **DomPDF** - PDF Generation
- **Filament Excel** - Excel Export

### Frontend
- **Tailwind CSS 4** - CSS Framework
- **Alpine.js** - JavaScript Framework
- **Vite** - Build Tool
- **Feather Icons** - Icon Library

### Development Tools
- **Laravel Breeze** - Authentication Scaffolding
- **Laravel Pint** - Code Style Fixer
- **PHPUnit** - Testing Framework

## 📦 Persyaratan Sistem

- **PHP** >= 8.2
- **Composer** >= 2.0
- **Node.js** >= 18.x
- **NPM** >= 9.x
- **MySQL** >= 8.0
- **Web Server** (Apache/Nginx) atau PHP Built-in Server

## 🚀 Instalasi

### 1. Clone Repository

```bash
git clone https://github.com/username/appDiagnosaHIV.git
cd appDiagnosaHIV
```

### 2. Install Dependencies

```bash
# Install PHP dependencies
composer install

# Install Node.js dependencies
npm install
```

### 3. Setup Environment

```bash
# Copy file environment
cp .env.example .env

# Generate application key
php artisan key:generate
```

### 4. Konfigurasi Database

Edit file `.env` dan sesuaikan konfigurasi database:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=db_diagnosa_hiv
DB_USERNAME=root
DB_PASSWORD=
```

### 5. Import Database

Import file SQL yang ada di folder `db_backup/` ke database MySQL Anda, atau jalankan migration:

```bash
# Jalankan migration
php artisan migrate

# Jalankan seeder (jika ada)
php artisan db:seed
```

### 6. Setup Storage Link

```bash
php artisan storage:link
```

### 7. Build Assets

```bash
# Development
npm run dev

# Production
npm run build
```

### 8. Jalankan Aplikasi

```bash
# Development server
php artisan serve

# Atau menggunakan Laragon/XAMPP
# Akses melalui http://localhost/appDiagnosaHIV/public
```

## ⚙️ Konfigurasi

### Setup Admin User

Untuk membuat user admin pertama kali, jalankan:

```bash
php artisan tinker
```

Kemudian di dalam tinker:

```php
$user = \App\Models\User::create([
    'name' => 'Admin',
    'email' => 'admin@example.com',
    'password' => bcrypt('password'),
]);

$user->assignRole('admin');
```

Atau gunakan seeder yang sudah ada:

```bash
php artisan db:seed --class=RolePermissionSeeder
```

### Konfigurasi Filament

Pastikan konfigurasi Filament sudah benar di file `.env`:

```env
APP_URL=http://localhost
FILAMENT_DOMAIN=localhost
```

## 📖 Penggunaan

### Untuk User (Frontend)

1. **Akses Halaman Beranda**
   - Buka browser dan akses URL aplikasi
   - Klik tombol "Mulai Diagnosis" atau "Cek Sekarang"

2. **Isi Data Diri**
   - Masukkan nama, usia, dan pilih jenis kelamin
   - Klik "Lanjut" untuk memulai kuesioner

3. **Jawab Pertanyaan Gejala**
   - Jawab setiap pertanyaan gejala dengan "Ya" atau "Tidak"
   - Sistem akan menampilkan pertanyaan berikutnya secara otomatis

4. **Lihat Hasil Diagnosis**
   - Setelah semua pertanyaan selesai, sistem akan menampilkan hasil
   - Hasil menampilkan persentase kemungkinan untuk setiap fase HIV
   - Fase dengan persentase tertinggi akan ditampilkan sebagai diagnosis utama

5. **Download Hasil (Opsional)**
   - Klik tombol "Download PDF" untuk menyimpan hasil diagnosis

### Untuk Admin (Backend)

1. **Login ke Admin Panel**
   - Akses `/admin/login`
   - Masukkan email dan password admin

2. **Kelola Data**
   - **Penyakit**: Tambah/edit fase HIV beserta keterangannya
   - **Gejala**: Kelola daftar gejala yang akan ditanyakan
   - **Relasi**: Hubungkan gejala dengan penyakit yang relevan
   - **Solusi**: Tambahkan rekomendasi solusi untuk setiap penyakit
   - **Hasil Diagnosis**: Lihat riwayat semua diagnosis yang telah dilakukan

3. **Manajemen User**
   - Tambah/edit user
   - Atur role dan permission untuk setiap user

## 📁 Struktur Proyek

```
appDiagnosaHIV/
├── app/
│   ├── Filament/              # Filament Admin Panel Resources
│   │   ├── Pages/
│   │   ├── Resources/         # CRUD Resources untuk Admin
│   │   └── Widgets/          # Dashboard Widgets
│   ├── Http/
│   │   ├── Controllers/      # Application Controllers
│   │   └── Requests/         # Form Request Validation
│   ├── Models/               # Eloquent Models
│   │   ├── Gejala.php
│   │   ├── Penyakit.php
│   │   ├── Solusi.php
│   │   ├── Relasi.php
│   │   └── HasilDiagnosa.php
│   └── Providers/
├── config/                    # Configuration Files
├── database/
│   ├── migrations/           # Database Migrations
│   └── seeders/              # Database Seeders
├── public/                    # Public Assets
├── resources/
│   ├── views/                # Blade Templates
│   │   ├── front/            # Frontend Views
│   │   └── filament/        # Filament Views
│   ├── css/                  # CSS Files
│   └── js/                   # JavaScript Files
├── routes/
│   └── web.php               # Web Routes
├── db_backup/                # Database Backup Files
└── tests/                    # Test Files
```

## 🧮 Algoritma Diagnosis

Sistem menggunakan algoritma **Rule-Based dengan Perhitungan Persentase**:

### Formula Perhitungan

```
Persentase = (Jumlah Gejala yang Cocok / Total Gejala untuk Penyakit) × 100%
```

### Proses Diagnosis

1. **Input Gejala**: User menjawab pertanyaan gejala satu per satu
2. **Koleksi Gejala**: Sistem mengumpulkan semua gejala yang dijawab "Ya"
3. **Perhitungan**: Untuk setiap penyakit (fase HIV):
   - Ambil daftar gejala yang terkait dengan penyakit tersebut
   - Hitung berapa banyak gejala yang cocok dengan gejala yang dipilih user
   - Hitung persentase: `(gejala cocok / total gejala penyakit) × 100%`
4. **Hasil**: Penyakit dengan persentase tertinggi menjadi diagnosis utama

### Contoh

Jika user memilih gejala: [1, 2, 3, 4, 5]

Penyakit A memiliki gejala: [1, 2, 3, 6, 7, 8]
- Gejala cocok: [1, 2, 3] = 3 gejala
- Total gejala: 6
- Persentase: (3/6) × 100% = 50%

Penyakit B memiliki gejala: [1, 2, 3, 4, 5]
- Gejala cocok: [1, 2, 3, 4, 5] = 5 gejala
- Total gejala: 5
- Persentase: (5/5) × 100% = 100%

**Hasil**: Penyakit B dengan persentase 100% menjadi diagnosis utama.

## 🖼️ Screenshot

*(Tambahkan screenshot aplikasi di sini jika diperlukan)*

## 🤝 Kontribusi

Kontribusi sangat diterima! Untuk berkontribusi:

1. Fork repository ini
2. Buat branch fitur baru (`git checkout -b feature/AmazingFeature`)
3. Commit perubahan Anda (`git commit -m 'Add some AmazingFeature'`)
4. Push ke branch (`git push origin feature/AmazingFeature`)
5. Buka Pull Request

## ⚠️ Disclaimer

**PENTING**: Aplikasi ini adalah sistem pendukung keputusan yang dirancang untuk memberikan informasi awal. Hasil diagnosis dari sistem ini **BUKAN** pengganti konsultasi medis profesional. Selalu konsultasikan dengan dokter atau tenaga kesehatan profesional untuk diagnosis dan pengobatan yang tepat.

## 📝 Lisensi

Proyek ini menggunakan lisensi [MIT License](LICENSE).

## 👤 Author

- **Your Name** - [GitHub](https://github.com/username)

## 🙏 Acknowledgments

- Laravel Community
- Filament Team
- Spatie Team
- Semua kontributor open source yang membuat proyek ini mungkin

---

**Dibuat dengan ❤️ menggunakan Laravel & Filament**
