# Dokumentasi Analisa dan penjelesan output Metrics Hasura

![image](https://github.com/user-attachments/assets/af93fc59-b039-4b44-92e0-6d2774382fd0)

Berikut adalah penjelasan mengenai setiap keluaran metrik yang disediakan oleh Hasura.

## 1. `hasura_action_request_bytes_total`
- **Deskripsi**: Ini mengukur total ukuran (dalam byte) dari semua data yang dikirim sebagai bagian dari permintaan HTTP ke API Hasura melalui fitur "actions". Fitur actions memungkinkan Anda menulis logika khusus yang tidak dapat dijalankan langsung oleh GraphQL. Setiap kali Anda mengirim data (seperti JSON), ukurannya akan dihitung di sini.
- **Tipe**: Counter (artinya nilai ini terus bertambah seiring waktu, tidak pernah berkurang).

## 2. `hasura_action_response_bytes_total`
- **Deskripsi**: Sama seperti metrik di atas, tapi ini mengukur ukuran total dari respons HTTP yang diterima setelah permintaan dikirim melalui fitur actions. Ini membantu Anda memahami berapa banyak data yang Anda terima sebagai respons dari server eksternal melalui actions.
- **Tipe**: Counter

## 3. `hasura_active_subscription_pollers`
- **Deskripsi**: Metrik ini menunjukkan jumlah "poller" aktif, yang digunakan untuk mengawasi perubahan data pada server. Ketika ada subscription aktif seperti live-query atau streaming di Hasura, poller ini aktif. Ini membantu mengetahui berapa banyak subscription yang berjalan saat ini.
- **Tipe**: Gauge (nilai ini bisa naik atau turun seiring waktu, tergantung aktivitas).
- **Label**:
  - `subscription_kind`: Jenis subscription, seperti "live-query" (mengawasi perubahan data terus-menerus) atau "streaming" (mengalirkan data secara real-time).

## 4. `hasura_active_subscription_pollers_in_error_state`
- **Deskripsi**: Ini mengukur jumlah poller subscription yang mengalami kesalahan atau berada dalam keadaan error. Misalnya, jika subscription gagal memproses permintaan karena masalah jaringan atau lainnya, poller tersebut akan terhitung di sini.
- **Tipe**: Gauge
- **Label**:
  - `subscription_kind`: Jenis subscription yang mengalami error, seperti "live-query" atau "streaming".

## 5. `hasura_cache_request_count`
- **Deskripsi**: Metrik ini menunjukkan berapa kali sistem Hasura memeriksa cache untuk permintaan data. "Cache hit" artinya data ditemukan di cache, sehingga permintaan tidak perlu mengambil data dari database. "Cache miss" artinya data tidak ditemukan di cache, sehingga Hasura harus mengambilnya dari database.
- **Tipe**: Counter
- **Label**:
  - `status`: Status apakah permintaan data ditemukan di cache ("hit") atau tidak ("miss").
