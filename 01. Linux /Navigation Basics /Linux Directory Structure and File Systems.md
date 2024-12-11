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

1. **Root File System Directory (`/`)**, Disk-Based
  - Direktori tingkat atas dalam hierarki sistem file Linux.
  - Semua direktori dan file lainnya berada di bawah direktori ini.

2. **/etc**
  - Berisi file konfigurasi sistem dan skrip shell yang digunakan untuk booting dan inisialisasi sistem.
  - Contoh: `passwd`, `fstab`, dan `hosts`.




---

**Source: `RHCSA® Red Hat® Enterprise Linux® 8 (UPDATED) Training and Exam Preparation Guide, EX200, Edisi Kedua, November 2020`**

`Hal: 99-105`
