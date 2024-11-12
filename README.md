Tugas 8
1. Apa kegunaan const di Flutter? Jelaskan apa keuntungan ketika menggunakan const pada kode Flutter. Kapan sebaiknya kita menggunakan const, dan kapan sebaiknya tidak digunakan?  
const digunakan untuk mendefinisikan nilai konstan yang tidak akan berubah selama runtime. Di Flutter, const sering digunakan untuk mendeklarasikan widget yang tidak perlu dibangun ulang setiap kali widget tree di-render ulang, sehingga meningkatkan efisiensi aplikasi. const sebaiknya digunakan untuk widget yang tidak akan berubah spt teks statis atau nilai konstan, sedangkan jika widgetnya sering update maka tidak disarankan menggunakan const  

2. | Aspek | Column | Row |
|-------|---------|-----|
| Arah Penataan | Vertikal (Atas ke Bawah) | Horizontal (Kiri ke Kanan) |
| Properti Utama | mainAxisAlignment, crossAxisAlignment | mainAxisAlignment, crossAxisAlignment |
| Penggunaan Umum | Daftar item, form input, konten vertikal lainnya | Menu navigasi, tombol berdampingan, baris ikon |

implementasi column:  
``` dart
import 'package:flutter/material.dart';

class ColumnExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Contoh Column'),
      ),
      body: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: <Widget>[
          Text('Widget Pertama'),
          SizedBox(height: 10),
          Text('Widget Kedua'),
          SizedBox(height: 10),
          ElevatedButton(
            onPressed: () {},
            child: Text('Tombol'),
          ),
        ],
      ),
    );
  }
}   
```

implementasi row: 
``` dart 
import 'package:flutter/material.dart';

class RowExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Contoh Row'),
      ),
      body: Row(
        mainAxisAlignment: MainAxisAlignment.center,
        children: <Widget>[
          Icon(Icons.star, color: Colors.red),
          SizedBox(width: 10),
          Icon(Icons.star, color: Colors.green),
          SizedBox(width: 10),
          Icon(Icons.star, color: Colors.blue),
        ],
      ),
    );
  }
}   
```
3. Sebutkan apa saja elemen input yang kamu gunakan pada halaman form yang kamu buat pada tugas kali ini. Apakah terdapat elemen input Flutter lain yang tidak kamu gunakan pada tugas ini? Jelaskan! 
    Elemen input yang digunakan:  
    
    TextFormField untuk Product:  
    Digunakan untuk memasukkan nama produk.  
    Validasi: Tidak boleh kosong.  

    TextFormField untuk Amount:  
    Digunakan untuk memasukkan jumlah produk.
    Validasi:
    Tidak boleh kosong.  
    Harus berupa angka.  
    Tidak boleh non-positif.  

    TextFormField untuk Description:  
    Digunakan untuk memasukkan deskripsi produk.  
    Validasi: Tidak boleh kosong.  

    ElevatedButton untuk Save:  
    Digunakan untuk menyimpan data produk setelah validasi berhasil.

    Elemen input yang tidak digunakan:  
    DropdownButton:
    Fungsi: Menyediakan pilihan dropdown untuk memilih satu opsi dari daftar.  

    DropdownButton:
    Fungsi: Menyediakan pilihan dropdown untuk memilih satu opsi dari daftar.

    dan lain-lain

4. Bagaimana cara kamu mengatur tema (theme) dalam aplikasi Flutter agar aplikasi yang dibuat konsisten? Apakah kamu mengimplementasikan tema pada aplikasi yang kamu buat?  
Pada main.dart, ubah colorScheme pada ThemeData, pada tugas kali ini aku set warnanya jadi green (primar) dan green[200] (secondary), tidak lupa mengatur useMaterial:3. Sekarang ketika aku membutuhkan warna maka aku tinggal panggil saja ColorScheme-nya  

5. Bagaimana cara kamu menangani navigasi dalam aplikasi dengan banyak halaman pada Flutter?  
Untuk mengimplementasikan navigasi pada Flutter, sudah disediakan sistem untuk melakukan navigasi antar halaman. Salah satu caranya dengan menggunakan widget Navigator. Widget Navigator menampilkan halaman-halaman yang ada kepada layar seakan sebagai sebuah tumpukan (stack). Untuk menavigasi sebuah halaman baru, kita dapat mengakses Navigator melalui BuildContext dan memanggil fungsi yang ada, seperti misalnya push(), pop(), serta pushReplacement().  

Salah satu contoh implementasi dengan Navigator:  
``` dart
// Navigasi ke halaman baru
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => HalamanBaru()),
);

// Kembali ke halaman sebelumnya
Navigator.pop(context);
```  

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