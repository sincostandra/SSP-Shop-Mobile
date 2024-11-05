Tugas 7  
1. Stateless widget adalah widget yang tidak memiliki state yang dapat berubah, artinya tampilan dan behaviour widget ini bersifat statis setelah pembuatan, stateless widget cocok digunakan untuk konten yang tidak akan berubah selama aplikasi digunakan, seperti ikon, teks statis, gambar, dan lain-lain. Sedangkan Stateful Widget adalah widget yang memiliki state yang dapat berubah selama siklus aplikasi berjalan, artinya widget ini dapat merespon interaksi client, perubahan data, dan lain-lain.  
2. Widget yang digunakan dalam proyek ini antara lain:

    1. MaterialApp: Widget root yang menyediakan tema dan navigasi untuk aplikasi.  
    2. Scaffold: Menyediakan struktur dasar halaman, seperti `AppBar`, `body`, dan `FloatingActionButton`.  
    3. AppBar: Menampilkan bilah aplikasi di bagian atas dengan judul dan tindakan.  
    4. Padding: Menambahkan ruang di sekitar widget anaknya.  
    5. Column: Menyusun widget secara vertikal.  
    6. Row: Menyusun widget secara horizontal.  
    7. InfoCard: Widget kustom untuk menampilkan informasi dalam bentuk kartu.  
    9. Container: Widget untuk mengatur layout, termasuk padding, margin, dan ukuran.  
    10. Icon: Menampilkan ikon dari material design.  
    11. SnackBar: Menampilkan pesan notifikasi di bagian bawah layar.  
    12. dll

3. Fungsi setState() dalam Flutter digunakan untuk memberi tahu framework bahwa ada perubahan pada state dari sebuah StatefulWidget yang perlu diperbarui. Contoh variabel yang terdampak adalah items, ketika terdapat perubahan di itemhomepage, maka setState() harus dipanggil untuk memperbarui UI sesuai data terbaru  

4. final digunakan untuk variabel yang nilainya diinisialisasi sekali dan ditentukan saat runtime, sedangkan const digunakan untuk nilai yang konstan dan diketahui pada waktu kompilasi. Gunakan final untuk nilai yang tidak berubah setelah diinisialisasi tetapi ditentukan saat runtime, dan gunakan const` untuk nilai yang benar-benar konstan dan diketahui pada waktu kompilasi.  

Step by Step:
1. Buat sebuah aplikasi Flutter baru dengan menggunakan perintah `flutter create ssp_shop`  
2. Pada direktori lib, buat file baru bernama menu.dart untuk menyimpan menu yang akan ditampilkan di main  
3. Di menu.dart, buat widget ItemHomepage dan ItemCard, tambahkan juga atribut warna pada widget ItemHomePage, buat list items yang beirisi button-button dan panggil komponen ItemHomePage yg sudah dibuat ke main  
4. Untuk mengimplementasikan warna yang berbeda, ubah nilai/value colors di list items yang sudah dibuat tadi, dan ganti color pada ItemCard menjadi item.color  
5. Buat juga kode yang akan menampilkan snackbar ketika button dipencet (onTap)  