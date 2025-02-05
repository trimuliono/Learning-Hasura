# Kerberos, KDC server, phoenix thick client, dan thin client

## 1. Mekanisme Kerberos dan KDC Server

### **Apa itu Kerberos?**
Kerberos adalah protokol autentikasi jaringan yang dirancang untuk menyediakan autentikasi aman menggunakan sistem tiket. Kerberos memungkinkan pengguna untuk membuktikan identitas mereka tanpa mengirimkan kata sandi secara langsung di jaringan.

### **Bagaimana Mekanisme Kerberos Bekerja?**

1. **Client Requests Authentication Ticket (TGT):**
   - Pengguna memasukkan kredensial (username/password).
   - Kredensial ini digunakan untuk meminta _Ticket-Granting Ticket_ (TGT) dari **Key Distribution Center (KDC)**.

2. **KDC Verifies Credentials:**
   - KDC, yang terdiri dari Authentication Server (AS) dan Ticket-Granting Server (TGS), memverifikasi kredensial.
   - Jika valid, KDC mengirimkan TGT yang dienkripsi dengan kunci rahasia KDC.

3. **Client Uses TGT to Request Service Ticket:**
   - Ketika pengguna ingin mengakses layanan, client mengirimkan TGT dan permintaan layanan ke TGS.

4. **TGS Issues Service Ticket:**
   - TGS memverifikasi TGT.
   - Jika valid, TGS mengeluarkan _service ticket_ yang memungkinkan akses ke layanan yang diminta.

5. **Client Accesses the Service:**
   - Client menggunakan service ticket untuk mengakses layanan.
   - Server memverifikasi service ticket tanpa meminta kata sandi tambahan.
  
### **Apa itu KDC Server?**
KDC (Key Distribution Center) adalah komponen utama dalam sistem Kerberos yang bertanggung jawab untuk:
   - Mengautentikasi pengguna melalui Authentication Server (AS).
   - Mengeluarkan tiket layanan melalui Ticket-Granting Server (TGS).

**Kelebihan KDC:**
- Sentralisasi autentikasi.
- Meningkatkan keamanan karena kata sandi tidak pernah dikirim di jaringan.

**Kekurangan KDC:**
- Titik kegagalan tunggal (Single Point of Failure).
- Memerlukan sinkronisasi waktu yang ketat antara server dan client.

---
## 2. Perbedaan Phoenix Thick Client dan Thin Client

### **Apa itu Thick Client?**
Thick client adalah aplikasi yang berjalan pada komputer pengguna dan memiliki banyak logika pemrosesan di sisi client. Contoh: aplikasi desktop.

#### **Kelebihan Thick Client:**
- **Performa lebih baik**: Pemrosesan dilakukan di perangkat lokal.
- **Respon cepat**: Karena sebagian besar logika ada di sisi client.
- **Offline Mode**: Dapat bekerja tanpa koneksi internet dalam beberapa kasus.

#### **Kekurangan Thick Client:**
- **Kompleksitas Deployment**: Perlu diinstal di setiap perangkat pengguna.
- **Pemeliharaan yang rumit**: Perubahan kode harus diupdate secara manual di setiap client.
- **Keamanan lebih rendah**: Data sensitif mungkin lebih rentan di perangkat lokal.

---

### **Apa itu Thin Client?**
Thin client adalah aplikasi yang sebagian besar logikanya berjalan di server, sementara client hanya digunakan untuk interaksi pengguna. Contoh: aplikasi berbasis web.

#### **Kelebihan Thin Client:**
- **Kemudahan Deployment**: Tidak memerlukan instalasi lokal, hanya membutuhkan browser atau koneksi ke server.
- **Pemeliharaan lebih mudah**: Update dilakukan di sisi server dan langsung berlaku untuk semua pengguna.
- **Keamanan lebih tinggi**: Data tetap disimpan di server.

#### **Kekurangan Thin Client:**
- **Ketergantungan pada jaringan**: Membutuhkan koneksi internet atau intranet yang stabil.
- **Respon lebih lambat**: Karena pemrosesan dilakukan di server.
- **Kapasitas server yang besar**: Beban server meningkat saat jumlah pengguna bertambah.

