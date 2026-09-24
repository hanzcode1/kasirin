# 🧾 Kasirin — Aplikasi Kasir Digital Ringan

Aplikasi kasir (POS) sederhana untuk usaha mikro, kecil, dan menengah.
Dibuat ringan, cepat, dan gampang dipakai — cocok buat warung, toko kelontong,
kafe kecil, food truck, atau siapa aja yang jualan.

> **Filosofi kami:** kasir nggak harus ribet. Yang penting jalan, cepat, dan datanya aman.

---

## 📋 Daftar Isi

1. [Fitur Utama](#-fitur-utama)
2. [Persyaratan Sistem](#-persyaratan-sistem)
3. [Cara Install (Step by Step)](#-cara-install-step-by-step)
4. [Cara Pakai](#-cara-pakai)
5. [Akun Default](#-akun-default)
6. [Troubleshooting](#-troubleshooting)
7. [FAQ](#-faq)
8. [Teknologi yang Dipakai](#-teknologi-yang-dipakai)

---

## ✨ Fitur Utama

### Untuk Kasir
- 🛒 **Transaksi cepat** — klik produk, langsung masuk keranjang
- 💰 **Dua metode bayar** — Tunai dan QRIS
- 🔍 **Pencarian produk** — cari pakai nama, langsung muncul
- 🏷️ **Filter kategori** — Makanan, Minuman, Snack, Sembako, dll
- 🖨️ **Cetak struk** — tinggal klik, langsung print
- 📱 **Responsif** — jalan di komputer, tablet, atau HP

### Untuk Admin
- 📊 **Dashboard ringkas** — penjualan, transaksi, stok, semua kelihatan
- 📦 **Kelola produk** — tambah, edit, hapus, atur stok
- 📈 **Laporan penjualan** — per hari, per periode, bisa difilter
- ⚙️ **Pengaturan toko** — nama, alamat, telepon, footer struk
- 👥 **Multi user** — bikin akun kasir dan admin terpisah
- 🔐 **Ganti password sendiri** — aman, tanpa perlu bantuan developer

### Keamanan
- ✅ Password di-hash pakai bcrypt (bukan plain text)
- ✅ Semua query pakai prepared statement (aman dari SQL injection)
- ✅ Session-based login
- ✅ Role-based access (admin vs kasir beda halaman)

---

## 💻 Persyaratan Sistem

Sebelum mulai, pastikan komputer kamu punya:

| Kebutuhan | Versi Minimal | Keterangan |
|-----------|---------------|------------|
| **PHP** | 7.4 atau lebih baru | Bahasa pemrograman utamanya |
| **MySQL / MariaDB** | 5.7 atau lebih baru | Tempat nyimpan data |
| **Web Server** | Apache / Nginx | Bisa pakai XAMPP, Laragon, atau MAMP |
| **Browser** | Chrome, Firefox, Edge, Safari | Browser modern apa aja boleh |

> **Buat yang baru mulai:** cara paling gampang adalah install **XAMPP**.
> XAMPP sudah include PHP + MySQL + Apache dalam satu paket. Tinggal download,
> install, nyalain. Selesai.

---

## 🚀 Cara Install (Step by Step)

### Langkah 1 — Install XAMPP

1. Download XAMPP di [https://www.apachefriends.org](https://www.apachefriends.org)
2. Install seperti biasa (next, next, finish)
3. Buka **XAMPP Control Panel**
4. Klik **Start** pada bagian **Apache** dan **MySQL**
5. Kalau dua-duanya hijau, berarti sudah jalan ✅

### Langkah 2 — Copy Folder Project

1. Copy folder `kasirin/` ke dalam folder `htdocs`
   - **Windows:** `C:\xampp\htdocs\kasirin\`
   - **Mac:** `/Applications/XAMPP/htdocs/kasirin/`
   - **Linux:** `/opt/lampp/htdocs/kasirin/`

2. Pastikan isinya seperti ini:
![folder](https://fands.infinityfreeapp.com/pixelite/uploads/6ab4cb8481f49_1790233476.png)


### Langkah 3 — Buat Database

1. Buka browser, ketik: **`http://localhost/phpmyadmin`**
2. Klik **New** di sidebar kiri
3. Nama database: **`kasirin`**
4. Klik **Create**

### Langkah 4 — Import Database

1. Klik database **`kasirin`** yang baru dibuat
2. Klik tab **Import** di atas
3. Klik **Choose File** → pilih file **`db.sql`** dari folder project
4. Scroll ke bawah, klik **Import**
5. Kalau berhasil, akan muncul pesan hijau ✅
6. Cek sidebar kiri — harusnya muncul tabel: `users`, `produk`, `kategori`, `transaksi`, `transaksi_detail`, `pengaturan`

### Langkah 5 — Konfigurasi Koneksi Database

1. Buka file **`config/database.php`** pakai text editor (Notepad++, VS Code, Sublime)
2. Sesuaikan bagian ini dengan pengaturan komputer kamu:

```php
define('DB_HOST', 'localhost');   // biasanya localhost
define('DB_USER', 'root');        // default XAMPP: root
define('DB_PASS', '');            // default XAMPP: kosong
define('DB_NAME', 'kasirin');     // nama database tadi
define('BASE_URL', 'http://localhost/kasirin/');
```
> Catatan: kalau kamu pakai Laragon atau MAMP, DB_USER dan DB_PASS
mungkin beda. Cek dokumentasi tool-nya ya.

### Langkah 6 — Buka Aplikasi

1. Buka browser
2. Ketik: http://localhost/kasirin/
3. Akan muncul halaman login
4. Login pakai akun default

---
## 📖 Cara Pakai

### Login Pertama Kali
1. Buka http://localhost/kasirin/
2. Masukkan:
**Username**: `admin`
**Password**: `admin`
3. Klik **Masuk**

### Menambah Produk (Pertama Kali)
Database produk masih kosong — jadi tugas pertama kamu adalah mengisi produk.
1. Setelah login, kamu masuk ke **`Dashboard Admin`**
2. Klik menu **Produk** di sidebar kiri
3. Klik tombol **Tambah Produk** (kanan atas)
4. Isi form:
**Kode produk** — otomatis terisi, boleh diubah
**Nama produk** — contoh: "Nasi Goreng Spesial"
**Kategori** — pilih dari dropdown
**Stok** — jumlah barang yang ada
**Harga beli** — harga modal (opsional)
**Harga jual** — harga ke pembeli (wajib)
**Satuan — pcs**, porsi, botol, kg, dll
5. Klik **Simpan Produk**
6. Ulangi untuk produk lainnya

### Melakukan Transaksi (Kasir)

1. Klik menu **Buka Kasir** di sidebar (atau tombol di kanan atas)
2. Kamu akan masuk ke halaman kasir
3. **Pilih produk** — klik kartu produk, langsung masuk keranjang
4. **Atur jumlah** — pakai tombol `+` dan `-` di keranjang
5. **Pilih metode bayar** — Tunai atau QRIS
6. Klik tombol **Bayar Sekarang**
7. Muncul popup sukses → klik **Transaksi Baru** atau **Cetak Struk**

Stok produk otomatis berkurang setiap kali transaksi berhasil ✅

### Melihat Laporan Penjualan

1. Klik menu **Laporan** di sidebar
2. Pilih periode (dari tanggal — sampai tanggal)
3. Klik **Tampilkan**
4. Muncul ringkasan: total penjualan, jumlah transaksi, tunai vs QRIS, dan detail tiap transaksi

### Mengubah Password & Username

1. Klik menu **Pengaturan** di sidebar
2. Scroll ke bagian **Akun Saya**
3. Isi:
Username baru (boleh tetap sama)
Password lama (wajib benar)
Password baru
Konfirmasi password baru
4. Klik **Ubah Akun**

### Menambah User Baru (Kasir/Admin)

1. Masih di halaman **Pengaturan**
2. Scroll ke bagian **Tambah User**
3. Isi username, nama lengkap, password, dan pilih role:
**Kasir** — cuma bisa akses halaman kasir
**Admin** — bisa akses semua
4. Klik **Tambah User**

### Mengubah Nama Toko / Alamat

1. Halaman **Pengaturan** → bagian **Informasi Toko**
2. Ubah nama, alamat, telepon, footer struk
3. Klik **Simpan**

## 🔑 Akun Default

Setelah import `db.sql`, akan ada satu akun otomatis:

| Username | Password | Role          |
|----------|----------|---------------|
| admin    | admin    | Administrator |

> **PENTING!** Setelah login pertama kali, segera ganti password
> lewat menu **Pengaturan → Akun Saya**. Jangan biarkan password default
> terlalu lama — demi keamanan toko kamu.

---

## 🔧 Troubleshooting

### ❌ "Koneksi database gagal"

**Penyebab:** MySQL belum nyala atau konfigurasi salah.

**Solusi:**
- Buka XAMPP Control Panel, pastikan **MySQL** hijau
- Cek `config/database.php` — pastikan `DB_NAME = kasirin`
- Kalau pakai Laragon/MAMP, `DB_PASS` mungkin tidak kosong

---

### ❌ "404 Not Found" saat buka `http://localhost/kasirin/`

**Penyebab:** Folder salah taruh, atau nama folder beda.

**Solusi:**
- Cek folder `kasirin` benar ada di `htdocs` (XAMPP) atau `www` (Laragon)
- Pastikan `BASE_URL` di `config/database.php` sesuai
- Coba akses langsung: `http://localhost/kasirin/login.php`

---

### ❌ "Username atau password salah" padahal isi `admin` / `admin`

**Penyebab:** Hash password di database tidak cocok.

**Solusi:**

1. Buat file `install.php` di folder `kasirin/` dengan isi:

   ```php
   <?php
   echo password_hash('admin', PASSWORD_DEFAULT);
   ```

2. Buka `http://localhost/kasirin/install.php` di browser
3. Copy hasil hash-nya
4. Buka phpMyAdmin → database `kasirin` → tabel `users`
5. Edit baris `admin`, ganti kolom `password` dengan hash tadi
6. Simpan → coba login lagi
7. **Hapus file `install.php` setelah selesai**

---

### ❌ Halaman putih / blank

**Penyebab:** Ada error PHP yang tidak tampil.

**Solusi:**
- Buka `php.ini` (di folder XAMPP)
- Cari `display_errors`, ubah jadi `On`
- Restart Apache
- Refresh halaman — error akan muncul

---

### ❌ Stok tidak berkurang setelah transaksi

**Penyebab:** Transaksi gagal tersimpan ke database.

**Solusi:**
- Cek tabel `transaksi` di phpMyAdmin — apakah ada data baru?
- Kalau tidak ada, kemungkinan session habis — coba login ulang
- Kalau masih error, lihat pesan error di browser

---

## ❓ FAQ

**Q: Apakah aplikasi ini gratis?**
A: Ya. Silakan pakai, ubah, dan kembangkan sesuai kebutuhan.

**Q: Bisa dipakai di HP?**
A: Bisa. Tampilannya sudah responsif. Tapi untuk pengalaman terbaik,
kasir biasanya dipakai di komputer atau tablet.

**Q: Bisa dipakai offline?**
A: Bisa, selama server (XAMPP) jalan di komputer yang sama.
Kalau mau diakses dari banyak perangkat, harus di-hosting atau pakai
jaringan lokal.

**Q: Bagaimana kalau saya jualan di 2 tempat?**
A: Versi ini satu outlet. Untuk multi-outlet, butuh pengembangan tambahan.

**Q: Apakah data aman?**
A: Selama kamu rutin backup database (export dari phpMyAdmin),
data relatif aman. Password user sudah di-hash, jadi tidak bisa dibaca
langsung di database.

**Q: Bisa import produk dari Excel?**
A: Belum ada fitur itu di versi ini. Tapi kamu bisa tambah produk
satu per satu (cukup cepat kok).

**Q: Kenapa stok ada yang warna kuning/merah?**
A: Itu indikator visual:
- 🟢 Hijau = stok aman
- 🟡 Kuning = stok menipis (≤ 5)
- 🔴 Merah = stok habis

**Q: Bagaimana cara backup data?**
A: Buka phpMyAdmin → pilih database `kasirin` → tab **Export** →
klik **Go**. File `.sql` akan otomatis terdownload. Simpan file itu
di tempat aman.

**Q: Bagaimana cara restore data dari backup?**
A: Buka phpMyAdmin → pilih database `kasirin` → tab **Import** →
pilih file `.sql` backup → klik **Go**.

---

## 🛠️ Teknologi yang Dipakai

| Bagian     | Teknologi                        | Alasan                              |
|------------|----------------------------------|-------------------------------------|
| Backend    | PHP 7.4+ (native, tanpa framework)| Ringan, cepat, mudah dipahami       |
| Database   | MySQL / MariaDB                  | Standar industri, gratis, stabil    |
| Frontend   | HTML5 + CSS3 murni               | Tanpa framework, ringan             |
| JavaScript | Vanilla JS (tanpa library)       | Cepat, tidak perlu compile          |
| Font       | Poppins (Google Fonts)           | Modern, mudah dibaca                |
| Icon       | Font Awesome 6                   | Lengkap, konsisten                  |
| Warna      | Palet pastel smooth              | Nyaman di mata, tidak melelahkan    |

---

## 📝 Lisensi

Bebas dipakai, dimodifikasi, dan dibagikan.
Silakan pakai untuk usaha kamu sendiri, atau kembangkan jadi lebih baik.