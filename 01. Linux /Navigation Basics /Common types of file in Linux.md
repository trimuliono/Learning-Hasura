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
root@server:~# ls -l
-rw-r--r-- 1 root root 1234 Jun 12 14:00 contoh_file.txt
root@server:~#
```

Perhatikan tanda hubung (`-`) di kolom pertama sebelum `rw`. Tanda ini menunjukkan bahwa file tersebut adalah **file reguler**.

#### Menggunakan Perintah `file` dan `stat`

Untuk mengetahui tipe file lebih detail, kita bisa menggunakan perintah `file`, dan `stat`:

```bash
root@server:~# file contoh_file.txt
contoh_file.txt: ASCII text
root@server:~# stat contoh_file.txt
  File: contoh_file.txt
  Size: 52              Blocks: 8          IO Block: 4096   regular file
Device: 252,1   Inode: 1502382     Links: 1
Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (    0/    root)
Access: 2024-12-06 03:40:59.596756961 +0000
Modify: 2024-10-25 04:21:43.456372700 +0000
Change: 2024-10-25 04:21:43.456372700 +0000
 Birth: 2024-10-25 04:21:43.456372700 +0000
root@server:~#

```

- **Perintah `file`** akan memberikan informasi spesifik mengenai tipe data dalam file, misalnya: `ASCII text`.  
- **Perintah `stat`** akan melaporkan bahwa file tersebut adalah **file reguler**.

---

### File Direktori

Direktori adalah wadah yang menyimpan  file dan subdirektori. Contoh output perintah `ls` di direktori `/usr/bin` akan menunjukkan beberapa direktori.
Contoh:

```bash
root@server:~# ls -l
drwxr-xr-x 2 root root 4096 Jun 12 10:30 example_directory
root@server:~#
```

Pada output di atas:
- Huruf **"d"** di awal setiap baris menandakan bahwa file tersebut adalah **direktori**.

#### Menggunakan Perintah `file` dan `stat`

Untuk mengetahui tipe file lebih detail, kita bisa menggunakan perintah `file`, dan `stat`:

```bash
root@server:~# file /usr
/usr: directory
root@server:~# stat /usr
  File: /usr
  Size: 4096            Blocks: 8          IO Block: 4096   directory
Device: 252,1   Inode: 1179649     Links: 13
Access: (0755/drwxr-xr-x)  Uid: (    0/    root)   Gid: (    0/    root)
Access: 2024-12-11 03:36:43.358392726 +0000
Modify: 2024-09-27 03:11:26.109060136 +0000
Change: 2024-09-27 03:11:26.109060136 +0000
 Birth: 2024-09-10 02:31:16.164929116 +0000
root@server:~#

```

- **Perintah `file`** akan memberikan informasi spesifik mengenai tipe data dalam file, misalnya: `directory`.  
- **Perintah `stat`** akan melaporkan bahwa file tersebut adalah **directory**.

---

### File Perangkat Blok dan Karakter
