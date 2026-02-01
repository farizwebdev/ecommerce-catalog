# 🛍️ E-Commerce Catalog - Vue.js

![Vue.js](https://img.shields.io/badge/Vue.js-35495E?style=for-the-badge&logo=vuedotjs&logoColor=4FC08D)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![Netlify](https://img.shields.io/badge/Netlify-00C7B7?style=for-the-badge&logo=netlify&logoColor=white)

> **Tugas Akhir Project Based Internship: Rakamin Academy x Core Initiative**

Proyek ini adalah aplikasi web responsif yang mensimulasikan katalog produk e-commerce sederhana. Aplikasi ini mengambil data secara dinamis dari **FakeStoreAPI** dan menampilkan produk dengan tema UI yang berbeda-beda secara otomatis berdasarkan kategorinya (Pakaian Pria vs Pakaian Wanita).

---

## Demo Aplikasi

**[🔗 Klik disini untuk melihat Website Live](https://ecommerce-catalog-fariz.netlify.app/)**

---

## Fitur Utama

### 1. Tema Dinamis (Dynamic Theming) 🎨
Tampilan UI secara otomatis beradaptasi berdasarkan kategori produk yang diambil dari API:
- **Pakaian Pria (Men's Clothing):** Tema Biru dengan pola geometris spesifik.
- **Pakaian Wanita (Women's Clothing):** Tema Ungu dengan pola abstrak yang lembut.
- **Tidak Tersedia (Unavailable):** Tema Abu-abu dengan tata letak khusus "Wajah Sedih" untuk kategori yang tidak didukung.

### 2. Pengalaman Pengguna (UX) ⚡
- **Modal Selamat Datang:** Popup informatif yang responsif saat pertama kali masuk, menjelaskan cakupan proyek.
- **Desain Responsif:** Tampilan yang optimal untuk Desktop, Tablet, dan Ponsel (Mobile).
- **Status Loading:** Indikator loading (spinner) kustom untuk memberi tahu pengguna saat data sedang diambil.
- **Penanganan Error:** Menangani produk di luar kategori target dengan tampilan yang rapi (tidak error blank).

### 3. Spesifikasi Teknis 🛠️
- Dibangun menggunakan **Vue.js 2** (Options API).
- Styling menggunakan **Pure Vanilla CSS** (Tanpa Framework seperti Bootstrap/Tailwind).
- Pengambilan data menggunakan **Fetch API** bawaan browser.

---

## Instalasi & Penggunaan

Jika Anda ingin menjalankan proyek ini secara lokal di komputer Anda, ikuti langkah-langkah berikut:

1. Clone repository
```bash
git clone [https://github.com/farizwebdev/ecommerce-catalog.git](https://github.com/farizwebdev/ecommerce-catalog.git)
cd ecommerce-catalog
```

2. Install dependencies
Pastikan Node.js sudah terinstall, lalu jalankan:
```bash
npm install
```

3. Jalankan server development
```bash
npm run serve
```
Aplikasi akan berjalan di http://localhost:8080.

---

## Struktur Proyek

```bash
ecommerce-catalog/
├── public/
├── src/
│   ├── assets/
│   │   └── style/
│   │       └── page.css      # Semua styling global & komponen (Vanilla CSS)
│   ├── components/
│   │   └── ProductDisplay.vue # Komponen utama (Logika & UI)
│   ├── App.vue               # Komponen Root
│   └── main.js               # Entry point Vue
├── package.json
└── README.md
```

---

## Author

Fariz Husain Albar Mahasiswa Informatika UIN Sunan Kalijaga.

 - Instagram: farizwebdev

 - LinkedIn: Fariz Husain Albar

Copyright © 2026. All rights reserved.
