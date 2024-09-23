# Dokumentasi Proses Pengelolaan dan Analisis Remote Shcema GraphQL pada Hasura

### Skenario 1: Matikan Kedua Sumber GQL Mas Ferdy
Langkah: Scale down (0 replicas) kedua deployment GQL Mas Ferdy.

![image](https://github.com/user-attachments/assets/87713f19-43f7-457e-bdd4-f94c51e5f0c0)

![image](https://github.com/user-attachments/assets/a24e5a4a-28fd-4362-95b9-9712d9ce93a2)


Tujuan: Menonaktifkan sementara GQL Mas Ferdy untuk melihat dampaknya pada layanan lain yang melakukan remote query.

### Skenario 2: Analisis Error pada Hasura yang Menggunakan Remote GQL Mas Ferdy

Error yang terjadi:

```json
{
  "errors": [
    {
      "message": "HTTP exception occurred while sending the request to \"http://10.100.14.10:8989/query\"",
      "extensions": {
        "path": "$",
        "code": "remote-schema-error",
        "internal": {
          "message": "Connection failure: Network.Socket.connect: <socket: 40>: does not exist (Connection refused)",
          "request": {
            "host": "10.100.14.10",
            "method": "POST",
            "path": "/query",
            "port": 8989,
            "queryString": "",
            "requestHeaders": {
              "Content-Type": "application/json",
              "User-Agent": "hasura-graphql-engine/v2.42.0",
              "x-hasura-role": "admin"
            },
            "responseTimeout": "ResponseTimeoutMicro 60000000",
            "secure": false
          },
          "type": "http_exception"
        }
      }
    }
  ]
}
```
![image](https://github.com/user-attachments/assets/edb6c99c-ff2e-4218-9b8c-0cf07ac96d72)

Error ini terjadi karena Hasura tidak bisa menghubungi endpoint remote schema yang terhubung ke GQL Mas Ferdy. Pesan yang muncul adalah:

  - "HTTP exception occurred while sending the request": Ini menunjukkan bahwa permintaan HTTP tidak berhasil dikirim.
  - "Connection failure: Network.Socket.connect: does not exist (Connection refused)": Ini menunjukkan bahwa socket untuk koneksi ke server GQL Mas Ferdy tidak ditemukan karena instance-nya sudah mati.

Kesimpulan: Hasura gagal melakukan remote request ke GQL Mas Ferdy karena service tidak aktif.

### Skenario 3: Lakukan Query dari Postman saat GQL Mas Ferdy Mati
Langkah: Buat Query Menggunakan Postman

Kirimkan request GraphQL yang biasanya mengakses GQL Mas Ferdy.
Endpoint yang digunakan: Arahkan query ke endpoint yang mengakses remote schema GQL Mas Ferdy.
Analisis Error yang Muncul di Postman:

Error yang muncul sama seperti pada hasura console.

![image](https://github.com/user-attachments/assets/cd21f43e-5618-47b4-9d93-2008c49f46f2)


### Skenario 4: Scale Up GQL Mas Ferdy
Langkah: Scale Up GQL Mas Ferdy menjadi 1 Replica


![image](https://github.com/user-attachments/assets/b25257ca-a7e8-4051-aeb1-2b77792ad22c)


### Skenario 5: Lakukan Query dari Postman (Sebelum Reload Schema)
Langkah: Ulangi Query dari Postman

Kirim query GraphQL melalui Postman ke remote schema yang mengarah ke GQL Mas Ferdy (yang baru saja diaktifkan kembali).
Analisis Error:

Tidak terjadi eroor apapun meskipun belum dilakukan Reload Shcema.

![image](https://github.com/user-attachments/assets/0fba62d4-aa06-486f-8da3-2d73e2fe1cf1)


## Kesimpulan Keseluruhan Pengelolaan dan Analisis GQL pada Hasura

Berdasarkan percobaan yang telah dilakukan dalam berbagai skenario, berikut adalah kesimpulan dari seluruh proses:

### Skenario saat GQL Mas Ferdy Dimatikan:

- Ketika instance GQL Mas Ferdy dimatikan (scale down menjadi 0), layanan Hasura yang melakukan remote query ke GQL Mas Ferdy langsung mengalami **error**. Error yang muncul berkaitan dengan **"Connection refused"** karena tidak ada service yang dapat diakses di endpoint yang dimaksud.
  
### Error yang terjadi:
- Di **Hasura**, error yang terjadi adalah **remote schema error**, yang menunjukkan bahwa Hasura tidak dapat menghubungi endpoint remote GQL Mas Ferdy.
- Di **Postman**, saat mencoba melakukan query, Postman juga mengembalikan error serupa dengan pesan **Network Error: Connection refused** atau **Timeout**, yang menandakan tidak ada koneksi yang bisa dilakukan ke GQL Mas Ferdy.

### Skenario saat GQL Mas Ferdy Dijalankan Kembali (Scale Up):

- Setelah service GQL Mas Ferdy diaktifkan kembali (scale up menjadi 1), koneksi kembali tersedia.
- Ketika mencoba query dari **Postman** setelah GQL aktif namun **tanpa reload schema di Hasura**, **tidak ada error** yang muncul. Ini menunjukkan bahwa Hasura tetap bisa menjalankan remote query meskipun remote schema belum di-reload, asalkan service remote GQL sudah aktif kembali.
- Proses reload schema **tidak langsung diperlukan** kecuali ada perubahan pada schema di remote GQL. Jika tidak ada perubahan, remote schema akan tetap berfungsi normal setelah service aktif kembali.

### Kesimpulan Utama:

- **Error hanya terjadi saat instance GQL Mas Ferdy dimatikan**. Error ini muncul karena Hasura tidak bisa melakukan koneksi ke remote GQL.
- **Setelah GQL Mas Ferdy diaktifkan kembali**, baik query dari Hasura maupun Postman dapat dijalankan dengan normal **tanpa perlu reload schema** di Hasura, selama schema GQL tidak mengalami perubahan. 
- **Error yang muncul** bersifat langsung dan terkait dengan koneksi, yaitu **Connection refused** dan **Timeout**. Error ini sepenuhnya teratasi ketika service diaktifkan kembali.

### Rekomendasi:

- Jika remote GQL mengalami downtime atau dimatikan sementara, cukup dengan mengaktifkan kembali service (scale up), dan query akan kembali normal tanpa perlu langkah tambahan seperti reload schema di Hasura, kecuali schema remote telah berubah.
- Dalam kasus downtime yang terencana atau berulang, memonitor log Hasura dan menggunakan tools seperti Postman untuk memverifikasi status koneksi dapat membantu mengidentifikasi masalah lebih awal.

Dokumentasi ini memberikan panduan lengkap mengenai pengelolaan remote schema di Hasura, beserta analisis yang terstruktur untuk menangani potensi downtime pada remote GQL services.


