Smart Lab
Sistem Peminjaman dan Pengelolaan Kunci Laboratorium Berbasis RFID dan
Website

Smart Lab adalah proyek sistem peminjaman kunci laboratorium yang
mengintegrasikan teknologi RFID, ESP32, kunci solenoid elektrik,
dan website. Sistem ini dirancang untuk membantu pengurus laboratorium
mencatat aktivitas peminjaman dan pengembalian kunci secara digital,
memantau kondisi loker, serta mengetahui siapa yang sedang menggunakan
kunci laboratorium.

Proyek ini dikembangkan sebagai prototype untuk lingkungan laboratorium
Teknik Komputer dan Jaringan (TKJ).
Daftar Isi
- Latar Belakang
- Tujuan
- Fitur Utama
- Gambaran Sistem
- Alur Peminjaman dan
  Pengembalian
- Peran Pengguna
- Perangkat Keras
- Teknologi yang Digunakan
- Gambaran Arsitektur
- Data yang Dikelola
- Keamanan dan Penanganan Darurat
- Rencana Pengembangan
- Catatan Prototype
Latar Belakang
Peminjaman kunci laboratorium yang dilakukan secara manual dapat
menimbulkan beberapa kendala, seperti pencatatan peminjaman yang tidak
konsisten, kesulitan mengetahui pihak yang sedang memegang kunci,
keterlambatan pengembalian, serta kurangnya informasi mengenai
ketersediaan laboratorium.

Smart Lab dikembangkan untuk membantu mengatasi kendala tersebut melalui
proses identifikasi kartu RFID dan pencatatan terpusat pada website.
Dengan sistem ini, aktivitas peminjaman dan pengembalian dapat direkam
secara digital sehingga pengurus laboratorium lebih mudah melakukan
pemantauan.
Tujuan
1. Mendigitalisasi proses peminjaman dan pengembalian kunci
   laboratorium.
2. Mengidentifikasi pengguna menggunakan kartu RFID.
3. Mengontrol akses loker kunci menggunakan solenoid elektrik.
4. Menampilkan status ketersediaan dan penggunaan kunci melalui
   website.
5. Menyimpan riwayat transaksi agar dapat diperiksa oleh pengurus
   laboratorium.
Fitur Utama
- Identifikasi RFID: pengguna melakukan pemindaian kartu RFID yang
  telah terdaftar.
- Akses loker: sistem memproses kartu dan mengaktifkan solenoid
  pada loker yang sesuai apabila transaksi diizinkan.
- Peminjaman dan pengembalian: kartu yang sama digunakan untuk
  mencatat peminjaman dan pengembalian pada loker asal.
- Monitoring website: menampilkan status setiap loker, informasi
  pengguna yang sedang meminjam, dan riwayat transaksi.
- Pengelolaan data: pengurus dapat mengelola data pengguna,
  loker/laboratorium, dan riwayat peminjaman sesuai hak akses.
- Pencatatan otomatis: data transaksi dikirim dari ESP32 ke server
  untuk disimpan dalam basis data.
Gambaran Sistem
Prototype Smart Lab menggunakan dua loker yang mewakili dua
laboratorium:

  Loker   Laboratorium   Kunci
  1       LAB TKJ 1      1 kunci
2       LAB TKJ 2      1 kunci

Setiap loker memiliki satu RFID reader dan satu solenoid. Pengguna
mendatangi loker laboratorium yang dituju dan menempelkan kartu RFID
pada reader di loker tersebut. Pengguna tidak perlu memilih laboratorium
melalui website atau menu perangkat karena lokasi reader sudah
menunjukkan loker yang akan digunakan.

Prototype dirancang untuk melayani 9 siswa dan 3 pengurus
laboratorium. Seluruh pengguna menggunakan kartu RFID yang telah
didaftarkan ke sistem.
Alur Peminjaman dan Pengembalian
Peminjaman
1. Siswa mendatangi loker laboratorium yang ingin digunakan.
2. Siswa menempelkan kartu RFID terdaftar pada reader di loker
   tersebut.
