# Connect Remote Schemas Graphql

rabu 18/09/2024
remote schemas mas verdy, lakukan query remote schema tersebut pake postman
deadline: besok jam 4 sore

Untuk melakukan query remote schema melalui Hasura menggunakan Postman, Anda harus memahami bahwa query remote schema dilakukan melalui endpoint Hasura, bukan langsung ke endpoint remote schema tersebut. Hasura bertindak sebagai proxy yang menghubungkan ke remote schema yang telah ditambahkan.

Berikut adalah langkah-langkah detail yang harus dilakukan untuk mengirim query ke remote schema di Hasura melalui Postman:

### 1. Pastikan Remote Schema Sudah Ditambahkan di Hasura
Sebelum melakukan query dari Postman, pastikan bahwa remote schema di Hasura sudah dikonfigurasi dengan benar. Untuk menambahkannya:

Buka Hasura Console.
Navigasi ke Remote Schemas dan tambahkan remote schema dengan URL remote shcemas yang ingin dihubungkan
Berikan nama untuk remote schema ini, misalnya: remote_schema_example.

![image](https://github.com/user-attachments/assets/08f6a45a-7f08-4577-ab08-173ef9080a95)

![image](https://github.com/user-attachments/assets/5f5cef13-f6d0-4d6a-a1f2-3c20cf510ab3)

![image](https://github.com/user-attachments/assets/b9e12f54-8b63-4dbd-925f-97cfb69f5d2a)

![image](https://github.com/user-attachments/assets/bc3cf647-82f7-4a75-90ae-27093cfc9eda)

### 2. URL Endpoint Hasura di Postman
Dalam Postman, Anda akan mengirimkan request ke endpoint GraphQL Hasura, bukan langsung ke remote schema. Endpoint-nya adalah:

```bash
http://10.100.14.6:8082/v1/graphql
```

### 3. Setel Headers di Postman
- Buat request baru di Postman dengan type GraphQL
![image](https://github.com/user-attachments/assets/1e93511c-8d5b-4aaf-b504-5114a41d4f51)

  - Masukkan URL endpoint Hasura:
  
    ```bash
    http://10.100.14.6:8082/v1/graphql
    ```
    ![image](https://github.com/user-attachments/assets/eb3c33f7-364c-4735-8c24-82f461eedabe)

  - Pada bagian Headers, tambahkan key-value `x-hasura-admin-secret`

    ![image](https://github.com/user-attachments/assets/83734c9c-442d-4d5b-958c-42e7777e81b2)

  - Klik Tab `Query` klik `Use GraphQL Introspection`

    ![image](https://github.com/user-attachments/assets/8b4944c3-6065-465c-8777-e76b6dc46644)

maka semua query pada schema akan muncul dan dapat digunakan seperti pada Hasuara Console

![image](https://github.com/user-attachments/assets/aec6e405-dc82-4fa2-bbc5-1d45a23b974f)


### 4. Tes Query Remote Shcemas

  #### Query Using GraphQL Request
  Untuk melakukan `query` dapat dilakukan dengan dua cara yang sama seperti pada hasura console, yaitu dapat dengan men-klik pada
  checkbox query di sebelah kiri atau dapat langsung mengetik query secara langsung di sebelah kanan.
  Dalam hal ini, akan saya contohkan untuk `query table todos`
  
  ```json
  query Todos {
      todos {
          id
          text
          done
      }
  }
  ```
  ![image](https://github.com/user-attachments/assets/aa1b2738-c126-446c-acbc-d88b58a33fa1)
  
  Berikut Outputnya:
  
  ![image](https://github.com/user-attachments/assets/1aa20e0a-9d33-4c54-84ec-7714ea06b51d)
  
  #### Query Using HTTP Request
  Selain menggunakan GraphQL Request, query juga dapat dilakukan dengan HTTP Request. Untuk penulisan query juga bisa dilakukan dengan
  format GraphQL maupun format Json.
  
  Berikut contoh Untuk Query Using HTTP Request dengan input body format GraphQL:
  
  ![image](https://github.com/user-attachments/assets/783b3813-ece8-4515-993d-add6e10a25d2)
  
  Berikut contoh Untuk Query Using HTTP Request dengan input body format Json:
  
  ![image](https://github.com/user-attachments/assets/0dcaaa1d-fac4-4dff-8fa9-dc7b0fe7ad78)

### 5. Analisis Query GraphQL

#### Schema: todosGraphql

##### Query 1: GetAllTodos

```graphql
query tri_GetAllTodos {
    todos {
      done
      id
      text
      user {
        id
        name
      }
    }
  }
```
**Penjelasan:** Query ini digunakan untuk mengambil semua data dari tabel todos beserta data usernya dikarenakan query diatas dijoinkan dengan tabel users. Setiap todo yang diambil akan menampilkan informasi status (done), ID todo (id), teks todo (text), serta data pengguna yang terkait dengan todo tersebut (ID dan nama pengguna).

Berikut adalah hasil ketika diterapkan pada GraphQL di Postman:

![image](https://github.com/user-attachments/assets/b2759020-49b8-4e7a-9383-5d194aefcbb6)

##### Query 2: GetAllUsers

```graphql
query tri_GetAllUsers {
    users {
      id
      name
    }
  }
```
**Penjelasan:** Query ini mengambil seluruh data pengguna (users) dari schema todosGraphql. Hanya dua atribut yang ditampilkan, yaitu ID pengguna (id) dan nama pengguna (name).

Berikut adalah hasil ketika diterapkan pada GraphQL di Postman:

![image](https://github.com/user-attachments/assets/86aa89f0-b414-48ce-bac2-53a19a262e89)
Dari hasil di atas dapat diketahui bahwa jumlah data pada tabel users adalah satu.

##### Query 3: todoByPK

```graphql
query tri_todoByPK {
    todo(id: "1") {
      done
      id
      text
      user {
        id
        name
      }
    }
    users {
      id
    }
  }
```  

**Penjelasan:** Query ini mengambil data todo berdasarkan primary key, untuk pk pada tabel ini yaitu kolom `id`, dalam hal ini todo dengan ID "1". Informasi yang diambil meliputi status (done), ID (id), teks todo (text), dan data pengguna terkait (id dan name). Selain itu, query ini juga mengambil semua ID pengguna yang ada di dalam tabel users.

Berikut adalah hasil ketika diterapkan pada GraphQL di Postman:

![image](https://github.com/user-attachments/assets/13167c4c-1dbf-4c7a-a252-ea3314ea8007)
Dari hasil di atas dapat diketahui bahwa data dengan `id = 1` tabel `todos` adalah user dengan nama **ferdy**.

#### Schema: springbootGraphql

##### Query 1: countAuthorsAndTutorials

 ```graphql
query tri_countAuthorsAndTutorials {
    countAuthors
    countTutorials
}
```

**Penjelasan:** Query ini digunakan untuk menghitung total jumlah penulis (countAuthors) dan jumlah tutorial (countTutorials) di schema springbootGraphql.

Berikut adalah hasil ketika diterapkan pada GraphQL di Postman.

![image](https://github.com/user-attachments/assets/0cc908c3-b998-43ac-8e4e-51e8a27970a2)
Dari hasil di atas dapat diketahui bahwa terdapat 1 row pada tabel `Authors` dan 2 rows pada tabel `Tutorials`.

##### Query 2: getAllAuthors

```graphql
query tri_getAllAuthors {
    findAllAuthors {
      age
      id
      name
    }
}
```

**Penjelasan:** Query ini mengambil semua data penulis (findAllAuthors). Setiap penulis akan menampilkan informasi berupa umur (age), ID penulis (id), dan nama penulis (name).

Berikut adalah hasil ketika diterapkan pada GraphQL di Postman.

![image](https://github.com/user-attachments/assets/5c91ae52-89cf-4d25-9f65-8213a92aac10)
Dari hasil di atas dapat diketahui bahwa terdapat 1 Author dengan data usia = 27, id = 1, dan nama = "bezkoder".

