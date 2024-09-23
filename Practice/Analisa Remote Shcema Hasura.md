# Dokumentasi Proses Pengelolaan dan Analisis Remote Shcema GraphQL pada Hasura

Skenario 1: Matikan Kedua Sumber GQL Mas Ferdy
Langkah: Scale down (0 replicas) kedua deployment GQL Mas Ferdy.

![image](https://github.com/user-attachments/assets/87713f19-43f7-457e-bdd4-f94c51e5f0c0)

![image](https://github.com/user-attachments/assets/a24e5a4a-28fd-4362-95b9-9712d9ce93a2)


Tujuan: Menonaktifkan sementara GQL Mas Ferdy untuk melihat dampaknya pada layanan lain yang melakukan remote query.

Skenario 2: Analisis Error pada Hasura yang Menggunakan Remote GQL Mas Ferdy

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


Skenario 3: Lakukan Query dari Postman saat GQL Mas Ferdy Mati
Langkah: Buat Query Menggunakan Postman

Kirimkan request GraphQL yang biasanya mengakses GQL Mas Ferdy.
Endpoint yang digunakan: Arahkan query ke endpoint yang mengakses remote schema GQL Mas Ferdy.
Analisis Error yang Muncul di Postman:

Error yang muncul sama seperti pada hasura console.

![image](https://github.com/user-attachments/assets/cd21f43e-5618-47b4-9d93-2008c49f46f2)


Skenario 4: Scale Up GQL Mas Ferdy
Langkah: Scale Up GQL Mas Ferdy menjadi 1 Replica


![image](https://github.com/user-attachments/assets/b25257ca-a7e8-4051-aeb1-2b77792ad22c)


Skenario 5: Lakukan Query dari Postman (Sebelum Reload Schema)
Langkah: Ulangi Query dari Postman

Kirim query GraphQL melalui Postman ke remote schema yang mengarah ke GQL Mas Ferdy (yang baru saja diaktifkan kembali).
Analisis Error:

Tidak terjadi eroor apapun meskipun belum dilakukan Reload Shcema.

![image](https://github.com/user-attachments/assets/0fba62d4-aa06-486f-8da3-2d73e2fe1cf1)

