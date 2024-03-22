# Modul 6: Rust Web Server

## Pradipta Arya Pramudita - 2206083685

### Commit 1

Fungsi `handle_connection` adalah mengelola data TCP dengan cara membaca data dari `TcpStream` melalui `BufReader` baris demi baris sampai menemukan baris kosong, yang menandakan akhir header HTTP. Data yang terkumpul kemudian ditampilkan, menjadikannya penting untuk mengumpulkan dan menunjukkan permintaan HTTP.

---

### Commit 2
Fungsi `handle_connection` telah direfaktorisasi untuk mencakup kode tambahan yang berfungsi untuk membuat dan mengirim respons HTTP ke client. Prosesnya dimulai dengan menetapkan baris status untuk menunjukkan respons berhasil dengan kode 200 OK. Lalu, isi dari file `hello.html` dibaca dan diubah menjadi `string`. Setelah itu, panjang konten dihitung dan digunakan untuk menangkap respons HTTP, yang mencakup `status_line`, `content-length`, serta isi dari file `hello.html`. Respons ini lalu dikirim kembali ke client melalui aliran TCP menggunakan metode `write_all()`. Secara singkat, fungsi ini sekarang dapat membaca isi `hello.html`, menyusun respons HTTP yang tepat, dan mengirimkannya kembali ke client.

![Commit 2 screen capture](/assets/images/commit2.png)

---

### Commit 3

Fungsi `handle_connection` telah direfaktorisasi untuk menangani permintaan HTTP yang tidak valid. Jika permintaan tidak valid, maka kode status `400 Bad Request` akan dikirimkan ke client. Kode status ini mengembalikan pesan yang menjelaskan bahwa permintaan tidak valid. Fungsi ini sekarang dapat menangani permintaan HTTP yang tidak valid dengan cara mengirimkan respons yang sesuai ke client.

![Commit 3 screen capture](/assets/images/commit3.png)

---

### Commit 4

Fungsi `/sleep` telah ditambahkan ke server. Fungsi ini akan menangani permintaan HTTP yang mengandung `/sleep`. Jika permintaan ditemukan, maka server akan menunggu selama 10 detik sebelum mengirimkan respons ke client. Fungsi ini dapat digunakan untuk menunjukkan bagaimana server dapat menangani permintaan HTTP yang membutuhkan waktu pemrosesan yang lebih lama.

---

### Commit 5

Implementasi `ThreadPool` dilakukan melalui pembuatan sebuah array `workers`, yang berisi thread yang akan digunakan untuk menangani permintaan HTTP. Setiap thread akan menjalankan fungsi `Worker::new(id, receiver)`, yang akan menginisialisasi thread dan mengembalikan `Worker` baru. Setiap `Worker` akan menerima `receiver` sebagai parameter, yang digunakan untuk menerima `Job` dari `ThreadPool`. Setiap `Worker` akan menjalankan loop yang akan menerima `Job` dari `receiver` dan menjalankannya. Dengan demikian, `ThreadPool` dapat menangani permintaan HTTP dengan cara yang lebih efisien.