# Modul 6 - Concurrency

**Commit 1 Reflection Notes**

Method *handle_connection* adalah sebuah fungsi dalam bahasa pemrograman Rust yang mengelola koneksi TCP dengan klien. Method ini akan menerima koneksi TCP sebagai argumen dan membaca permintaan HTTP dari klien yang terhubung. Method akan menggunakan `BufReader` untuk membaca data dari koneksi TcpStream dan menyimpannya dalam bentuk vektor (*Vec<_>*). Data dibaca baris per baris hingga ditemukan baris kosong yang menandakan akhir permintaan HTTP. Selanjutnya, permintaan HTTP yang telah dibaca disimpan dalam vektor `http_request` dan ditampilkan ke konsol.