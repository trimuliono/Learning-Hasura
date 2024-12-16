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

| Opsi       | Deskripsi                                                        |
| ---------- | ---------------------------------------------------------------- |
| `-p`     | Membuat direktori bersarang (parent directories) jika belum ada. |
| `-v`     | Menampilkan pesan setiap direktori yang dibuat.                  |
| `--help` | Menampilkan panduan penggunaan `mkdir`.                        |

---

## Menghapus File dan Direktori

Menghapus file di Linux berarti membuang file yang tidak diinginkan atau tidak perlu dari komputer Anda. Anda menggunakan perintah rm untuk menghapus file, dan itu bersifat permanen, jadi berhati-hatilah. Kita juga dapat menggunakan `rm -i` (interaktif) untuk meminta konfirmasi sebelum menghapus, yang membantu mencegah hilangnya file penting secara tidak sengaja.

**Menghapus 1 file**

```bash
root@server:~# ls file1.txt
file1.txt
root@server:~# rm file1.txt
root@server:~# ls file1.txt
ls: cannot access 'file1.txt': No such file or directory
root@server:~#
```

**Menghapus banyak file**

```bash
root@server:~# ls *.txt
file1.txt  file2.txt  file3.txt
root@server:~# rm file1.txt file2.txt file3.txt
root@server:~# ls *.txt
ls: cannot access '*.txt': No such file or directory
root@server:~#
```

**Menghapus file dengan `-i` untuk keamanan**

```bash
root@server:~# ls *.txt
important_file.txt
root@server:~# rm -i important_file.txt
rm: remove regular empty file 'important_file.txt'? y
root@server:~# ls *.txt
ls: cannot access '*.txt': No such file or directory
root@server:~#
```

---

**Menghapus Direktori kosong dengan `rm -d`**

```bash
root@server:~# rm emptydir/
rm: cannot remove 'emptydir/': Is a directory
root@server:~# rm -d emptydir/
root@server:~# ls emptydir/
ls: cannot access 'emptydir/': No such file or directory
root@server:~#
```

**Menghapus Direktori kosong dengan `rmdir`**

```bash
root@server:~# rm emptydir2/
rm: cannot remove 'emptydir2/': Is a directory
root@server:~# rmdir emptydir2/
root@server:~# ls emptydir2
ls: cannot access 'emptydir2': No such file or directory
root@server:~#
```

**Menghapus Direktori dan semua isi di dalamnya dengan `rm -r` (recursive)**

```bash
root@server:~# ls dir1
file.txt
root@server:~# rmdir dir1
rmdir: failed to remove 'dir1': Directory not empty
root@server:~# rm -r dir1
root@server:~# ls dir1
ls: cannot access 'dir1': No such file or directory
root@server:~#
```

---

**Source: `RHCSA® Red Hat® Enterprise Linux® 8 (UPDATED) Training and Exam Preparation Guide, EX200, Edisi Kedua, November 2020`**

`Hal: 142-150`
---
