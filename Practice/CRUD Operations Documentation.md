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

#### 5. Addresses
- **Columns**:
  - `id` (integer, Primary Key, Auto-increment)
  - `user_id` (foreign key from `Users.id`)
  - `street` (string)
  - `city` (string)
  - `postal_code` (string)
  - `country` (string)

### Cara Membuat Tabel Menggunakan DBeaver

#### Langkah-langkah Membuat Tabel di DBeaver:

1. **Buka DBeaver** dan buat koneksi ke database MySQL Anda.
   - Klik kanan pada **database** yang ingin Anda gunakan, lalu pilih **Create -> Table**.

2. **Definisikan Nama Tabel** dan **Kolom**:
   - Masukkan nama tabel (misalnya, `Users`, `Products`, dll.).
   - Tambahkan kolom yang diperlukan dengan menekan tombol **Add** di bagian bawah.
     - Untuk kolom `id`, set **Data Type** sebagai `INT`, centang **Auto Increment** dan **Primary Key**.
     - Tambahkan kolom lainnya seperti `username`, `email`, dan `password` dengan tipe data yang sesuai (`VARCHAR`, `TEXT`, dll.).

3. **Membuat Relasi Foreign Key**:
   - Untuk membuat foreign key, setelah tabel selesai dibuat:
     - Klik kanan pada tabel, pilih **Modify Table**.
     - Pilih **Foreign Keys** di bagian tab bawah, lalu klik **Add** untuk menambahkan foreign key.
     - Tentukan kolom yang ingin Anda hubungkan dengan tabel lain (misalnya, `user_id` di tabel `Orders` mengacu pada `id` di tabel `Users`).

4. **Simpan Tabel**:
   - Setelah semua kolom dan relasi didefinisikan, klik **Save** untuk membuat tabel tersebut di database.

#### Contoh Pembuatan Tabel `Users`:

1. **Create Table `Users`** di DBeaver:
   - Nama Tabel: `Users`
   - Kolom:
     - `id` (INT, Primary Key, Auto Increment)
     - `username` (VARCHAR(50))
     - `email` (VARCHAR(100))
     - `password` (VARCHAR(255))

```sql
CREATE TABLE Users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  username VARCHAR(50) NOT NULL,
  email VARCHAR(100) NOT NULL,
  password VARCHAR(255) NOT NULL
);

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
