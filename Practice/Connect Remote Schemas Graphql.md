# Connect Remote Schemas Graphql

rabu 18/09/2024
remote schemas mas verdy, lakukan query remote schema tersebut pake postman
deadline: besok jam 4 sore

Untuk melakukan query remote schema melalui Hasura menggunakan Postman, Anda harus memahami bahwa query remote schema dilakukan melalui endpoint Hasura, bukan langsung ke endpoint remote schema tersebut. Hasura bertindak sebagai proxy yang menghubungkan ke remote schema yang telah ditambahkan.

Berikut adalah langkah-langkah detail yang harus dilakukan untuk mengirim query ke remote schema di Hasura melalui Postman:

### 1. Pastikan Remote Schema Sudah Ditambahkan di Hasura
Sebelum melakukan query dari Postman, pastikan bahwa remote schema di Hasura sudah dikonfigurasi dengan benar. Untuk menambahkannya:

Buka Hasura Console.
Navigasi ke Remote Schemas dan tambahkan remote schema dengan URL http://10.100.14.10:8989/query.
Berikan nama untuk remote schema ini, misalnya: remote_schema_example.

### 2. URL Endpoint Hasura di Postman
Dalam Postman, Anda akan mengirimkan request ke endpoint GraphQL Hasura, bukan langsung ke remote schema. Endpoint-nya adalah:

```bash
http://10.100.14.6:8082/v1/graphql
```

### 3. Setel Headers di Postman
Buat request baru di Postman dengan metode POST.
Masukkan URL endpoint Hasura:

```bash
http://10.100.14.6:8082/v1/graphql
```

![image](https://github.com/user-attachments/assets/3eed4cca-a995-4fe2-9553-ba6312627d85)


### 4. Tulis Query untuk Remote Schema di Body
Di bagian Body, pilih opsi raw dan pilih format JSON. Kemudian, masukkan query yang akan mengakses remote schema yang telah ditambahkan di Hasura.

Misalnya, jika Anda ingin melakukan query ke remote schema bernama remote_schema_example, query-nya bisa seperti ini:

Contoh Query Sederhana:

```json
{
  "query": "query MyRemoteSchemaQuery { remote_schema_example { field1 field2 } }"
}
```

Berikut Outputnya:

![image](https://github.com/user-attachments/assets/0c9fd23b-af83-48d4-a4f8-4d2cb3cde9f7)

