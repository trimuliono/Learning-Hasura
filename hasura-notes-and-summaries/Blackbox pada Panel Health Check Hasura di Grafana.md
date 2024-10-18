## Monitoring Health Status Hasura dengan Blackbox Exporter, Prometheus, dan Grafana

Ketika kita memiliki sebuah instance **Hasura**, memantau status kesehatannya (health check) sangat penting untuk memastikan aplikasi kita berjalan dengan baik. Hasura menyediakan beberapa endpoint untuk melakukan monitoring, seperti endpoint `/v1/metrics` yang memberikan informasi umum tentang performa sistem, dan **/healthz** yang secara spesifik untuk memeriksa status kesehatan (health status) dari instance Hasura itu sendiri.

Namun, agar kita bisa memantau status **/healthz** di platform monitoring seperti **Grafana**, diperlukan beberapa langkah, yang melibatkan penggunaan **Prometheus** dan **Blackbox Exporter**.

Mari kita bahas langkah-langkah ini satu per satu dan mengapa komponen-komponen ini penting.

## Apa Itu Blackbox dan Blackbox Exporter?

- **Blackbox**: Istilah "blackbox" dalam dunia IT menggambarkan sesuatu yang kita pantau dari luar tanpa harus tahu bagaimana sistem tersebut bekerja di dalam. Kita hanya melihat hasil akhirnya, misalnya apakah suatu service bisa diakses atau tidak. Dalam konteks monitoring, kita memantau apakah sebuah service berjalan dengan baik dari luar, seperti memeriksa apakah sebuah endpoint HTTP merespons, tanpa peduli tentang bagaimana service itu diimplementasikan di dalam.
  
- **Blackbox Exporter**: Ini adalah alat yang dibuat oleh **Prometheus** untuk memeriksa status dari berbagai jenis layanan dengan pendekatan blackbox. Alat ini bisa digunakan untuk memantau layanan HTTP, HTTPS, DNS, TCP, dan ICMP (seperti ping). Dengan Blackbox Exporter, kita bisa memeriksa apakah sebuah layanan, seperti **Hasura** atau endpoint tertentu seperti **/healthz**, bisa dijangkau dan memberikan respon yang benar.

## Alur Kerja Blackbox Exporter

