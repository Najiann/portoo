# Dokumentasi Teknis Portofolio Jihan Aulia

Dokumentasi komprehensif arsitektur, fitur interaktif, tata kelola keamanan panel admin, dan panduan penerapan (*deployment*) portofolio Jihan Aulia.

---

## 1. Ikhtisar & Filosofi Desain

Proyek ini adalah portofolio interaktif berbasis **Vue 3** dan **Vite** yang dirancang khusus untuk memenuhi standar ekspektasi **Tech Recruiter (HR)** dan calon klien jasa automasi alur kerja (*workflow automation*).

### Standar Kualitas antislop
Desain dan kode mematuhi panduan filter antislop secara ketat:
- **Bebas AI Slop:** Tidak menggunakan gradien ungu generik, ornamen bola melayang, kapsul badge bertuliskan "AI Powered", atau pola grid blueprint tanpa fungsi.
- **Hierarki Berbasis Konten (C-1, C-3):** Setiap bagian layout disusun untuk memamerkan kapabilitas teknis nyata (n8n, Laravel/PHP, Python ML, integrasi bot).
- **Kejujuran Data & Bukti Nyata (C-5, R-17, R-18, R-38):** Menghindari testimoni palsu dan angka metrik fiktif. Seluruh proyek ditautkan langsung ke repositori publik asli di GitHub (@Najiann).
- **Aksesibilitas Penuh (R-25, R-32):** Memenuhi standar rasio kontras WCAG AA di kedua tema, navigasi ramah keyboard (`Tab`, `Enter`, `Escape`), dan cincin fokus `:focus-visible` berdefinisi tinggi.
- **Larangan Karakter Em Dash (R-02):** Bebas 100% dari karakter em dash di seluruh salinan teks dan kode antarmuka.

---

## 2. Struktur Proyek

```text
portoo-main/
├── dist/                      # Direktori artefak produksi hasil build Vite
├── public/                    # Aset statis publik
├── src/
│   ├── assets/                # Gambar, logo, dan ikon
│   ├── components/            # Komponen modular Vue
│   ├── App.vue                # Komponen utama portofolio & state management
│   ├── main.js                # Entry point aplikasi Vue 3
│   └── style.css              # Reset CSS global & sistem token tema (dark/light)
├── DESIGN.md                  # Spesifikasi desain, palet warna, dan dial antislop
├── DOCUMENTATION.md           # Dokumentasi teknis lengkap (berkas ini)
├── GEMINI.md                  # Panduan agen AI dengan blok pointer antislop
├── index.html                 # Template HTML utama
├── package.json               # Konfigurasi dependensi dan skrip npm
├── README.md                  # Panduan umum & ringkasan proyek untuk GitHub
└── vite.config.js             # Konfigurasi bundler Vite
```

---

## 3. Rincian Fitur Utama

### A. Pengalih Tema (Dark & Light Mode)
- **Tema Bawaan:** Dark Theme (`#0b1118` latar belakang dengan `#111c27` kartu permukaan). Dirancang dengan nuansa teknis presisi untuk kenyamanan mata rekruter dan klien.
- **Tema Terang:** Light Theme (`#f8fafc` latar belakang dengan `#ffffff` kartu permukaan).
- **Penyimpanan Status:** Preferensi tema disimpan secara lokal di `localStorage` (`jihan_portfolio_theme`), sehingga pilihan tema tidak akan hilang saat halaman disegarkan (*refresh*).

### B. Visualisasi Interaktif Alur Automasi (n8n Pipeline Explorer)
Komponen edukatif dan interaktif yang mendemonstrasikan logika kerja nyata yang pernah dibangun di PT Mafi Global Asia:
1. **Langkah 1 (Trigger):** Webhook HTTP POST untuk menangkap event pesanan baru secara real-time.
2. **Langkah 2 (Transformasi):** Pembersihan, normalisasi format nomor WhatsApp, dan validasi data via Code Node.
3. **Langkah 3 (Integrasi Data):** Sinkronisasi database transaksi dan pembaruan catatan lead CRM.
4. **Langkah 4 (Notifikasi):** Pengiriman pesan instan otomatis via WhatsApp Business Gateway.

