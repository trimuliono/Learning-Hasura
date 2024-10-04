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

### `1.1 Panel Overview` - Dashboard Hasura HTTP GraphQL
Dokumentasi ini memberikan penjelasan untuk setiap panel yang terlihat pada bagian *Overview* dari *Hasura HTTP GraphQL Dashboard* di Grafana. Setiap panel memberikan wawasan mengenai kinerja query dan mutasi GraphQL yang terjadi dalam Hasura.

  #### 1. **Total Queries**
   - **Deskripsi:** Panel ini menunjukkan jumlah total *query* GraphQL yang dijalankan dalam periode waktu yang dipantau.
   - **Nilai yang Ditampilkan:** Dalam gambar, terdapat 12 *query* yang tercatat.
   - **Penggunaan:** Panel ini membantu melacak seberapa sering *query* GraphQL digunakan dalam aplikasi. Administrator bisa menggunakan data ini untuk memahami pola penggunaan dan mendeteksi lonjakan yang tidak wajar.

  #### 2. **Query Latency (P95)**
   - **Deskripsi:** Panel ini menampilkan latensi (dalam milidetik) dari *query* GraphQL. Latensi P95 berarti 95% dari permintaan memiliki latensi yang sama atau lebih rendah dari angka ini.
   - **Nilai yang Ditampilkan:** Dalam gambar, nilai P95 dari latensi *query* adalah 27.0 ms.
   - **Penggunaan:** Panel ini penting untuk memantau performa *query*. Jika latensi terlalu tinggi, hal ini bisa menandakan masalah performa di sisi server, seperti masalah dalam optimasi *query*, beban server, atau keterbatasan sumber daya.

  #### 3. **Total Mutations**
   - **Deskripsi:** Panel ini menunjukkan jumlah total operasi *mutation* GraphQL yang dilakukan.
   - **Nilai yang Ditampilkan:** Pada gambar, hanya ada 1 *mutation* yang tercatat.
   - **Penggunaan:** Administrator dapat memantau seberapa sering operasi *mutation* digunakan dalam aplikasi. Seperti *query*, data ini berguna untuk memahami pola penggunaan dan mendeteksi aktivitas yang mencurigakan.

  #### 4. **Mutation Latency (P95)**
   - **Deskripsi:** Panel ini menampilkan latensi operasi *mutation*. Seperti *query*, P95 mengacu pada 95% dari operasi memiliki latensi yang sama atau lebih rendah.
   - **Nilai yang Ditampilkan:** Pada gambar, nilai P95 dari latensi *mutation* adalah 9.50 ms.
   - **Penggunaan:** Latensi *mutation* penting karena operasi *mutation* mengubah data. Jika latensi terlalu tinggi, ini bisa mempengaruhi pengalaman pengguna dan efisiensi aplikasi. Sama seperti pada *query*, masalah performa perlu diidentifikasi.

  #### 5. **Top Queries**
   - **Deskripsi:** Panel ini biasanya akan menunjukkan *query-query* yang paling sering digunakan dalam aplikasi.
   - **Nilai yang Ditampilkan:** Dalam gambar, tidak ada data yang ditampilkan.
   - **Penggunaan:** Panel ini bermanfaat untuk mengidentifikasi *query* yang sering digunakan dan memerlukan optimasi lebih lanjut untuk meningkatkan performa aplikasi.

  #### 6. **Top Mutations**
   - **Deskripsi:** Panel ini biasanya menampilkan *mutation* yang paling sering digunakan.
   - **Nilai yang Ditampilkan:** Pada gambar, tidak ada data yang terlihat.
   - **Penggunaan:** Panel ini memberikan wawasan tentang operasi *mutation* yang sering digunakan. Jika operasi tertentu sering digunakan, penting untuk memastikan bahwa operasi tersebut optimal dalam hal performa.

  #### 7. **Top Error Rate**
   - **Deskripsi:** Panel ini menunjukkan tingkat kesalahan (*error rate*) dari operasi *query* atau *mutation* yang dilakukan.
   - **Nilai yang Ditampilkan:** Tidak ada data yang ditampilkan pada gambar.
   - **Penggunaan:** Panel ini penting untuk memantau stabilitas sistem. Jika terjadi lonjakan kesalahan, administrator perlu segera melakukan investigasi untuk mencegah masalah lebih lanjut dalam aplikasi.

