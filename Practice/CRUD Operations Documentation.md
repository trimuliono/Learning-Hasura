# Toko Online - CRUD Operations Documentation


### Overview
Proyek ini adalah implementasi sederhana dari sistem Toko Online dengan operasi CRUD (Create, Read, Update, Delete) yang diimplementasikan menggunakan **Hasura GraphQL**. Database yang digunakan adalah **MySQL** dan terhubung dengan Hasura untuk memungkinkan mutasi CRUD.

### Struktur Tabel dan Relasi

![image](https://github.com/user-attachments/assets/9db2b428-403b-4412-be3b-ae3046870041)

#### Relasi antar Tabel
- `Users (1) -> Addresses (1)`
- `Users (1) —> Orders (N)`
- `Orders (1) —> OrderItems (N)`
- `Products (1) —> OrderItems (N)`

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

#### Contoh Pembuatan Tabel dengan SQL DBeaver:

1. **Create Table `Users`** di DBeaver:
 
```sql
CREATE TABLE Users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  username VARCHAR(50) NOT NULL,
  email VARCHAR(100) NOT NULL,
  password VARCHAR(255) NOT NULL
);
```

2. **Create Table `Products`** di DBeaver:
 
```sql
CREATE TABLE Products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    stock INT NOT NULL
);
```

3. **Create Table `Orders`** di DBeaver:
 
```sql
CREATE TABLE Orders (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    order_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(id)
);
```

4. **Create Table `OrderItems`** di DBeaver:
 
```sql
CREATE TABLE OrderItems (
    id INT AUTO_INCREMENT PRIMARY KEY,
    order_id INT,
    product_id INT,
    quantity INT NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (order_id) REFERENCES Orders(id),
    FOREIGN KEY (product_id) REFERENCES Products(id)
);
```

5. **Create Table `Addresses`** di DBeaver:
 
```sql
CREATE TABLE Addresses (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT UNIQUE, -- Foreign key harus unique agar menjaga relasi one-to-one
    street VARCHAR(255),
    city VARCHAR(100),
    postal_code VARCHAR(20),
    country VARCHAR(100),
    FOREIGN KEY (user_id) REFERENCES Users(id)
);
```


### CRUD Operations

#### untuk melakukan perubahan data pada database, graphql menggunakan fungsi mutation. berikut adalah contoh query mutasi untuk insert data:

Berikut adalah operasi CRUD di graphQL untuk masing-masing entitas di Toko Online.

#### 1. Users

Kita harus mulai dengan memasukkan data ke tabel Users, karena tabel ini adalah pusat dari relasi yang terhubung ke banyak tabel lain (seperti Orders dan Addresses).

- **Create User**
  ```graphql
  mutation {
    insert_Users(object: {
      username: "dodo",
      email: "dodo@example.com",
      password: "hashed_password"
    }) {
      id
      username
      email
    }
  }
  ```
  Berikut adalah outputnya:
  ![image](https://github.com/user-attachments/assets/c327f8cd-d6dc-4045-9c78-f93cdaca9420)

#### 2. Addresses

Setelah data pengguna dimasukkan, kita dapat memasukkan alamat terkait ke tabel Addresses. Karena ini adalah relasi One-to-One dengan Users, kita perlu menggunakan foreign key user_id.

Untuk mutasi ini dilakukan menggunakan Query Variables dimana user_id bertipe Int secara eksplisit. Hal ini dilakukan untuk mengatasi  GraphQL yang terkadang salah membaca tipe data langsung di dalam mutasi, dimana dalam case ini int terbaca float.

- **Create Addresses**
  ```graphql
    mutation InsertAddress($user_id: Int!) {
    insert_Addresses(objects: {
      user_id: $user_id,  
      street: "123 Main St",
      city: "New York",
      postal_code: "10001",
      country: "USA"
    }) {
      affected_rows
      returning {
        id
        user_id
        street
        city
      }
    }
  }
  ```

Lalu, di bagian Query Variables (biasanya di bagian bawah panel GraphQL):
  ```json
    {
      "user_id": 10
    }
  ```

  Berikut adalah outputnya:
  ![image](https://github.com/user-attachments/assets/36f36391-9cc5-4d2d-aa82-2ec723c51ded)

#### 3. Products

Sebelum kita bisa membuat pesanan (order), kita perlu menambahkan produk ke tabel Products, karena setiap item pesanan akan mereferensikan produk.

- **Create Products**
  ```graphql
    mutation InsertProduct {
    insert_Products(objects: {
      name: "Laptop", 
      price: 15000000, 
      stock: 20
    }) {
      affected_rows
      returning {
        id
        name
        price
        stock
      }
    }
  }
  ```
  Berikut adalah outputnya:
  ![image](https://github.com/user-attachments/assets/36414a38-5312-4f62-b27f-f1eefbb7e7fd)

#### 4. Orders

Setelah kita memiliki pengguna dan produk, kita bisa memasukkan pesanan ke tabel Orders. Relasi Orders dengan Users adalah One-to-Many, di mana setiap pesanan mengacu pada user_id.

Untuk mutasi ini dilakukan menggunakan Query Variables dimana user_id bertipe Int secara eksplisit. Hal ini dilakukan untuk mengatasi  GraphQL yang terkadang salah membaca tipe data langsung di dalam mutasi, dimana dalam case ini int terbaca float.

- **Create Orders**
  ```graphql
  mutation InsertOrder($user_id: Int!) {
    insert_Orders(objects:  {
      user_id: $user_id,  # ID pengguna yang diinsert pada mutasi pertama
      order_date: "2024-09-01"
    }) {
      affected_rows
      returning {
        id
        user_id
        order_date
      }
    }
  }
  ```

Lalu, di bagian Query Variables (biasanya di bagian bawah panel GraphQL):
  ```json
    {
      "user_id": 10
    }
  ```
  Berikut adalah outputnya:
  ![image](https://github.com/user-attachments/assets/379d404f-d5c7-40eb-a267-25527ad2c14c)


#### 5. OrderItems

Terakhir, kita perlu menambahkan item pesanan ke tabel OrderItems, di mana setiap item pesanan mengacu pada order_id (dari tabel Orders) dan product_id (dari tabel Products).

Untuk mutasi ini dilakukan menggunakan Query Variables dimana user_id bertipe Int secara eksplisit. Hal ini dilakukan untuk mengatasi  GraphQL yang terkadang salah membaca tipe data langsung di dalam mutasi, dimana dalam case ini int terbaca float.

- **Create OrderItems**
  ```graphql
    mutation InsertOrderItem($order_id: Int!, $product_id: Int!) {
    insert_OrderItems(objects: {
      order_id: $order_id,  # Menggunakan variabel
      product_id: $product_id,  # Menggunakan variabel
      quantity: 2, 
      price: 30000000
    }) {
      affected_rows
      returning {
        id
        order_id
        product_id
        quantity
        price
      }
    }
  }
  ```

Lalu, di bagian Query Variables (biasanya di bagian bawah panel GraphQL):
  ```json
  {
    "order_id": 10,
    "product_id": 6
  }
  ```
  Berikut adalah outputnya:
  ![image](https://github.com/user-attachments/assets/04a4a25c-b020-482d-a7ef-ce2819854ac2)


