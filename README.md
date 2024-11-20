Tugas 9  
1.  Jelaskan mengapa kita perlu membuat model untuk melakukan pengambilan ataupun pengiriman data JSON? Apakah akan terjadi error jika kita tidak membuat model terlebih dahulu?  

Pentingnya Membuat Model untuk JSON di Flutter  
Keuntungan Membuat Model  
Struktur Data Jelas: Model mendefinisikan struktur JSON secara eksplisit, membuat kode lebih terorganisir.  
Type Safety: Mencegah error runtime dengan memastikan data sesuai tipe yang diharapkan.
Parsing & Serialisasi Mudah: Metode fromJson dan toJson menyederhanakan konversi JSON ke objek Dart dan sebaliknya.  
Maintainability: Perubahan struktur data hanya perlu dilakukan di model, tidak tersebar di seluruh kode.  
Auto-Completion: Memanfaatkan fitur IDE untuk meningkatkan produktivitas dan mengurangi kesalahan.  
Risiko Tanpa Model  
Kode Tidak Terstruktur: Parsing langsung dengan map/dynamic membuat kode sulit dibaca.
Kurangnya Type Safety: Meningkatkan risiko error runtime.  
Parsing Kompleks: Memerlukan penanganan manual setiap field.    

2.  Jelaskan fungsi dari library http yang sudah kamu implementasikan pada tugas ini    

Library http digunakan untuk komunikasi antara aplikasi Flutter dan API Django di backend. Fungsinya meliputi:  

Mengambil Data (GET Request): Mengambil daftar produk atau informasi lain dari server.  
Mengirim Data (POST Request): Mengirim data baru, seperti produk atau formulir   pengguna, ke server.  
Autentikasi: Mengelola login dan registrasi pengguna dengan mengirim kredensial ke server.  
Dengan http, aplikasi dapat melakukan operasi CRUD dan autentikasi secara efisien, memungkinkan integrasi penuh antara frontend dan backend.    

3. Jelaskan fungsi dari CookieRequest dan jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.    
CookieRequest dari library pbp_django_auth mengelola autentikasi berbasis cookie dengan fungsi utama:  
Autentikasi: Menangani login/logout dan menyimpan cookie sesi.  
Pengelolaan Sesi: Memastikan sesi pengguna tetap aktif untuk akses API backend.  
Permintaan Terautentikasi: Menyertakan cookie sesi otomatis untuk setiap permintaan HTTP.  

4.  Jelaskan mekanisme pengiriman data mulai dari input hingga dapat ditampilkan pada Flutter.  

Mekanisme Pengiriman Data di Flutter  
Input Pengguna:  
Pengguna mengisi data melalui widget seperti TextFormField, yang disimpan dalam TextEditingController.   

Pengiriman Data:  
Data dikirim ke backend Django menggunakan CookieRequest melalui permintaan POST atau GET.  

Proses Backend:  
Django memproses permintaan, seperti autentikasi atau penyimpanan data, dan mengembalikan respons JSON.  

Penanganan Respons:  
Flutter memproses respons untuk menampilkan notifikasi, mengarahkan pengguna, atau memperbarui data di aplikasi.   

Penampilan Data:  
Data dari backend diubah menjadi model Dart dan ditampilkan menggunakan widget seperti ListView atau GridView.  
 
Pembaruan UI:
Tampilan diperbarui dengan setState() atau state management lainnya.  

5. Jelaskan mekanisme autentikasi dari login, register, hingga logout. Mulai dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.  
Register:  

Pengguna mengisi formulir di Flutter, data dikirim ke Django melalui CookieRequest dengan endpoint auth/register/.  
Django memvalidasi dan membuat akun, lalu mengirim respons sukses.  
Flutter menampilkan notifikasi dan mengarahkan pengguna ke halaman login.  
Login:  

Pengguna memasukkan kredensial, data dikirim ke endpoint auth/login/.  
Django memverifikasi data, mengembalikan status login.  
Jika berhasil, sesi disimpan dan pengguna diarahkan ke halaman utama. Jika gagal, ditampilkan pesan error.  
Logout:  

Flutter mengirim permintaan logout ke endpoint auth/logout/.  
Django menghapus sesi pengguna, lalu mengembalikan status logout.  
Pengguna diarahkan ke halaman login.  
Navigasi dan Sesi:  

Sesi dikelola otomatis oleh CookieRequest. UI diperbarui menggunakan state management untuk memastikan pengalaman autentikasi yang konsisten.  

6. Step-by-Step:  

### Setup Autentikasi pada Django untuk Flutter  
1. **Buat Aplikasi Django untuk Autentikasi:**
   - Buat sebuah django-app bernama `authentication` dalam project Django yang telah dibuat sebelumnya.

