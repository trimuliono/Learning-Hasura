# Jenis-jenis File Umum di Linux

Linux mendukung berbagai jenis file yang diidentifikasi berdasarkan jenis data yang disimpannya. Ada file yang menyimpan informasi dalam format teks biasa atau biner. Jenis ini sangat umum. Selain itu, ada file lain yang menyimpan informasi perangkat atau hanya menunjuk ke data yang sama pada disk. Pemahaman yang baik tentang jenis file di Linux penting bagi pengguna dan administrator Linux.

---

## Jenis-jenis file di Linux

**RHEL** mendukung tujuh jenis file berikut:

1. **File Reguler**
2. **Direktori**
3. **File perangkat Blok**
4. **File perangkat karakter**
5. **Tautan Simbolik (Symbolyc Link)**
6. **Named Pipe** *(tidak dibahas di sini)*
7. **Socket** *(tidak dibahas di sini)*

Dua jenis file pertama (file reguler dan direktori) adalah yang paling umum di Linux. File perangkat digunakan oleh sistem operasi untuk berkomunikasi dengan perangkat periferal. Tautan simbolik juga sering ditemukan, sedangkan **named pipes** dan **socket** digunakan untuk komunikasi antar proses.

#### Mengenali Jenis File
Linux tidak memerlukan ekstensi untuk mengidentifikasi jenis file. Linux menyediakan tiga perintah utama untuk mengetahui jenis file.
- **file**
- **stat**
- **ls**

### File Reguler
**File Reguler** adalah file yang berisi teks atau data biner. File ini bisa berupa skrip shell atau perintah dalam format biner. Saat kita menjalankan perintah `ls` pada suatu direktori pada `cli`, semua file yang dimulai dengan tanda hubung (`-`) di awal kolom pertama menujukkan file reguler.

Contoh output yang dipersingkat dari direktori `/root`:

```bash
root@server:~# ls -ll
-rw-r--r-- 1 root root 1234 Jun 12 14:00 contoh_file.txt
root@server:~#
```

Perhatikan tanda hubung (`-`) di kolom pertama sebelum `rw`. Tanda ini menunjukkan bahwa file tersebut adalah **file reguler**.
