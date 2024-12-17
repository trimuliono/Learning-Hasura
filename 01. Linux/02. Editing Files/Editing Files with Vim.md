# File Editing with Vim

Vim (Vi Improved) adalah editor teks yang kuat dan fleksibel yang digunakan dalam sistem mirip Unix. Vim dibangun di atas editor Vi asli dengan fitur dan peningkatan tambahan, termasuk pembatalan multi-level, penyorotan sintaksis, dan serangkaian perintah ekstensif untuk manipulasi teks.

## Mode of Operation

Editor `vim` memiliki tiga mode operasi:

- **Normal** (untuk navigasi dan manipulasi)
- **Insert** (untuk editing teks)
- **Command** (untuk menjalankan perintah)

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

**Source: `RHCSA® Red Hat® Enterprise Linux® 8 (UPDATED) Training and Exam Preparation Guide, EX200, Edisi Kedua, November 2020`**

`Hal: 136-`
---