3. ESP32 membaca UID kartu dan mengirimkan data ke server melalui
   jaringan Wi-Fi.
4. Server memeriksa identitas pengguna, hak akses, dan status loker.
5. Jika transaksi diizinkan, sistem mengaktifkan solenoid untuk
   melepaskan pengunci loker.
6. Siswa membuka loker secara manual dan mengambil kunci laboratorium.
7. Sistem menyimpan transaksi peminjaman dan memperbarui status pada
   website.
Pengembalian
1. Pengguna kembali ke loker tempat kunci dipinjam.
2. Pengguna menempelkan kartu RFID yang sama pada reader.
3. Sistem memeriksa transaksi aktif pengguna pada loker tersebut.
4. Jika pengembalian valid, solenoid melepaskan pengunci agar loker
   dapat dibuka.
5. Pengguna memasukkan kembali kunci dan menutup loker secara manual.
6. Sistem mencatat waktu pengembalian dan memperbarui status loker pada
   website.
Catatan: Solenoid berfungsi sebagai pengunci/pembuka kunci
elektrik, bukan sebagai motor pembuka atau penutup pintu. Pintu loker
tetap dibuka dan ditutup secara manual oleh pengguna.

Peran Pengguna
1. Siswa
- Menggunakan kartu RFID yang telah terdaftar.
- Melakukan peminjaman kunci melalui reader pada loker laboratorium.
- Mengembalikan kunci pada loker tempat peminjaman.
- Melihat informasi ketersediaan laboratorium melalui website.
2. Pengurus Laboratorium (Admin)
- Login ke halaman administrasi website.
- Memantau status loker dan penggunaan kunci.
- Melihat identitas peminjam serta waktu peminjaman dan pengembalian.
- Mengelola data pengguna dan data laboratorium/loker.
- Melihat dan mengelola riwayat transaksi.
- Melakukan penanganan manual sesuai prosedur ketika terjadi keadaan
  darurat.
Prototype direncanakan menggunakan tiga akun/kartu pengurus laboratorium
dan sembilan akun/kartu siswa.
Perangkat Keras
Komponen utama yang digunakan atau direncanakan dalam prototype:
  Komponen                            Fungsi
  ESP32                               Pengendali utama dan penghubung
perangkat dengan server melalui
Wi-Fi

  RFID Reader MFRC522 (2 unit)        Membaca kartu RFID pada
masing-masing loker

  Kartu RFID                          Identitas siswa dan pengurus
laboratorium

  Solenoid Door Lock 12V (2 unit)     Mengunci dan melepaskan pengunci
loker secara elektrik

  Modul relay                         Mengendalikan suplai daya ke
solenoid

  Sensor pintu magnetik               Membaca kondisi pintu loker terbuka
atau tertutup

  Microswitch                         Mendeteksi kondisi/posisi komponen
mekanis yang ditentukan pada
rancangan

  LCD 16x2 I2C                        Menampilkan informasi proses pada
perangkat

  Buzzer                              Memberikan notifikasi suara

  LED indikator                       Menampilkan indikator status proses
Catu daya                           Menyediakan tegangan sesuai
kebutuhan rangkaian
Jumlah dan spesifikasi komponen dapat disesuaikan dengan hasil perakitan
serta pengujian prototype.
Teknologi yang Digunakan
  Teknologi               Kegunaan
  MicroPython             Pemrograman ESP32
Thonny IDE              Menulis dan mengunggah program MicroPython ke ESP32
PHP                     Pemrosesan data pada sisi server/API
Laravel                 Pengembangan website dan pengelolaan aplikasi
MySQL                   Penyimpanan data pengguna, loker, dan transaksi
HTML, CSS, JavaScript   Antarmuka website
Wi-Fi                   Komunikasi ESP32 dengan server
HTTP/REST API           Pertukaran data antara ESP32 dan server

Catatan implementasi: program ESP32 direncanakan menggunakan
MicroPython melalui Thonny, sedangkan aplikasi website menggunakan
Laravel dan basis data MySQL. Detail endpoint API dan struktur tabel
mengikuti implementasi kode yang digunakan pada tahap pengembangan.
Gambaran Arsitektur
Secara umum, aliran komunikasi Smart Lab adalah:
Kartu RFID Pengguna
        |
        v
