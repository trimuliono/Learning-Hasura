# Dokumentasi Proses Pengelolaan dan Analisis Remote Shcema GraphQL pada Hasura

Skenario 1: Matikan Kedua Sumber GQL Mas Ferdy
Langkah: Scale down (0 replicas) kedua deployment GQL Mas Ferdy.

Tujuan: Menonaktifkan sementara GQL Mas Ferdy untuk melihat dampaknya pada layanan lain yang melakukan remote query.

Skenario 2: Analisis Error pada Hasura yang Menggunakan Remote GQL Mas Ferdy
Langkah: Pantau Log Hasura

Masuk ke masing-masing instance Hasura yang melakukan remote query ke GQL Mas Ferdy.

Skenario 3: Lakukan Query dari Postman saat GQL Mas Ferdy Mati
Langkah: Buat Query Menggunakan Postman

Kirimkan request GraphQL yang biasanya mengakses GQL Mas Ferdy.
Endpoint yang digunakan: Arahkan query ke endpoint yang mengakses remote schema GQL Mas Ferdy.
Analisis Error yang Muncul di Postman:

Skenario 4: Scale Up GQL Mas Ferdy
Langkah: Scale Up GQL Mas Ferdy menjadi 1 Replica

Skenario 5: Lakukan Query dari Postman (Sebelum Reload Schema)
Langkah: Ulangi Query dari Postman

Kirim query GraphQL melalui Postman ke remote schema yang mengarah ke GQL Mas Ferdy (yang baru saja diaktifkan kembali).
Analisis Error:

Meskipun GQL Mas Ferdy sudah aktif kembali, jika Hasura belum melakukan reload schema, mungkin masih ada error.
Error yang mungkin muncul:
Stale schema: Hasura mungkin masih menggunakan schema lama, sehingga mengembalikan error karena remote schema belum di-refresh.
Invalid response: Query mungkin tidak dieksekusi dengan benar karena cache atau schema lama yang belum diperbarui.
