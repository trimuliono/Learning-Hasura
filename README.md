# Hasura Project Setup & Monitoring Guide

Selamat datang di repositori proyek Hasura! Proyek ini bertujuan untuk memberikan panduan menyeluruh dalam mengatur dan mempelajari berbagai teknologi yang diperlukan untuk membangun aplikasi dengan Hasura, serta alat monitoring yang dapat membantu memantau dan mengoptimalkan kinerja aplikasi.

## Teknologi yang Terlibat

Dalam proyek ini, kamu akan belajar tentang berbagai alat dan teknologi yang mendukung pengembangan aplikasi modern, termasuk:
- **Hasura**: Platform GraphQL yang memungkinkan pengembangan backend dengan cepat.
- **Docker** dan **Kubernetes**: Untuk containerization dan orkestrasi aplikasi.
- **PostgreSQL**, **MySQL**, dan **MSSQL**: Database yang mendukung Hasura.
- **Redis**: Untuk caching dan penyimpanan data sementara.
- **Grafana** dan **Prometheus**: Alat untuk monitoring metrik performa aplikasi.
- **ElasticSearch** dan **Kibana**: Untuk pencarian dan visualisasi log.
- **APM (Application Performance Monitoring)**: Untuk memonitor kinerja aplikasi.
- **Postman** dan **JMeter**: Untuk testing API dan melakukan load testing.

## Struktur Folder

Repositori ini diatur dengan mengikuti urutan teknologi yang disarankan untuk dipelajari. Berikut adalah penjelasan singkat tentang setiap folder:

### 1. `1_linux/`
- **Deskripsi**: Materi pembelajaran tentang **Linux** dan penggunaan dasar terminal yang penting untuk pengelolaan server dan pengembangan aplikasi.
- **Contoh materi**: Dasar-dasar Linux, perintah-perintah penting, dan pengelolaan file di Linux.

### 2. `2_docker/`
- **Deskripsi**: Panduan tentang **Docker** untuk membuat kontainer aplikasi yang ringan dan mudah di-deploy.
- **Contoh materi**: Cara membuat container dengan Docker, penggunaan Docker Compose untuk mengatur multi-container setup.

### 3. `3_db/`
- **Deskripsi**: Materi pembelajaran tentang **PostgreSQL**, **MySQL**, dan **MSSQL**, serta cara mengonfigurasi dan menggunakannya dengan Hasura.
- **Contoh materi**: Instalasi dan pengaturan database, serta mengintegrasikan dengan Hasura.

### 4. `4_hasura_v2/`
- **Deskripsi**: Panduan untuk memulai dengan **Hasura v2**, termasuk instalasi dan pengaturan awal.
- **Contoh materi**: Cara mengatur Hasura v2, memahami fitur-fitur dasarnya.

### 5. `5_hasura_v3/`
- **Deskripsi**: Materi tentang **Hasura v3**, yang mencakup pembaruan fitur dan cara migrasi dari v2 ke v3.
- **Contoh materi**: Fitur baru di Hasura v3, panduan upgrade dan implementasi.

### 6. `6_redis/`
- **Deskripsi**: Panduan untuk menggunakan **Redis** sebagai sistem caching dan penyimpanan data sementara.
- **Contoh materi**: Instalasi Redis, teknik caching dasar, dan pengaturan Redis dengan Hasura.

### 7. `7_kubernetes/`
- **Deskripsi**: Pembelajaran tentang **Kubernetes** untuk orkestrasi aplikasi dan deployment skala besar.
- **Contoh materi**: Men-deploy aplikasi menggunakan Kubernetes, konfigurasi cluster, dan manajemen pods.

### 8. `8_monitoring/`
- **Deskripsi**: Panduan lengkap untuk memonitor aplikasi menggunakan berbagai alat seperti **Prometheus**, **Grafana**, **APM**, **ElasticSearch**, dan **Kibana**.
- **Contoh materi**: Integrasi Prometheus dan Grafana untuk monitoring metrik, konfigurasi APM untuk memantau kinerja aplikasi, dan penggunaan ElasticSearch untuk menganalisis log.

### 9. `9_jmeter/`
- **Deskripsi**: Panduan untuk melakukan **load testing** menggunakan **JMeter**.
- **Contoh materi**: Menyusun skenario pengujian beban, pengukuran kinerja API, dan analisis hasil tes.

### 10. `10_api_testing/`
- **Deskripsi**: Pembelajaran tentang **API testing** menggunakan **Postman**.
- **Contoh materi**: Membuat dan mengelola koleksi Postman, pengujian endpoint GraphQL, dan menggunakan Postman untuk testing otomatis.

---

## Urutan Pembelajaran yang Disarankan

Berikut adalah urutan pembelajaran yang disarankan untuk memulai proyek ini, dimulai dari pemahaman dasar hingga penggunaan alat untuk monitoring dan testing aplikasi:

1. **Linux** - Memahami dasar-dasar Linux dan pengelolaan server.
2. **Docker** - Belajar containerization dan cara menjalankan aplikasi dalam container.
3. **Database** (PostgreSQL, MySQL, MSSQL) - Mengonfigurasi database yang akan digunakan dengan Hasura.
4. **Hasura v2** - Menguasai Hasura v2 sebagai platform backend untuk aplikasi GraphQL.
5. **Hasura v3** - Pembelajaran tentang Hasura v3 dan fitur-fitur barunya.
6. **Redis** - Penggunaan Redis untuk caching dan meningkatkan performa aplikasi.
7. **Kubernetes** - Memahami deployment dan orkestrasi aplikasi menggunakan Kubernetes.
8. **Monitoring** (Prometheus, Grafana, APM, ElasticSearch, Kibana) - Menggunakan berbagai alat untuk monitoring metrik dan log aplikasi.
9. **JMeter** - Menggunakan JMeter untuk menguji performa aplikasi dengan beban tinggi.
10. **API Testing** (Postman) - Menggunakan Postman untuk menguji API, termasuk GraphQL endpoint Hasura.

---

## Kontribusi

Jika kamu ingin berkontribusi pada proyek ini, silakan lakukan fork dan kirim pull request dengan perubahan yang kamu buat. Pastikan untuk mengikuti pedoman kontribusi dan melakukan pengujian sebelum mengajukan perubahan.

## Lisensi

Proyek ini dilisensikan di bawah [MIT License](LICENSE.md).

---
