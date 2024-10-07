# Laporan Hasura DDN

## 1. Apa Itu Hasura DDN?

**Hasura DDN** (Data Delivery Network) adalah fitur baru yang diperkenalkan di Hasura V3 untuk memfasilitasi distribusi data dengan lebih cepat dan efisien melalui jaringan cache terdistribusi. DDN memungkinkan query GraphQL untuk dipercepat dan di-cache dengan performa yang mirip dengan CDN (Content Delivery Network), tetapi khusus untuk data. Hal ini membantu mengurangi latensi dan meningkatkan efisiensi aplikasi yang mengandalkan API Hasura, terutama untuk aplikasi yang memiliki skala global.

## 2. Bagaimana Arsitektur dan Cara Kerjanya?

### Arsitektur
- **Cache Terdistribusi**: Hasura DDN bekerja dengan cache yang terdistribusi di beberapa lokasi atau edge servers. Ini memastikan bahwa data yang sering diakses oleh aplikasi pengguna tersedia dengan latensi rendah dari server terdekat.
- **GraphQL Layer**: DDN terintegrasi secara native dengan GraphQL Engine Hasura, memungkinkan pengguna untuk mengatur cache pada tingkat query. Setiap query bisa di-cache sesuai dengan parameter tertentu, seperti waktu kedaluwarsa atau kondisi spesifik.
- **Penyimpanan dan Sinkronisasi Data**: Data yang di-cache di edge servers disinkronisasi dengan database utama menggunakan mekanisme invalidasi cache yang efisien. Ini memastikan bahwa data tetap konsisten dan up-to-date tanpa harus menunggu pembaruan manual.

### Cara Kerja
1. **Query Execution**: Ketika sebuah query GraphQL dikirim ke Hasura, DDN memeriksa apakah hasil dari query tersebut sudah ada di cache.
2. **Cache Validation**: Jika data sudah tersedia dan masih valid, DDN langsung memberikan respons dari cache tersebut. Jika tidak, query akan diteruskan ke database utama.
3. **Cache Invalidation**: Ketika ada perubahan data di database utama, Hasura DDN mengupdate atau menghapus cache yang relevan, memastikan integritas dan konsistensi data.

## 3. Apa Perbedaan dengan Hasura V2?

| **Aspek**            | **Hasura V2**                          | **Hasura V3 (DDN)**                      |
|---------------------|----------------------------------------|-----------------------------------------|
| **Caching**         | Tidak memiliki caching bawaan          | Mendukung DDN untuk caching data        |
| **Performance**     | Bergantung pada performa database utama| Optimized dengan caching di edge servers|
| **Scalability**     | Skala terbatas pada satu server        | Skala global dengan cache terdistribusi |
| **Latency**         | Bergantung pada lokasi database        | Latensi rendah melalui edge cache       |
| **Integrasi DDN**   | Tidak ada integrasi DDN                | Integrasi native dengan DDN             |

## 4. Fitur di Hasura V2 dan V3

| **Fitur**                | **Hasura V2**                | **Hasura V3 (DDN)**              |
|------------------------|-----------------------------|---------------------------------|
| **GraphQL API**        | Ya                          | Ya                              |
| **Live Queries**       | Ya                          | Ya                              |
| **Caching**            | Tidak                       | Ya (DDN)                        |
| **Event Trigger**      | Ya                          | Ya                              |
| **Remote Schema**      | Ya                          | Ya                              |
| **Permissions**        | Ya                          | Ya                              |
| **Data Federation**    | Tidak                       | Ya (melalui DDN dan integrasi) |
| **Edge Servers**       | Tidak                       | Ya (terintegrasi dengan DDN)   |
| **Global Availability**| Tidak (bergantung pada DB)  | Ya (DDN)                        |

## 5. Keunggulan dan Kekurangan

### Keunggulan
- **Hasura DDN (V3)**:
  - **Performa Lebih Cepat**: Dengan caching di edge servers, respons API lebih cepat dan latensi lebih rendah.
  - **Global Scalability**: DDN memungkinkan aplikasi untuk menskalakan secara global dengan dukungan caching terdistribusi.
  - **Integrasi Caching GraphQL**: Pengguna bisa mengatur caching langsung pada tingkat GraphQL query, memberikan fleksibilitas dalam optimasi.

- **Hasura V2**:
  - **Stabilitas**: Sudah mature dan stabil digunakan di banyak skenario produksi.
  - **Fitur Dasar yang Kuat**: Mendukung event triggers, remote schemas, dan query optimization tanpa kompleksitas tambahan dari DDN.

### Kekurangan
- **Hasura DDN (V3)**:
  - **Kompleksitas Konfigurasi**: DDN memerlukan konfigurasi tambahan dan pemahaman tentang cache invalidation untuk bekerja secara optimal.
  - **Potensi Konsistensi Data**: Menggunakan caching pada skala besar bisa memunculkan isu konsistensi data jika tidak diatur dengan benar.

- **Hasura V2**:
  - **Tidak Ada Caching Native**: Semua query mengakses database utama, sehingga performa bisa menurun jika jumlah query tinggi.
  - **Tidak Skala Global Secara Otomatis**: Bergantung pada performa dan lokasi database utama.

