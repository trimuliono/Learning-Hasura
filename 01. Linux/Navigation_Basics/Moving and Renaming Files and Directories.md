# Moving and Renaming Files and Directories

File atau direktori dapat dipindahkan dalam sistem file yang sama atau ke sistem file lain. Dalam pemindahan dalam sistem file, sebuah entri ditambahkan ke direktori target dan entri sumber dihapus, sehingga data sebenarnya tetap utuh. Di sisi lain, pemindahan ke sistem file yang berbeda secara fisik memindahkan konten file atau direktori ke lokasi baru dan menghapus sumbernya.

## Memindahkan dan Mengganti Nama File

Perintah `mv` digunakan untuk memindahkan atau mengganti nama file. Opsi `-i` dapat ditentukan untuk konfirmasi pengguna jika file dengan nama tersebut sudah ada.

**Memindahkan File**:

```bash
root@server:~# mv renamed.txt dir1/
root@server:~# ls dir1
renamed.txt
root@server:~#
```

**Mengganti nama File**:

```bash
root@server:~# mv file.txt renamed.txt
root@server:~# ls -l renamed.txt
-rw-r--r-- 1 root root 0 Dec 16 05:02 renamed.txt
root@server:~#
```






---
**Source: `RHCSA® Red Hat® Enterprise Linux® 8 (UPDATED) Training and Exam Preparation Guide, EX200, Edisi Kedua, November 2020`**

`Hal: 149`
---