2. **Konfigurasi `settings.py`:**
   - Tambahkan `authentication` ke dalam `INSTALLED_APPS`.
   - Instal library `django-cors-headers` dan tambahkan ke `INSTALLED_APPS` serta `MIDDLEWARE`.
   - Tambahkan konfigurasi CORS dan keamanan sesi, seperti `CORS_ALLOW_ALL_ORIGINS`, `CORS_ALLOW_CREDENTIALS`, `CSRF_COOKIE_SECURE`, `SESSION_COOKIE_SECURE`, `CSRF_COOKIE_SAMESITE`, dan `SESSION_COOKIE_SAMESITE`.

3. **Sesuaikan `ALLOWED_HOSTS`:**
   - Tambahkan `10.0.2.2` (namun saya ubah ke localhost:8000, karena yg 10.0.2.2 error) ke dalam daftar `ALLOWED_HOSTS` untuk memungkinkan integrasi dengan emulator Android.

4. **Buat Metode View untuk Login:**
   - Implementasikan metode view di `authentication/views.py` yang menangani proses autentikasi pengguna, termasuk validasi kredensial dan pengelolaan sesi.

5. **Atur Rute URL:**
   - Buat file `urls.py` dalam folder `authentication` dan tambahkan routing untuk endpoint `login/`.
   - Tambahkan path `auth/` yang menginklusi `authentication.urls` pada file `urls.py` utama project Django.  

### Integrasi Sistem Autentikasi pada Flutter  
 1. **Instalasi Package**
   - Tambahkan package `provider` dan `pbp_django_auth` ke proyek Flutter menggunakan perintah `flutter pub add`.

 2. **Konfigurasi Root Widget**
   - Modifikasi root widget di `main.dart` untuk menyediakan instance `CookieRequest` ke seluruh komponen aplikasi menggunakan `Provider`.

 3. **Buat Halaman Login**
   - Buat berkas `login.dart` di folder `screens` dan implementasikan halaman login yang memanfaatkan `CookieRequest` untuk autentikasi pengguna.

 4. **Atur Navigasi ke LoginPage**
   - Ubah widget `MaterialApp` di `main.dart` agar halaman awal aplikasi adalah `LoginPage`.

 5. **Tambah Fungsi Register**
   - Modifikasi modul authentication di Django untuk menambahkan metode view register.
   - Buat berkas `register.dart` di Flutter untuk halaman pendaftaran yang terhubung dengan backend Django.  

### Pembuatan Model Kustom

Untuk membuat model yang sesuai dengan data JSON, Anda dapat menggunakan situs web Quicktype dengan langkah-langkah berikut:

1. **Persiapan Data JSON:**
   - Buka endpoint JSON yang telah dibuat sebelumnya.
   - Salin data JSON tersebut.

2. **Menggunakan Quicktype:**
   - Kunjungi situs web Quicktype.
   - Atur `setup name` menjadi `productEntry`, `source type` menjadi `JSON`, dan `language` menjadi `Dart`.
   - Tempel data JSON yang telah disalin ke dalam textbox.
   - Klik opsi "Copy Code" untuk mendapatkan kode model Dart.

3. **Integrasi ke Proyek Flutter:**
   - Buat folder `models/` di dalam direktori lib.  
   - Buat file `product_entry.dart` dan tempelkan kode model yang telah disalin dari Quicktype.

### Penerapan Fetch Data dari Django untuk Ditampilkan di Flutter

#### Menambahkan Dependensi HTTP

Untuk melakukan permintaan HTTP, tambahkan package `http` ke dalam proyek Flutter dengan menjalankan perintah `flutter pub add http`. Selain itu, pastikan untuk mengizinkan akses internet dengan menambahkan izin di file `AndroidManifest.xml`.

#### Melakukan Fetch Data dari Django

1. **Membuat Halaman Baru:**
   - Buat file `list_productentry.dart` di dalam direktori screens.  

2. **Impor Library yang Diperlukan:**
   - Impor library Flutter, model `productEntry`, dan widget pendukung lainnya.

3. **Implementasi Fetch Data:**
   - Buat fungsi `fetchproduct` yang melakukan permintaan GET ke endpoint Django.
   - Decode respons JSON dan konversi menjadi objek `productEntry`.
   - Tampilkan data menggunakan widget seperti `ListView.builder`.

4. **Integrasi dengan Navigasi:**
   - Tambahkan halaman `ProductEntryPage` ke dalam menu navigasi dengan menambahkan `ListTile` baru.
   - Pastikan navigasi mengarahkan ke halaman `ProductEntryPage` saat opsi "Daftar product" dipilih.  

### Integrasi Form Flutter Dengan Layanan Django

Langkah-langkah berikut akan dilakukan pada kode proyek Django dan Flutter untuk mengintegrasikan form produk.

#### Pada Proyek Django

