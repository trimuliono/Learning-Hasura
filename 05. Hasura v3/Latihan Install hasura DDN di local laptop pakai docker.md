
# Memulai Cepat API Supergraph di Hasura

Dalam waktu singkat dan tanpa perlu menghubungkan sumber data, kita bisa menjalankan API supergraph secara lokal dan juga di-deploy ke Hasura DDN. 🚀

## Prasyarat
### Instalasi DDN CLI

#### Windows
1. Unduh installer DDN CLI terbaru untuk Windows.
2. Jalankan file `DDN_CLI_Setup.exe` dan ikuti petunjuk yang diberikan. Proses ini hanya memakan waktu sebentar.
3. Secara default, DDN CLI akan terinstal di `C:\Users\{Username}\AppData\Local\Programs\DDN_CLI`.
4. DDN CLI akan otomatis ditambahkan ke variabel lingkungan `%PATH%` sehingga kita bisa menggunakan perintah `ddn` langsung dari terminal.

### Instal Docker (untuk pengembangan lokal)

Workflow berbasis Docker membantu kita untuk mengembangkan API secara lokal tanpa perlu melakukan deploy ke Hasura DDN, membuat proses pengembangan lebih cepat. Pastikan kita memiliki Docker Compose versi 2.27.1 atau yang lebih baru.

### Validasi Instalasi

kita bisa memastikan DDN CLI telah terinstal dengan benar dengan menjalankan perintah:

```bash
ddn doctor
```

### Login melalui CLI
Perintah `ddn auth login` akan mengautentikasi sesi CLI kita dan memberikan akses ke sumber daya Hasura Cloud.

Saat menjalankan perintah ini, sebuah jendela browser akan terbuka, memungkinkan kita untuk login ke Hasura Cloud. Setelah login berhasil, kita akan diarahkan kembali ke sesi CLI dan siap melanjutkan pembuatan supergraph.

```bash
ddn auth login
```

## Inisialisasi Supergraph Baru di Direktori Baru
Perintah `ddn supergraph init` akan menginisialisasi supergraph — sebuah API gabungan — dengan mengatur semua file dan direktori yang diperlukan di dalam direktori baru, `mysupergraph`.

Setelah menjalankan perintah ini, CLI akan membuat file `Docker Compose`, file `.env` untuk menjalankan Hasura engine secara lokal, serta file konfigurasi lainnya. CLI juga akan membuat dua subgraph awal, yaitu `globals` dan `app`, sebagai awal untuk membangun API kita. Dengan setup ini, kita dapat memulai dan mengelola layanan supergraph secara lokal menggunakan Docker.

```bash
ddn supergraph init mysupergraph
cd mysupergraph
```

## Menghubungkan ke Data
Perintah `ddn connector init` menambahkan konektor data baru ke proyek supergraph.

Konektor data memungkinkan kita menghubungkan tipe sumber data tertentu (seperti PostgreSQL, MongoDB, MySQL, ClickHouse, dll.).

Di sini, kita akan menamakan konektor kita `my_connector`. Dengan menggunakan opsi `-i` (interaktif), kita akan diminta untuk memilih jenis konektor data dan memasukkan variabel lingkungan yang diperlukan, seperti detail koneksi sumber data. CLI akan membuat file yang berkaitan dengan konektor serta menambahkan objek metadata `DataConnectorLink` untuk menghubungkan konektor ini ke supergraph.

Tidak punya sumber data saat ini? kita bisa memilih konektor `hasura/postgres` yang secara default terhubung ke database Postgres contoh kami untuk dicoba. Atau, kita bisa mengikuti panduan ini untuk mengatur database Postgres lokal menggunakan Docker.

```bash
ddn connector init my_connector -i
```

## Mengintrospeksi Sumber Data
Perintah `ddn connector introspect` akan mengintrospeksi sumber data kita.

Proses ini akan membuat sekumpulan file konfigurasi yang menggambarkan sumber data dalam format yang ditentukan oleh konektor. Selain itu, proses ini akan memperbarui `DataConnectorLink` dengan sumber daya dari sumber data yang bisa diakses melalui API. Ini akan digunakan untuk menghasilkan metadata dari setiap sumber daya yang ditemukan selama introspeksi.

Jika `introspect` tidak berfungsi, pastikan variabel lingkungan yang didefinisikan dalam file `.env` sudah benar.

```bash
ddn connector introspect my_connector
```

## Menambahkan Sumber Daya
Langkah ini akan membuat metadata untuk model, perintah, dan hubungan di dalam supergraph kita. Metadata ini mengonfigurasi GraphQL API dan mengekspose entitas yang ada dalam sumber data — seperti tabel.

```bash
ddn model add my_connector '*'
ddn command add my_connector '*'
ddn relationship add my_connector '*'
```

## Membangun Supergraph untuk Engine Lokal
Perintah `ddn supergraph build local` akan membangun supergraph kita dan membuat aset lokal untuk menjalankan engine.

Langkah ini memungkinkan kita untuk membuat build API yang tidak dapat diubah yang bisa dijalankan secara lokal untuk diuji sebelum perubahan didorong ke kontrol versi atau dibuat dan di-deploy di cloud, baik di Hasura DDN atau infrastruktur mandiri.

```bash
ddn supergraph build local
```

## Menjalankan Supergraph
Perintah `ddn run docker-start` akan mengeksekusi skrip yang ada di dalam file `.hasura/context.yaml`.

Saat menjalankan perintah ini, Docker akan memulai layanan untuk supergraph, setiap konektor yang telah kita tambahkan, dan alat observasi lainnya.

kita bisa mengeksplorasi, memvisualisasikan, dan menguji supergraph menggunakan konsol Hasura DDN. Cukup jalankan perintah berikut atau akses melalui [https://console.hasura.io/local/graphql](https://console.hasura.io/local/graphql).

```bash
ddn console --local
```

Selamat! Pada titik ini, kita telah berhasil membuat supergraph pertamamu yang berfungsi sepenuhnya 🎉

## Deploy Supergraph ke Hasura DDN

Catatan: Sumber data kita harus bisa diakses dari internet agar bisa terhubung ke Hasura DDN.

```bash
ddn run docker-start
```

### Membuat Proyek di Hasura DDN
Perintah `ddn project init` akan menyediakan proyek baru di Hasura DDN untuk deploy supergraph.

CLI juga akan membuat file `.env.cloud` berdasarkan file `.env` yang berisi variabel lingkungan yang diperlukan, seperti string koneksi sumber data. CLI juga akan mengatur nama proyek di konteks lokal sehingga kita dapat menjalankan perintah dengan lebih sederhana. Terakhir, CLI akan menghasilkan subgraph `globals` dan `app` di proyek Hasura DDN kita.

```bash
ddn project init
```

### Membangun dan Deploy Supergraph
Menjalankan `ddn supergraph build create` akan membangun data connector dan supergraph, menjadikan API kita tersedia di Hasura DDN.

Perintah ini akan membangun setiap konektor data yang terkait dengan proyek, memperbarui variabel lingkungan untuk menyesuaikan URL konektor, dan membuat build supergraph yang tidak dapat diubah. kita bisa mengeksplorasi build ini di konsol DDN. Setelah siap, kita bisa menerapkan build ini sehingga API proyek kita bisa diakses melalui endpoint Hasura.

```bash
ddn supergraph build create
```