![image](https://github.com/user-attachments/assets/9a6df46d-3334-4dbc-b196-96fa71a3edd0)

### `1.2 Panel GraphQL Metrics` - Dashboard Hasura HTTP GraphQL
Dokumentasi ini memberikan penjelasan untuk setiap panel yang terlihat pada bagian *GraphQL Metrics* dari *Hasura HTTP GraphQL Dashboard* di Grafana. Setiap panel menyediakan metrik penting terkait performa query dan mutation di Hasura.

  #### 1. Query Request Rate
   - **Deskripsi**: Panel ini menunjukkan jumlah *request* query GraphQL yang diterima oleh server dalam rentang waktu tertentu.
   - **Nilai yang Ditampilkan**: Dalam gambar, terlihat bahwa Query Request Rate berada di angka 0 sepanjang waktu, yang menunjukkan tidak ada permintaan query yang masuk pada waktu tersebut.
   - **Penggunaan**: Panel ini membantu administrator memantau seberapa banyak permintaan yang diterima oleh server. Jika terjadi penurunan signifikan atau lonjakan mendadak, administrator dapat memeriksa apakah terjadi anomali atau apakah server sedang overload.
   - **Cara Analisis**: 
     - Pastikan bahwa tingkat request stabil. Jika ada lonjakan tajam dalam request, ini bisa menandakan masalah performa di aplikasi yang menggunakan Hasura.
  ![image](https://github.com/user-attachments/assets/052c26af-e95b-464f-a2cf-ab75d3a7ac4b)

  #### 2. Mutation Request Rate
   - **Deskripsi**: Panel ini menunjukkan jumlah *request* mutation GraphQL yang diterima oleh server dalam waktu yang sama.
   - **Nilai yang Ditampilkan**: Tidak ada data yang ditampilkan (No Data).
   - **Penggunaan**: Memantau berapa banyak permintaan mutation diterima oleh server Hasura.
   - **Cara Analisis**: Jika mutation tidak aktif, periksa apakah aplikasi mengirimkan mutation sesuai harapan atau ada kesalahan pada bagian aplikasi.
  ![image](https://github.com/user-attachments/assets/e97d1a4d-037e-429d-b5e9-496cc32c5aff)

  #### 3. Query Error Rate
   - **Deskripsi**: Panel ini menampilkan persentase error yang terjadi pada permintaan query GraphQL.
   - **Nilai yang Ditampilkan**: Query Error Rate berada di angka 0, yang menunjukkan tidak ada kesalahan yang terjadi selama periode waktu tersebut.
   - **Penggunaan**: Panel ini penting untuk memantau kesalahan atau *error* dalam operasi query. Kesalahan yang meningkat bisa menjadi tanda adanya masalah performa server atau kesalahan di tingkat aplikasi.
   - **Cara Analisis**: Jika tingkat kesalahan tiba-tiba meningkat, segera selidiki penyebabnya, seperti konfigurasi yang salah atau query yang terlalu berat.
  ![image](https://github.com/user-attachments/assets/cc197704-f1a2-4447-9348-9face5c4eb48)


  #### 4. Mutation Error Rate
   - **Deskripsi**: Panel ini menampilkan persentase error yang terjadi pada permintaan mutation GraphQL.
   - **Nilai yang Ditampilkan**: Tidak ada data yang ditampilkan (No Data).
   - **Penggunaan**: Ini berguna untuk mendeteksi apakah mutation yang dijalankan mengalami kesalahan. Kesalahan yang tinggi bisa menjadi indikator masalah pada sisi server atau basis data.
   - **Cara Analisis**: Jika ada kesalahan, segera lakukan debugging pada operasi mutation.
  ![image](https://github.com/user-attachments/assets/05ec043a-81ae-4ad5-bf13-2347aac193c8)

  #### 5. Query Latency (P95)
   - **Deskripsi**: Panel ini menampilkan latensi (waktu tunda) dari 95% permintaan query yang berhasil dijalankan.
   - **Nilai yang Ditampilkan**: Untuk Query Latency, latensi rata-rata berada di sekitar 30 ms dan turun hingga 0 ms pada akhir periode waktu yang dipantau.
   - **Penggunaan**: Latensi rendah menunjukkan performa yang baik. Jika latensi meningkat, hal ini bisa menunjukkan adanya beban server atau masalah dalam query yang digunakan.
   - **Cara Analisis**: Pantau jika ada peningkatan tiba-tiba dalam latensi dan lakukan investigasi.

  #### 6. Mutation Latency (P95)
   - **Deskripsi**: Panel ini menampilkan latensi dari 95% permintaan mutation yang diproses.
   - **Nilai yang Ditampilkan**: Tidak ada data yang ditampilkan (No Data), yang berarti tidak ada operasi mutation yang terpantau selama waktu tersebut.
   - **Penggunaan**: Latensi yang rendah memastikan bahwa mutation berjalan dengan efisien. Jika latensi tinggi, bisa jadi server kelebihan beban atau ada masalah dalam operasi mutation.
   - **Cara Analisis**: Periksa apakah mutation dijalankan sesuai ekspektasi dan jika tidak ada data, selidiki apakah ada kesalahan pada bagian aplikasi.

  ![image](https://github.com/user-attachments/assets/1b4ae8f8-9c9e-49fd-a9d9-45f53f89d12f)


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


