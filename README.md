# Modul 6 - Concurrency

**Commit 1 Reflection Notes**

Method `handle_connection` adalah sebuah fungsi dalam bahasa pemrograman Rust yang mengelola koneksi TCP dengan klien. Method ini akan menerima koneksi TCP sebagai argumen dan membaca permintaan HTTP dari klien yang terhubung. Method akan menggunakan `BufReader` untuk membaca data dari koneksi `TcpStream` dan menyimpannya dalam bentuk vektor `Vec<_>`. Data dibaca baris per baris hingga ditemukan baris kosong yang menandakan akhir permintaan HTTP. Selanjutnya, permintaan HTTP yang telah dibaca disimpan dalam vektor `http_request` dan ditampilkan ke konsol.

**Commit 2 Reflection Notes**
![Commit 2 screen capture](/assets/images/commit2.png)
Method `handle_connection` yang sudah diperbarui, memiliki variabel `status_line` berisi status HTTP success. Selain itu, file hello.html sudah bisa tertampil di browser yang mana file ini dibaca oleh variabel `contents` dan di convert menjadi string. Pada akhir kode, terdapat variabel `response` yang mengindikasikan bahwa method akan menghasilkan HTTP response. 
