# File Editing with Vim

Vim (Vi Improved) adalah editor teks yang kuat dan fleksibel yang digunakan dalam sistem mirip Unix. Vim dibangun di atas editor Vi asli dengan fitur dan peningkatan tambahan, termasuk pembatalan multi-level, penyorotan sintaksis, dan serangkaian perintah ekstensif untuk manipulasi teks.

## Mode of Operation

Editor `vim` memiliki tiga mode operasi:

- **Normal** (untuk navigasi dan manipulasi)

![1734410516930](image/EditingFileswithVim/1734410516930.png)

- **Insert** (untuk editing teks)

![1734410555337](image/EditingFileswithVim/1734410555337.png)

- **Command** (untuk menjalankan perintah)

![1734410595186](image/EditingFileswithVim/1734410595186.png)

---

## Startting Vim

Editor vim dapat dimulai dengan mengetikkan perintah vim pada perintah prompt, dan mungkin mengikuti nama file yang sudah ada atau nama file baru sebagai argumen. Tanpa nama file tertentu, itu hanya membuka layar kosong di mana Kita bisa memasukkan teks. Kita dapat menyimpan teks dalam file atau membuang menggunakan perintah yang disediakan di subbagian selanjutnya.

```bash
root@server:~# vim
```

Output:

![1734406443266](image/EditingFileswithVim/1734406443266.png)

Alternatifnya, Kita dapat memberikan nama file sebagai argumen. Dengan cara ini, vim akan membuka file yang ditentukan untuk diedit jika file tersebut ada, atau  akan membuat file dengan  nama itu jika tidak ada.

```bash
root@server:~# vim tes.txt
```

Output:

![1734406672841](image/EditingFileswithVim/1734406672841.png)

---

## Inserting text

Secara default saat awal dijalankan, editor vim akan masuk dalam `mode normal`. ada enam perintah yang dapat digunakan untuk pindah ke `mode insert`.

| Command | Action                                     |
|---------|--------------------------------------------|
| **i**   | Insert text sebelum posisi kursor saat ini |
| **I**   | Insert text di awal baris saat ini         |
| **a**   | Insert teks setelah posisi kursor saat ini |
| **A**   | Insert teks di akhir baris saat ini        |
| **o**   | Insert baris baru di bawah baris  saat ini |
| **O**   | Insert baris baru di atas baris saat ini   |

Untuk keluar dari mode insert ketika sudah selesai mengisi teks gunakan tombol `ESC`.

---

## Navigasi dalam Normal Mode

Navigasi dalam **Normal Mode** digunakan untuk **bergerak di dalam teks** atau **memanipulasi teks** menggunakan kombinasi tombol navigasi. Mode ini adalah mode default saat Kita membuka file di Vim.

### **Navigasi Dasar**  
| Tombol          | Fungsi                                   |
|-----------------|------------------------------------------|
| `h`            | Geser kursor ke kiri.                    |
| `l`            | Geser kursor ke kanan.                   |
| `j`            | Geser kursor ke bawah (baris berikutnya).|
| `k`            | Geser kursor ke atas (baris sebelumnya). |

### **Navigasi Cepat**  
| Perintah        | Fungsi                                   |
|-----------------|------------------------------------------|
| `0`            | Pindah ke awal baris.                    |
| `$`            | Pindah ke akhir baris.                   |
| `w`            | Lompat ke awal kata berikutnya.          |
| `b`            | Lompat ke awal kata sebelumnya.          |
| `gg`           | Pindah ke awal file.                     |
| `G`            | Pindah ke akhir file.                    |
| `:n`           | Lompat ke baris ke-`n`. (Contoh: `:5`).   |
| `Ctrl + d`     | Scroll turun setengah layar.             |
| `Ctrl + u`     | Scroll naik setengah layar.              |

---

## **Menghapus Teks di Vim**

Vim menyediakan beberapa perintah untuk melakukan operasi penghapusan teks. Perintah-perintah ini membantu Kita menghapus karakter, kata, atau baris secara efisien.


### **Tabel Perintah Menghapus Teks**

| **Perintah**   | **Aksi**                                                             |
|----------------|----------------------------------------------------------------------|
| `x`           | Menghapus karakter di posisi kursor.                                 |
| `X`           | Menghapus karakter sebelum posisi kursor.                            |
| `dw`          | Menghapus kata atau bagian kata di sebelah kanan posisi kursor.      |
| `dd`          | Menghapus seluruh baris tempat kursor berada.                        |
| `D`           | Menghapus teks dari posisi kursor hingga akhir baris saat ini.       |
| `:6,12d`      | Menghapus baris 6 hingga baris 12. *(Mode Command)*                  |

---

## **Membatalkan (Undo) dan Mengulangi (Repeat) Perintah di Vim**

Vim menyediakan perintah untuk membatalkan perubahan terakhir (**Undo**) dan mengulangi perintah yang terakhir dijalankan (**Repeat**). Tabel berikut menjelaskan perintah-perintah tersebut.


### **Tabel Perintah Undo dan Repeat**

| **Perintah**    | **Aksi**                                                         |
|-----------------|------------------------------------------------------------------|
| `u`            | Membatalkan (undo) perintah terakhir.                            |
| `U`            | Membatalkan semua perubahan yang dilakukan pada baris saat ini.  |
| `:u`           | Membatalkan perintah mode baris terakhir. *(Mode Command)*       |
| `.` (titik)    | Mengulangi perintah terakhir yang dijalankan.                    |

---

## **Mencari Teks di Vim**

Di Vim, Kita dapat melakukan **pencarian maju** atau **pencarian mundur** saat berada di **Normal Mode** menggunakan karakter `/` atau `?` diikuti dengan teks yang ingin dicari. 

---

### **Tabel Perintah Pencarian Teks**

| **Perintah**     | **Aksi**                                                       |
|------------------|----------------------------------------------------------------|
| `/string`        | Mencari **maju** ke arah bawah untuk string tertentu.          |
| `?string`        | Mencari **mundur** ke arah atas untuk string tertentu.         |
| `n`              | Menemukan kemunculan **berikutnya** dari string yang dicari.   |
| `N`              | Menemukan kemunculan **sebelumnya** dari string yang dicari.   |

---

**Source: `RHCSA® Red Hat® Enterprise Linux® 8 (UPDATED) Training and Exam Preparation Guide, EX200, Edisi Kedua, November 2020`**

`Hal: 136-142`
---
