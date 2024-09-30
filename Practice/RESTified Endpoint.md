# RESTified Endpoint

RESTified Endpoints di Hasura adalah fitur yang memungkinkan pengguna untuk membuat endpoint REST dari query atau mutation GraphQL yang ada, sehingga data dapat diakses dengan REST API tanpa harus menuliskan query graphql secara manual.

## Membuat REST Endpoints
Hal ini ini dapat dilakukan dengan beberapa langkah.

**1. Buka Tab `API` pada console hasura**
**2. Pada tab API, klik tab `REST` kemudian klik Button `Create Rest`**

![image](https://github.com/user-attachments/assets/734ec20d-a40c-40fc-a896-40de403ed112)

**3. Pada bagian `GraphQL Request` masukkan GraphQL queries atau mutations yang ingin dibuat Rest Endpoint nya. **

![image](https://github.com/user-attachments/assets/e000faac-298f-4e09-bfe0-094a52a2087b)

**4. Berikan nama, deskripsi, URL path, dan Method**

![image](https://github.com/user-attachments/assets/366081e4-d8a3-4629-a5df-5856b49ada9c)

Maka RESTified Endpoint, telah berhasil dibuat.

**Contoh RESTified Endpoint yang telah berhasil dibuat.**

![image](https://github.com/user-attachments/assets/91f3b0df-8096-4636-915c-f3a74c3b69fb)

## Pengujian RESTified Endpoint Menggunakan Postman

**1. Contoh RESTified Endpoint Query Join**

![image](https://github.com/user-attachments/assets/381b8d01-d8a3-44fd-a2a8-61b0782f340b)

**2. Contoh RESTified Endpoint Query FindAll**

![image](https://github.com/user-attachments/assets/e13ca7f0-763e-4cfc-ac2a-1dcd94f2ba16)

**3. Contoh RESTified Endpoint Query find todo using where by id**

![image](https://github.com/user-attachments/assets/0e655728-3707-40fe-a90b-ac9614d70589)

**4. Contoh RESTified Endpoint Query find todo by id using Parameter**

```graphql
query TrigetTodoById($id: ID!) {
    todo(id: $id) {
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

![image](https://github.com/user-attachments/assets/73b803d0-0848-47c7-9f67-b5e6875fb534)




