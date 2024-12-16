# File and Directory Operations

Dokumentasi ini menjelaskan berbagai operasi manajemen yang  dapat dilakukan pada file dan direktori. Operasi-operasi ini meliputi membuat, menampilkan isi, menyalin, memindahkan, mengganti nama, dan menghapus file maupun direktori.

## Membuat File dan Direktori

File dapat dibuat dengan berbagai cara menggunakan perintah yang berbeda; namun, hanya ada satu cara untuk membuat direktori.

### Membuat File kosong dengan `touch`

Perintah `touch` akan membuat sebuah file kosong. Jika file tersebut sudah ada, perintah ini hanya akan memperbarui timestamp pada file tersebut agar sesuai dengan tanggal dan waktu sistem saat ini.

Contoh:

```bash
root@server:~# touch file1
root@server:~# ls -l file1
-rw-r--r-- 1 root root 0 Dec 16 02:41 file1
root@server:~# touch file1
root@server:~# ls -l file1
-rw-r--r-- 1 root root 0 Dec 16 02:42 file1
root@server:~#
```

### Membuat File dengan `echo`

Perintah `echo` secara default akan menambahkan baris baru dalam isi file yang dibuat jika tidak diberi perintah eksplisit dengan `-n`

Contoh:

```bash
root@server:~# echo > file1
root@server:~# ls -l file1
-rw-r--r-- 1 root root 1 Dec 16 02:41 file1
root@server:~# echo -n > file2
root@server:~# ls -l file2
-rw-r--r-- 1 root root 0 Dec 16 02:42 file2
root@server:~#
```

### Membuat File dengan `cat`

Perintah `cat` (concatenate) digunakan untuk menampilkan, menggabungkan, atau menulis konten file. Perintah ini juga bisa digunakan untuk membuat file baru dan menambahkan konten ke dalamnya.

Contoh:

```bash
root@server:~# cat > file1
root@server:~# ls -l file1
-rw-r--r-- 1 root root 0 Dec 16 02:41 file1
root@server:~#
```

- Setelah menjalankan perintah **cat > file1** terminal akan menunggu input user.
- Ketik konten yang ingin dimasukkan, atau langsung;
- Tekan **Ctrl + D** untuk menyimpan dan keluar.
- `>` adalah operator **redirect** yang menulis output ke file.
- Jika file belum ada, maka file baru akan dibuat.
- Jika file sudah ada, konten lama akan **ditimpa**.

---

### Membuat Direktori 

Untuk membuat direktori pada linux hanya terdapat satu perintah utama yaitu `mkdir`. Perintah ini memungkinkan user untuk membuat satu atau beberapa direktori sekaligus.

Contoh:

```bash
root@server:~# mkdir dir1
root@server:~# mkdir -v dir2
mkdir: created directory 'dir2'
root@server:~# mkdir -vp dir3/subdir1/subsubdir1
mkdir: created directory 'dir3'
mkdir: created directory 'dir3/subdir1'
mkdir: created directory 'dir3/subdir1/subsubdir1'
root@server:~# mkdir -v dir4 dir5 dir6
mkdir: created directory 'dir4'
mkdir: created directory 'dir5'
mkdir: created directory 'dir6'
root@server:~#
```

| Opsi  | Deskripsi                                       |
|-------|-------------------------------------------------|
| `-p`  | Membuat direktori bersarang (parent directories) jika belum ada. |
| `-v`  | Menampilkan pesan setiap direktori yang dibuat. |
| `--help` | Menampilkan panduan penggunaan `mkdir`.      |

---

**Source: `RHCSA® Red Hat® Enterprise Linux® 8 (UPDATED) Training and Exam Preparation Guide, EX200, Edisi Kedua, November 2020`**

`Hal: 142-144`
---
