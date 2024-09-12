# Contoh isi README.md untuk tugas CRUD Toko Online (dalam format markdown)

readme_content = """
# Toko Online - CRUD Operations Documentation

## Tugas yang Dikerjakan oleh: Tri

### Overview
Proyek ini adalah implementasi sederhana dari sistem Toko Online dengan operasi CRUD (Create, Read, Update, Delete) yang diimplementasikan menggunakan **Hasura GraphQL**. Database yang digunakan adalah **MySQL** dan terhubung dengan Hasura untuk memungkinkan mutasi CRUD.

### Struktur Tabel dan Relasi

#### 1. Users
- **Columns**:
  - `id` (integer, Primary Key, Auto-increment)
  - `username` (string)
  - `email` (string)
  - `password` (string)

#### 2. Products
- **Columns**:
  - `id` (integer, Primary Key, Auto-increment)
  - `name` (string)
  - `price` (integer)
  - `stock` (integer)

#### 3. Orders
- **Columns**:
  - `id` (integer, Primary Key, Auto-increment)
  - `user_id` (foreign key from `Users.id`)
  - `order_date` (date)

#### 4. OrderItems
- **Columns**:
  - `id` (integer, Primary Key, Auto-increment)
  - `order_id` (foreign key from `Orders.id`)
  - `product_id` (foreign key from `Products.id`)
  - `quantity` (integer)
  - `price` (integer)

### CRUD Operations

Berikut adalah operasi CRUD untuk masing-masing entitas di Toko Online.

#### 1. Users

- **Create User**
  ```graphql
  mutation {
    insert_Users_one(object: {
      username: "tri",
      email: "tri@example.com",
      password: "hashed_password"
    }) {
      id
      username
      email
    }
  }