*Pengguna dapat mengeklik setiap langkah untuk meninjau contoh payload input, operasi node, serta dampak efisiensi bisnisnya.*

### C. Kredensial & Modal Sertifikat Interaktif
- Menampilkan sertifikasi nyata:
  - **Machine Learning Cohort Graduate** (Dicoding Indonesia x DBS Foundation Coding Camp 2025).
  - **Sertifikasi Kompetensi Kejuruan RPL** (Lembaga Sertifikasi Profesi / BNSP 2025).
  - **Digital Support & Workflow Automation Completion** (PT Mafi Global Asia 2026).
- **Label Transparan (R-23, R-38):** Sertifikat fisik yang belum memiliki berkas soft file dilabeli secara jujur `[Sertifikat Fisik / Menunggu Unggahan Digital]`.
- **Modal Interaktif:** Mengeklik kartu sertifikat membuka jendela rincian verifikasi yang dapat ditutup melalui tombol silang, klik di luar kotak, atau menekan tombol `Escape` pada keyboard.

### D. Integrasi Repositori Publik GitHub API
- Mengambil repositori publik terbaru dari endpoint: `https://api.github.com/users/Najiann/repos?sort=updated&per_page=15`.
- Menyaring repositori *fork* secara otomatis dan memprioritaskan proyek asli:
  - `Inventory-Management-System` (Laravel / Blade)
  - `Stunting_Prediction` (Laravel / Blade)
  - `Stunting_Model_ML` (Python / Jupyter Notebook)
  - `CosRent` (PHP / MySQL)
  - `Tripz-bus` (Blade / Laravel)
  - `portoo` (Vue 3)
- Dilengkapi tab filter kategori (Semua, Web & PHP, Machine Learning, Vue & Frontend), kotak pencarian langsung (*real-time search*), serta penanganan 3 kondisi status (*loading skeleton*, *error state* dengan tombol coba ulang, dan *empty state*).

### E. Komunikasi & Formulir Kontak Terverifikasi
- **Tombol Salin Email:** Mengeklik tombol langsung menyalin `jihanaulia2408@gmail.com` ke clipboard pengguna dengan umpan balik visual instan ("Tersalin!").
- **Formulir Pesan Fungsional:** Mengisi nama, email, kategori kebutuhan, dan pesan kemudian mengeklik tombol submit akan memvalidasi data dan otomatis membuka draf pesan email terstruktur (`mailto:`) ke alamat Jihan Aulia.

---

## 4. Mekanisme Keamanan Panel Admin Rahasia

Panel Admin dirancang agar **100% tersembunyi dari publik, klien, dan HR recruiter**. Elemen tombol admin hanya akan muncul jika identitas Anda telah terverifikasi di peramban.

### Cara Membuka Akses Admin (3 Metode Alternatif):

1. **Metode Parameter URL (Sangat Praktis):**
   Buka portofolio dengan menyisipkan parameter `admin=jihan`:
   ```text
   http://localhost:5173/?admin=jihan
   ```
   *(Di Vercel: `https://nama-domain-anda.vercel.app/?admin=jihan`)*
   Sistem otomatis mengaktifkan status admin, menyimpan izin ke `localStorage` (`jihan_admin_auth: true`), dan membersihkan URL dari bilah peramban.

2. **Metode Pintasan Keyboard (Desktop):**
   Tekan kombinasi tombol:
   ```text
   Ctrl + Shift + A   (Windows / Linux)
   Cmd + Shift + A    (macOS)
   ```
   Akan muncul dialog autentikasi rahasia. Masukkan PIN:
   - **PIN Bawaan:** `jihan2026` *(atau `admin2026`)*

