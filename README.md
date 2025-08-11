# Manajer Portofolio Berbasis Web

Ini adalah aplikasi web portofolio *single-page* yang sepenuhnya berjalan di sisi klien (*client-side*). Didesain untuk menjadi solusi yang ringkas, cepat, dan mudah dikelola tanpa memerlukan basis data atau server backend. Semua data dikelola melalui satu file `portfolio.json` dan disimpan sementara di browser pengguna, memberikan pengalaman pengeditan langsung.

## Tujuan Proyek

Tujuan utama dari proyek ini adalah untuk menyediakan platform bagi para profesional, pengembang, atau kreatif untuk menampilkan karya dan profil mereka dengan cara yang modern dan interaktif. Proyek ini memungkinkan pengguna untuk:

- **Menampilkan Profil Profesional:** Menunjukkan informasi pribadi, keahlian, dan tautan sosial.
- **Mempresentasikan Portofolio Proyek:** Mengelola dan menampilkan daftar proyek dengan deskripsi, media (gambar/video), dan dokumentasi teknis yang mendetail.
- **Manajemen Konten yang Mudah:** Memberikan antarmuka admin sederhana untuk menambah, mengedit, dan menghapus konten portofolio langsung dari browser.
- **Portabilitas Data:** Memungkinkan semua data portofolio diekspor dan diimpor dalam format JSON yang mudah dibaca.
- **Deployment Sederhana:** Dapat di-hosting di layanan hosting statis manapun dengan mudah.

---

## Stack Teknologi

Aplikasi ini dibangun menggunakan teknologi web standar yang berfokus pada performa dan kemudahan pengembangan.

- **HTML5:** Struktur dasar dari aplikasi web.
- **Tailwind CSS:** Kerangka kerja CSS *utility-first* untuk desain antarmuka yang modern dan responsif.
- **Vanilla JavaScript (ES6):** Logika inti aplikasi, termasuk manajemen state, manipulasi DOM, dan fungsionalitas admin, tanpa menggunakan kerangka kerja eksternal.
- **Marked.js:** Sebuah pustaka kecil untuk mem-parsing Markdown menjadi HTML, digunakan untuk menampilkan dokumentasi proyek yang kaya format.
- **JSON (JavaScript Object Notation):** Format data utama yang digunakan untuk menyimpan dan mengelola semua konten portofolio.

---

## Alur Kerja Program

Aplikasi ini beroperasi sepenuhnya di browser pengguna. Berikut adalah alur kerjanya:

1.  **Inisialisasi:** Saat halaman dimuat, JavaScript akan mencoba mengambil data dari file `portfolio.json`.
2.  **Fallback ke LocalStorage:** Jika `portfolio.json` tidak dapat diakses atau kosong, aplikasi akan mencoba memuat data dari `localStorage` browser. Ini memastikan bahwa sesi pengeditan sebelumnya tidak hilang.
3.  **Render Tampilan:** Data yang berhasil dimuat (profil dan item portofolio) akan ditampilkan di antarmuka pengguna.
4.  **Mode Admin:**
    - Pengguna dapat mengklik tombol **"Login"** untuk masuk ke mode admin.
    - Kata sandi admin di-hardcode dalam file `index.html` (default: `sirjosev`).
    - Setelah berhasil login, status login disimpan di `sessionStorage`, dan kontrol admin (tombol tambah, edit, hapus, dll.) akan muncul.
5.  **Manajemen Konten (CRUD):**
    - **Tambah/Edit:** Admin dapat mengisi formulir untuk menambah item baru atau mengedit item yang sudah ada. Perubahan ini mencakup judul, deskripsi, kategori (tag), tautan media, dan dokumentasi Markdown.
    - **Hapus:** Item dapat dihapus dengan konfirmasi.
    - **Edit Profil:** Informasi profil seperti nama, bio, dan tautan sosial juga dapat diubah melalui mode admin.
6.  **Penyimpanan Sementara:** Setiap perubahan yang dibuat (tambah, edit, hapus) akan **segera disimpan di `localStorage` browser**. Ini memungkinkan admin untuk melakukan banyak perubahan dalam satu sesi tanpa kehilangan data.
7.  **Penyimpanan Permanen (Ekspor):** Karena `localStorage` hanya ada di browser admin, perubahan tersebut tidak akan terlihat oleh pengunjung lain. Untuk membuatnya permanen, admin **harus** menggunakan tombol **"Ekspor Semua"** untuk mengunduh data dalam format `portfolio.json`. File yang diunduh ini kemudian harus menggantikan file `portfolio.json` yang ada di repositori proyek.

---

## Struktur Data (`portfolio.json`)

