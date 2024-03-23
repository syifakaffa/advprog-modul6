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

**Commit 4 Reflection Notes**

Ketika user mengakses halaman http://127.0.0.1:7878/sleep terdapat delay sekitar 10 detik karena pada kode program telah disetel thread sleep yang akan menghentikan thread sementara. Sedangkan ketika saya mengakses http://127.0.0.1:7878 pada browser, aplikasi memberikan respon tanpa delay (tidak ada pemberian thread sleep).

**Commit 5 Reflection Notes**

ThreadPool adalah kumpulan dari beberapa thread yang telah dipersiapkan dan siap digunakan untuk mengeksekusi tugas-tugas yang diberikan kepadanya. Thread dalam ThreadPool dapat digunakan kembali untuk menangani berbagai tugas secara bersamaan (concurrent), menghindari overhead pembuatan thread baru setiap kali sebuah tugas masuk. 

ThreadPool bekerja dengan cara mengelola antrian tugas (task queue) dan menugaskan tugas-tugas tersebut kepada thread yang tersedia dalam pool. Ketika suatu tugas selesai dieksekusi, thread akan kembali ke pool untuk digunakan kembali untuk tugas berikutnya. Dengan demikian, ThreadPool membantu mengoptimalkan penggunaan sumber daya sistem dan meningkatkan efisiensi dalam menangani banyak tugas secara bersamaan.

**Commit 6 Reflection Notes BONUS**

Dokumentasi rust pada modul 12.3 mengenai refactoring memberikan saran untuk lebih menggunakan method `build` pada saat melakukan inisialisasi ThreadPoll dibandingkan dengan menggunakan method `new` yang telah tutorial jelaskan sebelumnya. Penggunaan method `build` ini lebih direkomendasikan sebab dapat menghandle jikalau suatu saat permintaan requestnya failed (tidak sukses). Jika kita menggunakan `new` lalu pada suatu saat kita dihadapkan pada kondisi jumlah ThreadPool yang terlalu kecil, maka program akan mengalami error sebab method `new` ini hanya diekspektasikan untuk succes. Oleh karena itu perlu melakukan refactoring menggunakan method `build` agar bisa menghandle kondisi tersebut yang mana method build ini akan me return hasil dan nanti ketika value nya di kembalikan ke caller, kita bisa membuka wrapper nya untuk mendapatkan value dari si result tadi.