3. **Metode Ketukan Simbol Monogram (Mobile / Smartphone):**
   Ketuk simbol monogram **`>_`** di sebelah nama "Jihan Aulia" sebanyak **5 kali berturut-turut** dalam tempo 3 detik untuk memunculkan dialog PIN.

### Operasi di Dalam Panel Admin:
- **Tambah Sertifikat Baru:** Masukkan judul, lembaga penerbit, tahun, kategori, status dokumen (digital/fisik), dan deskripsi kompetensi.
- **Hapus Sertifikat:** Menghapus data sertifikat yang tidak lagi ingin ditampilkan.
- **Kembalikan Data Bawaan:** Tombol reset cepat untuk memulihkan dataset sertifikat standar.
- **Kunci & Keluar Mode Admin:** Klik tombol *"🔒 Kunci & Keluar Mode Admin"* di bagian bawah panel untuk menghapus sesi admin dan menguji tampilan portofolio sebagaimana dilihat oleh klien publik.

---

## 5. Panduan Menjalankan Secara Lokal

### Prasyarat:
- Node.js versi 18.x atau lebih baru.
- npm versi 9.x atau lebih baru.

### Langkah-langkah:
1. Masuk ke direktori proyek:
   ```bash
   cd d:\portoo-main
   ```
2. Pasang dependensi:
   ```bash
   npm install
   ```
3. Jalankan server pengembangan lokal:
   ```bash
   npm run dev
   ```
4. Buka tautan lokal di browser:
   ```text
   http://localhost:5173/
   ```
5. Untuk membuat bundel produksi:
   ```bash
   npm run build
   ```

---

## 6. Panduan Deployment ke Vercel

Portofolio ini siap diterapkan ke **Vercel** secara instan:

1. **Unggah Perubahan ke GitHub:**
   Pastikan kode terbaru sudah di-commit dan di-push ke repositori GitHub Anda (`Najiann/portoo`).
   ```bash
   git add .
   git commit -m "feat: complete interactive portfolio with antislop compliance and secret admin gate"
   git push origin main
   ```

2. **Impor Proyek di Vercel Dashboard:**
   - Masuk ke [vercel.com](https://vercel.com).
   - Klik tombol **"Add New..."** lalu pilih **"Project"**.
   - Hubungkan akun GitHub Anda dan pilih repositori `portoo`.

3. **Konfigurasi Project Settings:**
   - **Framework Preset:** Vite
   - **Build Command:** `npm run build` *(atau biarkan default)*
   - **Output Directory:** `dist` *(default Vite)*
   - **Install Command:** `npm install` *(default)*

4. **Klik Deploy:**
   - Vercel akan memproses build dalam waktu sekitar 20 sampai 40 detik.
   - Domain publik gratis akan langsung aktif (contoh: `https://portoo-najiann.vercel.app`).

---

## 7. Rencana Peningkatan Database Masa Depan (Opsional)

Saat ini seluruh data sertifikat disimpan secara mandiri dan cepat di `localStorage` peramban Anda. 
Jika kelak Anda ingin beralih ke database berbasis cloud:

1. **Rekomendasi Utama: Supabase (PostgreSQL Cloud):**
   - Menggunakan PostgreSQL asli yang dapat diakses langsung dari Vue via paket resmi `@supabase/supabase-js`.
   - Memiliki fitur **Supabase Storage** gratis untuk mengunggah berkas PDF sertifikat fisik saat sudah tersedia.
   - Memiliki sistem **Authentication** untuk login admin berbasis email & kata sandi resmi.
2. **Langkah Transisi:**
   - Cukup buat tabel `certificates` di Supabase.
   - Hubungkan kunci API publik Supabase di berkas `.env` proyek.
   - Arahkan metode `loadCertificates()` dan `saveCertificates()` di `App.vue` untuk memanggil Supabase client alih-alih `localStorage`.