File `portfolio.json` adalah pusat dari aplikasi ini. Strukturnya terdiri dari sebuah objek utama dengan dua properti: `profile` dan `items`.

```json
{
  "profile": {
    "name": "Nama Anda",
    "title": "Jabatan / Keahlian Anda",
    "bio": "Deskripsi singkat tentang diri Anda.",
    "imageUrl": "URL ke foto profil Anda",
    "githubUrl": "URL ke profil GitHub Anda",
    "linkedinUrl": "URL ke profil LinkedIn Anda"
  },
  "items": [
    {
      "id": "item-1754670390378",
      "title": "Judul Proyek",
      "categories": "#WebDev #UIUX #JavaScript",
      "description": "Deskripsi singkat mengenai proyek ini.",
      "media": [
        "https://url-ke-gambar-proyek.jpg",
        "https://url-ke-video-demo.mp4",
        "https://www.youtube.com/watch?v=xxxxx"
      ],
      "documentation": "Konten dokumentasi dalam format **Markdown**. Bisa berisi `code blocks`, daftar, dan lain-lain."
    }
  ]
}
```

- **`profile`**: Objek yang berisi informasi pribadi untuk ditampilkan di bagian "About Me".
- **`items`**: Array dari objek-objek portofolio. Setiap objek memiliki:
    - **`id`**: ID unik yang dibuat secara otomatis.
    - **`title`**: Judul proyek.
    - **`categories`**: String berisi tag-tag yang dipisahkan spasi, diawali dengan `#`. Digunakan untuk filtering.
    - **`description`**: Penjelasan singkat proyek.
    - **`media`**: Array dari string URL untuk gambar, video, atau tautan YouTube.
    - **`documentation`**: String berisi penjelasan mendetail dalam format Markdown.

---

## Petunjuk Penggunaan

### Untuk Pengunjung

1.  **Buka Halaman:** Cukup akses URL tempat proyek ini di-hosting.
2.  **Lihat Proyek:** Gulir ke bawah untuk melihat semua item portofolio dalam format kartu.
3.  **Filter Proyek:** Klik pada tag (misalnya, "WebDev", "UIUX") di bagian atas galeri untuk memfilter proyek berdasarkan kategori. Klik "all" untuk menampilkan kembali semua proyek.
4.  **Lihat Detail:** Klik di area mana saja pada kartu proyek untuk membuka tampilan detail (pratinjau) yang menampilkan deskripsi lengkap, media, dan dokumentasi.

### Untuk Admin (Pemilik Portofolio)

1.  **Login:** Klik tombol **"Login"** di pojok kanan atas dan masukkan kata sandi (default: `sirjosev`).
2.  **Kelola Item:**
    - **Tambah:** Klik tombol **"+ Tambah Item Baru"**.
    - **Edit/Hapus:** Tombol "Edit" dan "Hapus" akan muncul di setiap kartu proyek.
3.  **Edit Profil:** Klik tombol **"Edit Profil"** di bagian "About Me" untuk mengubah data pribadi Anda.
4.  **Simpan Perubahan (Sangat Penting!):**
    - Setelah selesai mengedit, klik tombol **"Ekspor Semua"**.
    - Sebuah file bernama `portfolio.json` akan terunduh ke komputer Anda.
    - **Ganti** file `portfolio.json` lama di repositori proyek Anda dengan file yang baru diunduh ini.
    - Commit dan push perubahan tersebut ke repositori Git Anda agar pembaruan dapat dilihat oleh semua orang.

---

## Cara Deployment

Aplikasi ini dapat di-deploy di platform hosting mana pun yang mendukung file statis.

### Contoh: GitHub Pages

1.  **Pastikan Repositori Anda Siap:** Pastikan semua file (`index.html`, `portfolio.json`, dan `README.md`) ada di repositori GitHub Anda.
2.  **Buka Pengaturan Repositori:** Navigasi ke repositori Anda di GitHub, lalu klik tab **"Settings"**.
3.  **Pilih Sumber Pages:** Di menu sebelah kiri, klik **"Pages"**.
4.  **Konfigurasi Build and Deployment:**
    - Di bawah "Build and deployment", pada bagian "Source", pilih **"Deploy from a branch"**.
    - Pilih branch yang ingin Anda deploy (biasanya `main` atau `master`).
    - Pastikan folder diatur ke `/ (root)`.
    - Klik **"Save"**.
5.  **Akses Situs Anda:** GitHub akan memberikan URL (misalnya, `https://<username>.github.io/<repository-name>/`) di mana portofolio Anda sekarang dapat diakses secara publik. Tunggu beberapa menit hingga proses deployment selesai.
