# Analisa Hasura dari Panel Grafana

## Overview

Pada tugas latihan kali ini kita diminta untuk menganalisa tiap panel grafana yang ada pada 2 dashboard hasura, yaitu 
- Hasura HTTP GraphQL
- Hasura Health

## 1. Hasura HTTP GraphQL Dashboard - Panel
Pada dashboard pertama ini terdapat 3 group panel yaitu:
- `Overview`, didalamnya terdapat 7 panels
- `GraphQL Metrics`, didalamnya terdapat 6 panels. dan
- `General Metrics`, didalamnya terdapat 4 panels.
  
![image](https://github.com/user-attachments/assets/48ddef2d-a6de-4fd4-9845-b580ac987b2c)

## 2. Hasura Health Dashboard - Panel
Dokumentasi ini memberikan penjelasan detail untuk setiap panel di dashboard Hasura Health yang ditampilkan di Grafana. Setiap panel memantau metrik kesehatan tertentu yang terkait dengan Hasura GraphQL Engine, memungkinkan administrator mengukur status dan kinerja sistem.

Pada dashboard ini terdapat 7 panels.

### 1. **Status Metadata**
   - **Deskripsi:** Panel ini menampilkan status konsistensi metadata Hasura saat ini. 
   - **Nilai yang Mungkin:**
     - `CONSISTENT` (hijau): Metadata konsisten dan tersinkronisasi di seluruh sistem Hasura.
     - `INCONSISTENT` (merah atau lainnya): Metadata memiliki perbedaan atau tidak sepenuhnya tersinkronisasi.
   - **Penggunaan:** Administrator harus memastikan bahwa metadata selalu `CONSISTENT`. Ketidakkonsistenan mungkin menunjukkan masalah dengan skema atau sinkronisasi sistem.

### 2. **Health Check Menggunakan Infinity**
   - **Deskripsi:** Panel ini menampilkan status pemeriksaan kesehatan koneksi Hasura ke datasource Infinity.
   - **Nilai yang Mungkin:**
     - `OK` (hijau): Koneksi ke datasource Infinity berjalan sehat.
     - `No Data` (merah): Tidak ada data untuk pemeriksaan kesehatan, yang mungkin menunjukkan masalah.
   - **Penggunaan:** Koneksi yang sehat ke datasource Infinity sangat penting untuk fungsi Hasura. Status `No Data` menunjukkan bahwa mungkin ada masalah konektivitas atau konfigurasi.

### 3. **Health Check menggunakan Blackbox (endpoint `/healthz`)**
   - **Deskripsi:** Panel ini menampilkan status pengecekan kesehatan layanan Hasura melalui HTTP endpoint `/healthz`, yang dimonitor menggunakan Blackbox.
   - **Nilai yang Mungkin:**
     - `OK` (hijau): Pemeriksaan kesehatan berhasil, dan layanan Hasura merespons dengan baik melalui endpoint `/healthz`.
     - `No Data` (merah): Tidak ada data yang tersedia dari endpoint `/healthz`, yang mungkin menunjukkan bahwa layanan tidak merespons atau endpoint tersebut tidak aktif atau sedang dalam gangguan.
   - **Penggunaan:** Pengecekan ini sangat penting untuk memastikan bahwa layanan Hasura berjalan dan merespons dengan baik terhadap permintaan HTTP health check melalui endpoint `/healthz`. Jika `No Data`, administrator perlu memeriksa apakah layanan berjalan dan apakah Blackbox atau endpoint `/healthz` dapat diakses dan berfungsi dengan benar.

### 4. **Source Health Check**
   - **Deskripsi:** Menampilkan pemeriksaan kesehatan untuk sumber tertentu, seperti instance Hasura atau lingkungan yang berbeda.
   - **Nilai yang Mungkin:**
     - `OK` (hijau): Pemeriksaan kesehatan untuk instance Hasura tertentu berhasil.
     - `FAIL` (merah): Pemeriksaan kesehatan untuk instance tersebut gagal.
   - **Penggunaan:** Berguna untuk memantau kesehatan instance Hasura yang berbeda. Jika satu instance gagal, mungkin akan mempengaruhi query atau mutasi tertentu tergantung pada bagaimana instance tersebut digunakan.

### 5. **Versi Metadata**
   - **Deskripsi:** Menampilkan versi metadata Hasura saat ini.
   - **Nilai yang Ditampilkan:** Versi numerik, misalnya `292`.
   - **Penggunaan:** Administrator dapat melacak perubahan atau pembaruan metadata Hasura menggunakan nomor versi ini. Ini berguna untuk debugging atau memastikan bahwa versi metadata tertentu sedang digunakan.

### 6. **Latency Health Check**
   - **Deskripsi:** Panel ini akan menampilkan latensi (dalam milidetik) dari pemeriksaan kesehatan yang dilakukan oleh Hasura.
   - **Nilai yang Mungkin:**
     - Nilai latensi dalam ms (nilai rendah lebih baik).
     - `No data`: Menunjukkan bahwa tidak ada pemeriksaan kesehatan yang dilakukan atau tidak ada data yang direkam.
   - **Penggunaan:** Latensi pemeriksaan kesehatan penting untuk memahami seberapa lama waktu yang dibutuhkan Hasura untuk memverifikasi kesehatan layanannya. Latensi yang lebih tinggi mungkin menunjukkan masalah kinerja.

### 7. **Postgres Connections**
   - **Deskripsi:** Panel ini menampilkan jumlah koneksi aktif ke database Postgres dari Hasura, yang dipantau berdasarkan instance yang digunakan (seperti `testsejuta` dan `default`).
   - **Nilai yang Ditampilkan:** Garis tren yang menunjukkan jumlah koneksi Postgres dari instance tertentu dalam waktu tertentu. Pada gambar, terdapat dua instance, yaitu:
     - **testsejuta (hijau):** Menunjukkan adanya aktivitas koneksi ke Postgres pada sekitar pukul 10:40, yang mencapai 1 koneksi dan kemudian turun kembali.
     - **default (kuning):** Menunjukkan tidak ada koneksi yang terdeteksi dalam periode waktu yang sama.
   - **Penggunaan:** Panel ini membantu administrator untuk memantau apakah ada lonjakan atau penurunan jumlah koneksi ke Postgres. Jika jumlah koneksi terlalu tinggi atau fluktuasi yang tidak biasa terdeteksi, bisa menandakan adanya masalah performa atau penggunaan sumber daya yang perlu dianalisis lebih lanjut.


![image](https://github.com/user-attachments/assets/5dc98be0-11fc-4e24-812d-46accf6ecc86)


