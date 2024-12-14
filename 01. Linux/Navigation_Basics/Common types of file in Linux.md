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

Setiap perangkat keras dalam sistem memiliki file yang terkait di direktori `/dev`. File ini digunakan oleh sistem untuk berkomunikasi dengan perangkat kera tersebut. File ini dikenal sebagai **file perangkat**.

#### Jenis file perangkat

Terdapat dua jenis file perangkat:
1. **File perangkat Karakter** (character / raw )
2. **File perangkat Blok** (Block)

Contoh output perintah `ls`:

```bash
root@server:~# ls -l /dev/console
crw--w---- 1 root tty 5, 1 Nov 27 00:23 /dev/console
root@server:~# ls -l /dev/sda
brw-rw---- 1 root disk 8, 0 Nov 27 00:23 /dev/sda
root@server:~#
```

- Huruf **"c"**: Menandakan **file perangkat karakter**.
- Huruf **"b"**: Menandakan **file perangkat blok**.

#### Menggunakan Perintah `file` dan `stat`

Untuk mengetahui tipe file lebih detail, kita bisa menggunakan perintah `file`, dan `stat`:

```bash
root@server:~# file /dev/console
/dev/console: character special (5/1)
root@server:~# stat /dev/console
  File: /dev/console
  Size: 0               Blocks: 0          IO Block: 4096   character special file
Device: 0,5     Inode: 13          Links: 1     Device type: 5,1
Access: (0620/crw--w----)  Uid: (    0/    root)   Gid: (    5/     tty)
Access: 2024-11-27 00:23:37.075447559 +0000
Modify: 2024-11-27 00:23:37.075447559 +0000
Change: 2024-11-27 00:23:37.075447559 +0000
 Birth: 2024-11-06 05:02:02.296000003 +0000
root@server:~# file /dev/sda
/dev/sda: block special (8/0)
root@server:~# stat /dev/sda
  File: /dev/sda
  Size: 0               Blocks: 0          IO Block: 4096   block special file
Device: 0,5     Inode: 328         Links: 1     Device type: 8,0
Access: (0660/brw-rw----)  Uid: (    0/    root)   Gid: (    6/    disk)
Access: 2024-12-11 06:52:08.943709920 +0000
Modify: 2024-11-27 00:23:37.114447127 +0000
Change: 2024-11-27 00:23:37.114447127 +0000
 Birth: 2024-11-06 05:02:07.443000168 +0000
root@server:~#

```

- **Perintah `file /dev/console`** akan memberikan informasi spesifik mengenai tipe data dalam file, misalnya: `character special (5/1)`.
- **character special**: Tipe file ini adalah perangkat character yang membaca/menulis data satu karakter dalam satu waktu, seperti terminal atau konsol.
- **Perintah `stat /dev/console`** akan melaporkan bahwa file tersebut adalah **character special**.

```bash
Device type: 5,1
Access: (0620/crw--w----)  Uid: (0/root)   Gid: (5/tty)
```
- **Device type (5,1)**: Kolom ini menunjukkan kombinasi major dan minor number.
- **Group `tty`**: Ini menunjukkan bahwa group tty memiliki akses write-only ke perangkat ini.
- Konsol digunakan oleh kernel untuk menampilkan pesan sistem dan input/output terminal utama.

---

#### Major dan Minor Number

Setiap perangkat keras seperti disk, CD/DVD, printer, dan terminal memiliki **device driver** yang dimuat di kernel. Kernel berkomunikasi dengan perangkat keras melalui driver tersebut.

- **Major Number**: Nomor unik yang digunakan kernel untuk mengenali jenis driver perangkat.  
- **Minor Number**: Nomor yang mengidentifikasi perangkat atau partisi spesifik dalam kategori driver tersebut.  

Contoh:

- **Major Number 8**: Driver untuk **perangkat blok SATA**.  
- **Major Number 253**: Driver untuk **device mapper** (VDO volume, LVM logical volumes, dll.).  
- **Major Number 11**: Driver untuk **perangkat optik** (CD/DVD).  

Kolom ke-5 dan ke-6 dalam output `ls -l` menunjukkan **major number** dan **minor number**.

---

### Tautan Simbolik (Symbolic Link)

**Tautan simbolik** (disebut juga **soft link** atau **symlink**) adalah referensi atau pintasan ke file atau direktori lain.  

Jika kita menjalankan perintah `ls -l` pada file atau direktori yang memiliki tautan simbolik, outputnya akan dimulai dengan huruf **"l"**, dan terdapat tanda panah (->) yang menunjukkan target tautan. Contoh:

```bash
root@server:~# ls -l /usr/sbin/vigr
lrwxrwxrwx 1 root root 4 Apr  9  2024 /usr/sbin/vigr -> vipw
root@server:~#
```

- Huruf **"l"**: Menandakan file tersebut adalah **tautan simbolik**.  
- **Panah "->"**: Menunjukkan lokasi target dari tautan tersebut.

### Perintah `file` dan `stat` pada Tautan Simbolik

Untuk memastikan file tersebut adalah tautan simbolik, jalankan perintah berikut:

```bash
root@server-eric:~# file /usr/sbin/vigr
/usr/sbin/vigr: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=xxxxxxxxxxxxxxxx, stripped
root@server-eric:~# stat /usr/sbin/vigr
  File: /usr/sbin/vigr -> vipw
  Size: 4               Blocks: 0          IO Block: 4096   symbolic link
Device: 252,1   Inode: 1187771     Links: 1
Access: (0777/lrwxrwxrwx)  Uid: (    0/    root)   Gid: (    0/    root)
Access: 2024-12-13 06:49:15.790004806 +0000
Modify: 2024-04-09 07:01:02.000000000 +0000
Change: 2024-09-10 02:31:28.229842382 +0000
 Birth: 2024-09-10 02:31:28.229842382 +0000
root@server-eric:~#
```

Output akan menunjukkan bahwa file tersebut adalah **symbolic link**.

---

**Source: `RHCSA® Red Hat® Enterprise Linux® 8 (UPDATED) Training and Exam Preparation Guide, EX200, Edisi Kedua, November 2020`**

`Hal: 127-131`
