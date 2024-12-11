# Struktur Direktori Linux

![image](https://github.com/user-attachments/assets/b76e052d-f940-4e27-a729-f35f928dc285)
Di Linux, semua file dan folder (direktori) **tersusun rapi** seperti pohon terbalik. Pohon ini membantu komputer supaya file lebih mudah **dikelola** dan **ditemukan**.  

Bayangkan seperti ini:  
- **Akar pohon** (root) adalah tempat tertinggi atau paling awal dari semua file di komputer.  
- Dari akar pohon, ada banyak **cabang**. Setiap cabang itu adalah **folder** atau **direktori**.  
- Dari setiap cabang, bisa muncul cabang-cabang **kecil** lagi, itu namanya **subdirektori** atau folder di dalam folder lain.  
- Di ujung cabang, ada **daun**. Nah, daun itu adalah **file** seperti gambar, dokumen, atau lagu.  

Sistem Linux membuat semua ini sangat **teratur**, jadi orang yang merawat komputer mudah tahu **apa isinya** dan **di mana letaknya**. 

---

## Filesystem Hierarchy Standard (FHS)
Filesystem Hierarchy Standard (FHS) adalah standar yang mendefinisikan struktur direktori dan isi dari sistem file pada sistem operasi Linux dan Unix.

File sistem ini dapat dikategorikan kedalam 3 grup dasar: 
- **Sistem file berbasis disk**: Dibuat pada media fisik seperti hard drive atau USB flash drive.
- **Sistem file berbasis jaringan**: Pada dasarnya adalah sistem file berbasis disk yang dibagikan melalui jaringan untuk akses jarak jauh.
- **Sistem file berbasis memori**: Virtual, dibuat otomatis saat sistem dinyalakan dan dihapus saat sistem dimatikan. Data yang disimpan di sini hilang saat sistem reboot.
Sistem file berbasis disk dan jaringan menyimpan informasi secara permanen, sedangkan data di sistem file berbasis memori hilang saat reboot.

### 1. **Root File System Directory (`/`)**, Disk-Based
  - Direktori tingkat atas dalam hierarki sistem file Linux.
  - Semua direktori dan file lainnya berada di bawah direktori ini.

### 2. **/etc**
  - Berisi file konfigurasi sistem dan skrip shell yang digunakan untuk booting dan inisialisasi sistem.
  - Contoh: `passwd`, `fstab`, dan `hosts`.

### 3. **/root**
  - Direktori Home default untuk user root (administrator sistem).

### 4. **/mnt** atau **/media**
  - Ini seperti **garasi**. Kamu bisa menyimpan barang dari luar rumah (`mount`), seperti USB atau hard disk (`sistem file sementara`).

### 5. **The Boot File System (/boot)**, Disk-Based
  - Direktori semua file penting untuk memulai (boot) sistem operasi Linux. Seperti kernel linux, file pendukung boot, dan file konfigurasi boot. 

### 6. **The Home Directory (/home)** 
  - Berisi direktori home dari masing-masing pengguna.
  - Setiap pengguna memiliki subdirektori di bawah `/home`, seperti `/home/user1`. 

### 7. **The Optional Directory (/opt)**
  - Berisi paket perangkat lunak opsional dan aplikasi pihak ketiga.
  - Setiap aplikasi memiliki subdirektori di bawah `/opt`, seperti `/opt/app1`. 

### 8. **The UNIX System Resources Directory (/usr)**
  - Berisi utilitas dan aplikasi pengguna.
  - Subdirektori termasuk `/usr/bin`, `/usr/sbin`, `/usr/lib`, dan `/usr/share`.

### 9. **/usr/bin**
  - Berisibiner perintah penting (eksekusi) yang diperlukan untuk  booting sistem dan mode pengguna tunggal.
  - Contoh: `la`, `cp`, `mv`, dan `rm`.

### 10.  **/usr/sbin**
  - Berisi biner sistem penting yang biasanya digunakan oleh pengguna root untuk administrasi sistem.
  - Contoh: `ifconfig`, `reboot`, dan `shutdown`.

### 11. **/usr/lib dan /usr/lib64**
  - Berisi rutinitas pustaka bersama yang diperlukan oleh banyak perintah dan program di /usr/bin dan /usr/sbin, serta oleh kernel dan aplikasi lainnya untuk instalasi dan operasi yang sukses.
  - Direktori /usr/lib juga menyimpan program inisialisasi sistem dan manajemen layanan.
  - Subdirektori /usr/lib64 berisi rutinitas pustaka bersama 64-bit.

### 12. **The Variable Directory (/var)**
  - Berisi data yang sering berubah saat sistem berjalan
  - File dalam direktori ini mencakup `log`, `satatus`, `spool`, `lock`, dan `data dinamis lainnya`.
  - Contoh: `/var/log`, `/var/spool`, dan `/var/tmp`.

### 13. **The Temporary Directory (/tmp)**
  - Berisi file sementara yang dibuat oleh proses sistem dan pengguna.
  - File di `/tmp` biasanya dihapus saat sistem reboot.

### 14. **The Devices File System (/dev), Virtual**
  - Berisi file perangkat yang mewakili komponen perangkat keras dan perangkat virtual.
  - Node perangkat ini dibuat dan dihapus secara otomatis oleh layanan **udevd** sesuai kebutuhan.
  - Ada dua jenis file perangkat: file perangkat karakter (atau mentah) dan file perangkat blok.
    - **Perangkat karakter**: Diakses secara serial dengan aliran bit yang ditransfer selama komunikasi kerneldengan dan perangkat. Contoh: konsol, printer serial, mouse, keyboard, `/dev/tty` (terminal), dll.
    -  **Perangkat Blok**: Diakses secara paralel dengan data yang dipertukarkan dalam blok selama komunikasi kernel dan  perangkat. Data pada perangkat blok diakses secara acak. Contoh: `/dev/sda` (hard drive), optical drive, printer paralel, dll.

### 15. **The Procfs File System (/proc), Virtual**
  - Digunakan untuk memelihara informasi tentang status saat ini dari kernel yang berjalan.
  - Termasuk detail konfigurasi perangkat keras saat ini dan informasi status tentang CPU, memori, disk, partisi, sistem file, jaringan, proses yang berjalan, dan sebagainya.
  - Informasi ini disimpan dalam hierarki subdirektori yang berisi ribuan file pseudo dengan panjang nol.
  - File-file ini menunjuk ke data relevan yang dipelihara oleh kernel dalam memori.
  - Struktur direktori virtual ini menyediakan antarmuka yang mudah untuk berinteraksi dengan informasi yang dipelihara oleh kernel.
  - Sistem file Procfs dikelola secara dinamis oleh sistem.
  - Isi dalam `/proc` dibuat dalam memori saat sistem boot, diperbarui selama runtime, dan dihapus saat sistem dimatikan.

### 16. **The System File System (/sys), Virtual**
- Berisi informasi tentang perangkat keras, driver, dan beberapa fitur kernel.
- Informasi ini digunakan oleh kernel untuk memuat dukungan yang diperlukan untuk perangkat, membuat node perangkat di `/dev`, dan mengkonfigurasi perangkat.
- Sistem file ini dikelola secara otomatis.


---

**Source: `RHCSA® Red Hat® Enterprise Linux® 8 (UPDATED) Training and Exam Preparation Guide, EX200, Edisi Kedua, November 2020`**

`Hal: 99-105`
