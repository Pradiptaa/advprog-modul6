# Modul 6: Rust Web Server

### Commit 1

Fungsi handle_connection adalah mengelola data TCP dengan cara membaca data dari TcpStream melalui BufReader baris demi baris sampai menemukan baris kosong, yang menandakan akhir header HTTP. Data yang terkumpul kemudian ditampilkan, menjadikannya penting untuk mengumpulkan dan menunjukkan permintaan HTTP.