![image](https://github.com/user-attachments/assets/e5fa2d50-abec-4b68-b212-02a84b4b14a1)

Gambar diatas tersebut menunjukkan alur kerja Blackbox Exporter dalam sistem monitoring menggunakan Prometheus. Berikut adalah penjelasan mengenai alur di gambar tersebut:

1. Prometheus: Prometheus adalah sistem monitoring yang melakukan scraping data dari berbagai exporter (termasuk Blackbox Exporter) untuk memantau metrik dari layanan atau sistem yang dipantau. Pada gambar ini, Prometheus mengirimkan HTTP request ke Blackbox Exporter.

2. HTTP Request (module, target): Prometheus mengirimkan HTTP request ke Blackbox Exporter, yang berisi informasi mengenai modul dan target yang akan diuji. Modul di sini menentukan jenis probe yang akan dilakukan (misalnya HTTP, ICMP, DNS), dan target adalah layanan atau endpoint yang akan diuji.

3. Blackbox Exporter: Blackbox Exporter melakukan probe ke target berdasarkan instruksi yang diberikan oleh Prometheus. Ini dapat berupa tes HTTP (untuk melihat apakah suatu endpoint tersedia), ICMP (ping untuk memeriksa apakah host aktif), atau jenis tes lainnya.

4. Probe is launched against target: Blackbox Exporter meluncurkan probe atau pengujian terhadap target yang diminta. Target ini bisa berupa layanan, server, API, atau endpoint lain yang ingin diuji kesehatannya.

5. Probe returns data: Setelah probe dilakukan, Blackbox Exporter mengumpulkan data dari target, seperti status respon (misalnya kode status HTTP 200, jika sukses), waktu respon (latency), atau informasi lainnya tergantung pada jenis probe yang digunakan.

6. HTTP Response (in Prometheus format): Setelah mendapatkan data dari probe, Blackbox Exporter mengirimkan hasilnya kembali ke Prometheus dalam format yang dimengerti oleh Prometheus, biasanya berupa metrik yang dapat di-scrape dan disimpan oleh Prometheus untuk analisis lebih lanjut.

7. Target: Target yang diuji bisa berupa aplikasi, API, layanan, atau infrastruktur lainnya yang ingin dipantau kesehatannya. Blackbox Exporter melakukan probe untuk mengumpulkan informasi terkait performa target tersebut.

Kesimpulan alurnya:

- Prometheus menginisiasi probe melalui Blackbox Exporter untuk memonitor status kesehatan suatu target.
- Blackbox Exporter melakukan pengujian eksternal terhadap target tersebut.
- Data hasil pengujian dikembalikan ke Prometheus dalam format metrik untuk dianalisis dan divisualisasikan di dashboard monitoring seperti Grafana.


### Langkah-langkah Menghubungkan Blackbox Exporter ke Prometheus dan Grafana

Agar kita bisa memantau status **/healthz** Hasura di **Grafana**, kita perlu melakukan beberapa langkah, di antaranya:

1. **Menyiapkan Blackbox Exporter**  
   Blackbox Exporter akan bertugas untuk memantau status **HTTP** atau **HTTPS** dari endpoint **/healthz** di Hasura. Blackbox Exporter akan memeriksa apakah endpoint tersebut memberikan respons yang baik atau tidak.

   Contohnya, jika kita ingin memantau apakah **/healthz** memberikan respons 200 (OK), maka kita bisa menggunakan Blackbox Exporter untuk mengirimkan request ke endpoint tersebut secara berkala.

2. **Menghubungkan Blackbox Exporter ke Prometheus**  
   Setelah Blackbox Exporter dikonfigurasi, kita perlu membuat **job** di **Prometheus**. Job ini adalah konfigurasi yang memberi tahu Prometheus untuk mengumpulkan data dari Blackbox Exporter.

   Contoh konfigurasi job di Prometheus mungkin terlihat seperti ini:

   ```yaml
   - job_name: 'hasura_health'
     metrics_path: /probe
     params:
       module: [http_2xx]  # ini akan memantau apakah respon HTTP adalah 2xx (berhasil)
     static_configs:
       - targets:
         - http://hasura-instance:8080/healthz
     relabel_configs:
       - source_labels: [__address__]
         target_label: __param_target
       - source_labels: [__param_target]
         target_label: instance
       - target_label: __address__
         replacement: blackbox-exporter:9115
   ```

   Dalam konfigurasi di atas:
   - **job_name** memberi nama pekerjaan, dalam hal ini untuk memantau health Hasura.
   - **metrics_path** memberitahu Prometheus bahwa Blackbox Exporter harus digunakan untuk memeriksa status.
   - **params** memberitahu kita ingin memeriksa apakah status HTTP yang diterima adalah 2xx (berhasil).
   - **static_configs** adalah lokasi endpoint yang akan diperiksa (misalnya **http://hasura-instance:8080/healthz**).
   - **relabel_configs** mengarahkan request ke Blackbox Exporter.

3. **Menyambungkan Prometheus ke Grafana**  
   Setelah Prometheus berhasil mengumpulkan data dari Blackbox Exporter, langkah berikutnya adalah menampilkan data tersebut di **Grafana**. Di Grafana, kita akan membuat **dashboard** yang memvisualisasikan hasil monitoring.

   Grafana akan mengambil data dari Prometheus dan menunjukkan status endpoint **/healthz**, seperti apakah instance Hasura kita berjalan normal (status 200 OK) atau sedang mengalami masalah.

### Kesimpulan

Dengan menggunakan **Blackbox Exporter**, kita bisa memantau endpoint **/healthz** di Hasura tanpa perlu tahu bagaimana sistem di dalam bekerja. Blackbox Exporter hanya akan memeriksa apakah endpoint tersebut memberikan respons yang baik.

Kemudian, data ini dikumpulkan oleh **Prometheus**, dan dari sana kita bisa membuat dashboard di **Grafana** untuk memvisualisasikan status health dari Hasura. Langkah-langkahnya melibatkan:
1. Menggunakan Blackbox Exporter untuk memantau endpoint.
2. Menghubungkan Prometheus dengan Blackbox Exporter melalui sebuah job.
3. Menampilkan hasil monitoring di Grafana untuk visualisasi yang mudah dibaca.

Dengan setup ini, kita bisa memantau health status Hasura secara otomatis dan real-time di Grafana!
