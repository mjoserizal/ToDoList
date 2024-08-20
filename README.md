# ToDo List Application

## Deskripsi

Aplikasi ToDo List ini memungkinkan pengguna untuk membuat daftar tugas (To Do) dengan kategori yang telah ditentukan. Pengguna juga dapat mengisi informasi profil seperti nama, username, dan email. Validasi dilakukan pada input email untuk memastikan format email yang dimasukkan benar.

## Fitur

- **Menambah To Do:** Pengguna dapat menambah tugas baru dengan deskripsi dan kategori yang dipilih.
- **Hapus To Do:** Pengguna dapat menghapus tugas yang tidak diperlukan.
- **Validasi Email:** Aplikasi memeriksa apakah format email yang dimasukkan valid sebelum menyimpan data.
- **Kategori To Do:** Pengguna dapat memilih kategori untuk setiap tugas dari daftar kategori yang tersedia.

## Teknologi yang Digunakan

- **Vue.js:** Framework JavaScript yang digunakan untuk membangun antarmuka pengguna.
- **Axios:** Digunakan untuk melakukan request HTTP ke backend.
- **SweetAlert2:** Digunakan untuk menampilkan pesan popup dengan gaya yang menarik.
- **CSS:** Untuk styling komponen.

## Instalasi

Untuk menjalankan proyek ini secara lokal, ikuti langkah-langkah berikut:

1. Clone repositori ini:
   ```bash
   git clone https://github.com/username/repository.git
   ```
2. Masuk ke direktori proyek:
   ```bash
   cd repository
   ```
3. Install dependencies menggunakan npm:
   ```bash
   npm install
   ```
4. Jalankan aplikasi:
   ```bash
   npm run serve
   ```
5. Akses aplikasi di browser pada alamat `http://localhost:8080`.

## API Endpoints

Aplikasi ini menggunakan API untuk mengambil data kategori dan menyimpan tugas. Berikut adalah endpoint yang digunakan:

- **GET `/api/categories`:** Mengambil daftar kategori.
- **POST `/api/tasks`:** Menyimpan daftar tugas yang telah dibuat oleh pengguna.

## Cara Penggunaan

1. Buka aplikasi di browser Anda.
2. Isi informasi pengguna pada form (Nama, Username, Email).
3. Tambahkan tugas dengan mengisi deskripsi dan memilih kategori.
4. Tekan tombol "SIMPAN" untuk menyimpan daftar tugas.

## Validasi Email

- Sebelum menyimpan form, aplikasi akan memvalidasi apakah format email yang dimasukkan benar. Jika tidak valid, akan muncul pesan error melalui SweetAlert2.

## Catatan Pengembangan

- **Tambah To Do:** Gunakan tombol "+ Tambah To Do" untuk menambah tugas baru.
- **Hapus To Do:** Gunakan tombol 🗑️ untuk menghapus tugas yang tidak diperlukan.
- **Kategori:** Kategori diambil dari API dan pengguna bisa memilih dari daftar dropdown.

## Kontribusi

Jika Anda ingin berkontribusi pada proyek ini, Anda dapat membuat pull request dengan perubahan atau penambahan fitur yang Anda buat.

## Lisensi

Proyek ini dilisensikan di bawah MIT License - lihat file [LICENSE](LICENSE) untuk detail lebih lanjut.