1. **Buat Fungsi View Baru:**
   - Tambahkan fungsi view baru di `main/views.py` yang menangani pembuatan produk.
   - Pastikan untuk mengimpor modul yang diperlukan seperti `csrf_exempt`, `json`, dan `JsonResponse`.

2. **Atur URL Routing:**
   - Tambahkan path baru di `main/urls.py` untuk mengakses fungsi view yang telah dibuat, misalnya `path('create-flutter/', create_product_flutter, name='create_product_flutter')`.

3. **Deploy Ulang Aplikasi Django:**
   - Jalankan ulang aplikasi Django untuk menerapkan perubahan. Jika aplikasi telah dideploy, perhatikan bahwa data akun dan produk mungkin akan hilang setelah redeploy.

#### Pada Proyek Flutter

1. **Hubungkan dengan CookieRequest:**
   - Di file `productentry_form.dart`, hubungkan halaman dengan `CookieRequest` menggunakan `context.watch<CookieRequest>()`.

2. **Modifikasi Tombol Submit:**
   - Ubah fungsi `onPressed` pada tombol submit untuk mengirim data produk ke endpoint Django yang telah dibuat.
   - Pastikan untuk mengganti `[URL_APP_KAMU]` dengan URL aplikasi Django Anda dan sesuaikan field data jika diperlukan.

3. **Perbaiki Impor yang Bermasalah:**
   - Lakukan quick fix pada baris impor yang diperlukan agar semua dependensi terhubung dengan benar.

4. **Jalankan Aplikasi:**
   - Jalankan ulang aplikasi Flutter dan coba tambahkan produk baru melalui form yang telah diintegrasikan. Pastikan produk tersebut tersimpan di backend Django.

### Implementasi Fitur Logout

#### Pada Proyek Django

1. **Buat Metode View Logout:**
   - Tambahkan metode view untuk logout di `authentication/views.py`.
   - Pastikan untuk mengimpor `logout` dari `django.contrib.auth`.

2. **Atur URL Routing Logout:**
   - Tambahkan path baru di `authentication/urls.py` untuk mengakses fungsi logout, misalnya `path('logout/', logout, name='logout')`.

#### Pada Proyek Flutter

1. **Tambahkan Fitur Logout pada UI:**
   - Buka file `widgets/product_card.dart` dan tambahkan logika untuk menangani tindakan logout.
   - Ubah fungsi `onTap` menjadi asinkronus dan tambahkan kondisi untuk menangani proses logout.

2. **Tampilkan Notifikasi dan Navigasi:**
   - Setelah berhasil logout, tampilkan notifikasi kepada pengguna dan arahkan mereka kembali ke halaman login.

3. **Verifikasi Fitur Logout:**
   - Jalankan ulang aplikasi Flutter dan lakukan proses logout untuk memastikan bahwa sesi pengguna telah dihapus dan navigasi berfungsi dengan baik.  

### Detail Product  
Pada halaman daftar produk (ProductEntryPage), setiap item produk dalam daftar dibuat menggunakan ListView.builder. Untuk memungkinkan pengguna melihat detail produk ketika mereka mengetuk salah satu item, saya membungkus setiap item produk dengan widget GestureDetector.  

Nah, di dalam GestureDetector, saya menggunakan fungsi Navigator.push. Fungsi ini akan mengarahkan pengguna ke halaman detail produk (ProductDetailPage) dan juga mengoper data produk yang dipilih. Contohnya seperti ini:  

```dart
Copy code
onTap: () {
  Navigator.push(
    context,
    MaterialPageRoute(
      builder: (context) => ProductDetailPage(
        product: snapshot.data![index], // Data produk yang dipilih
      ),
    ),
  );
},
```
Ketika pengguna mengetuk suatu produk, data produk yang terkait (snapshot.data![index]) akan diambil, lalu dikirim ke halaman detail melalui parameter konstruktor ProductDetailPage.  

Di halaman detail (ProductDetailPage), saya menerima data produk tersebut melalui parameter product. Dengan data ini, saya bisa menampilkan informasi detail seperti nama produk, harga, deskripsi, dan sebagainya. Saya juga menggunakan beberapa elemen visual seperti Text dan Row untuk menata informasi tersebut.









Tugas 8
1. Apa kegunaan const di Flutter? Jelaskan apa keuntungan ketika menggunakan const pada kode Flutter. Kapan sebaiknya kita menggunakan const, dan kapan sebaiknya tidak digunakan?  
const digunakan untuk mendefinisikan nilai konstan yang tidak akan berubah selama runtime. Di Flutter, const sering digunakan untuk mendeklarasikan widget yang tidak perlu dibangun ulang setiap kali widget tree di-render ulang, sehingga meningkatkan efisiensi aplikasi. const sebaiknya digunakan untuk widget yang tidak akan berubah spt teks statis atau nilai konstan, sedangkan jika widgetnya sering update maka tidak disarankan menggunakan const  

2. 
| Aspek | Column | Row |
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