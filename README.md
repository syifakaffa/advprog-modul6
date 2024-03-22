# Modul 6 - Concurrency

**Commit 1 Reflection Notes**

Method `handle_connection` adalah sebuah fungsi dalam bahasa pemrograman Rust yang mengelola koneksi TCP dengan klien. Method ini akan menerima koneksi TCP sebagai argumen dan membaca permintaan HTTP dari klien yang terhubung. Method akan menggunakan `BufReader` untuk membaca data dari koneksi `TcpStream` dan menyimpannya dalam bentuk vektor `Vec<_>`. Data dibaca baris per baris hingga ditemukan baris kosong yang menandakan akhir permintaan HTTP. Selanjutnya, permintaan HTTP yang telah dibaca disimpan dalam vektor `http_request` dan ditampilkan ke konsol.

**Commit 2 Reflection Notes**
![Commit 2 screen capture](/assets/images/commit2.png)
Method `handle_connection` yang sudah diperbarui, memiliki variabel `status_line` berisi status HTTP success. Selain itu, file hello.html sudah bisa tertampil di browser yang mana file ini dibaca oleh variabel `contents` dan di convert menjadi string. Pada akhir kode, terdapat variabel `response` yang mengindikasikan bahwa method akan menghasilkan HTTP response. 

**Commit 3 Reflection Notes**
![Commit 3 screen capture](/assets/images/commit3.png)
Untuk meghandle dua response yang berbeda, kita bisa melakukan pemeriksaan apakah `request_line` yang ada sama dengan request line dari permintaan GET ke path / yang kita kirimkan di browser. Jika request_line nya sama, maka akan masuk ke blok if dan akan menampilkan konten pada file hello.html (`filename` nya menjadi hello.html). Jika permintaan GET nya tidak sama dengan request_line pada path / atau dengan kata lain tidak request yang diminta tidak ada, misalnya `127.0.0.1:7878/foooo`, maka akan masuk ke blok else dimana akan menampilkan konten pada file 404.html. 

Refactoring perlu dilakukan agar tidak terjadi duplikasi kode. Sebelum dilakukan refactoring, program pada blok if-else hanya memiliki perbedaan pada `status_line` dan `filename`. Selebihnya, kedua blok sama-sama melakukan pembacaan file html dan menulis konten pada file html tsb ke stream. Untuk itu, perlu dilakukan refactroing dengan membuat blok if-else hanya untuk meng-assign value status_line dan filename.