RFID Reader pada Loker
        |
        v
      ESP32
        |
        | Wi-Fi
        v
 Router / Access Point
        |
        v
 Server Sekolah
        |
        +------ Aplikasi Laravel / API
        |
        +------ Database MySQL
        |
        v
 Website Smart Lab
        |
        +------ Halaman Informasi
        |
        +------ Dashboard Admin
ESP32 membaca kartu dari reader pada loker, kemudian mengirimkan
informasi yang diperlukan ke server. Server memvalidasi transaksi dan
menyimpan hasilnya ke MySQL. Website mengambil data dari server untuk
menampilkan informasi penggunaan dan riwayat.

Server direncanakan memanfaatkan server milik sekolah, sedangkan koneksi
perangkat menggunakan jaringan Wi-Fi sekolah. Konfigurasi jaringan akhir
mengikuti kebijakan dan fasilitas jaringan sekolah.
Data yang Dikelola
Secara konseptual, sistem membutuhkan data berikut:
- Data pengguna: identitas pengguna, jenis/peran pengguna, dan UID
  kartu RFID.
- Data loker/laboratorium: nama laboratorium, identitas loker, dan
  status penggunaan.
- Data transaksi: pengguna, loker, waktu peminjaman, waktu
  pengembalian, dan status transaksi.
- Data administrator: akun untuk mengakses halaman pengelolaan
  website.
UID kartu digunakan sebagai identitas RFID. Data pribadi yang
ditampilkan pada website sebaiknya dibatasi sesuai kebutuhan pemantauan
dan hak akses pengguna.
Keamanan dan Penanganan Darurat
- Hanya kartu RFID yang telah terdaftar dan memenuhi aturan sistem
  yang dapat melakukan transaksi.
- Sistem harus memeriksa status transaksi agar satu loker tidak
  dipinjam secara bersamaan oleh pengguna yang berbeda.
- Halaman administrasi dilindungi dengan autentikasi admin.
- Solenoid dan rangkaian kontrol harus menggunakan catu daya sesuai
  spesifikasi komponen.
- Pengurus laboratorium perlu memiliki prosedur pembukaan manual
  apabila terjadi gangguan listrik atau kerusakan sistem.
- Mekanisme pembukaan darurat harus dapat diakses oleh petugas yang
  berwenang dan tidak menghilangkan fungsi pengamanan dalam penggunaan
  normal.
Rencana Pengembangan
Pengembangan selanjutnya dapat mencakup:
1. Penyempurnaan validasi transaksi peminjaman dan pengembalian.
2. Penambahan notifikasi apabila kunci belum dikembalikan melewati
   batas waktu.
3. Penyempurnaan laporan dan ekspor riwayat transaksi.
4. Pengujian kestabilan komunikasi ESP32 dengan server.
5. Pengujian sensor pintu, relay, dan solenoid dalam berbagai kondisi.
6. Pengembangan sistem dari dua loker prototype ke lebih banyak
   laboratorium.
Catatan Prototype
Smart Lab pada tahap ini merupakan prototype dengan dua loker, yaitu
LAB TKJ 1 dan LAB TKJ 2. Sistem menggunakan kartu RFID untuk siswa
maupun pengurus laboratorium. Pengguna melakukan pemindaian langsung
pada reader di loker yang dituju; pemilihan laboratorium tidak dilakukan
melalui website.

Fungsi utama prototype adalah mendemonstrasikan identifikasi pengguna,
proses peminjaman dan pengembalian, kontrol pengunci elektrik,
pengiriman data ke server, serta pemantauan melalui website.
Implementasi akhir dapat mengalami penyesuaian berdasarkan hasil
pengujian dan kebutuhan sekolah.
Nama Proyek: Smart Lab
Jenis Proyek: Prototype IoT dan Website
Bidang: Sistem Peminjaman Kunci Laboratorium
Lingkungan Implementasi: Laboratorium TKJ
