# Perintah Dasar Sistem Linux

Navigasi dalam **Linux** berarti bergerak di antara folder (direktori) dan melihat file yang ada di komputer. Ada beberapa perintah dasar yang digunakan untuk **pindah direktori**, melihat **isi folder**, dan mengetahui **lokasi saat ini**. Perintah-perintah ini membantu kita menemukan dan mengatur file dengan mudah.  

---

## Understanding the Command Mechanics
**Sintaks dasar perintah Linux adalah:**
 
```bash
command opsi argumen
```

- **Option (opsional):** Mengubah perilaku perintah. 
  - Format pendek: diawali dengan `-` (contoh: `-l`, `-a`).
  - Format panjang: diawali dengan `--` (contoh: `--all`).
- **Argument (opsional/mandatory):** Target untuk perintah tersebut.

Contoh struktur perintah:

| Syntax | Deskripsi |
|------|-----------|
| `ls` | Perintah  tanpa opsi, argumen default adalah direktori saat ini. |
| `ls -l` | Perintah Satu opsi, argumen default adalah direktori saat ini. |
| `ls -al` | Perintah Dua opsi, tidak ada argumen eksplisit; argumen defaultnya adalah nama direktori saat ini. |
| `ls -all` | Perintah Satu opsi, tidak ada argumen eksplisit; argumen defaultnya adalah nama direktori saat ini. |
| `ls -l directory_name` | Perintah Satu opsi dan satu argumen eksplisit. |



---

### **1. Pindah Direktori: `cd` (Change Directory)**  
Perintah `cd` digunakan untuk pindah ke direktori atau folder lain.  
**Sintaks:**  
```bash
cd /path/ke/direktori
```

**Contoh Penggunaan:**  
- Pindah ke folder tertentu:  
   ```bash
   cd /home/user/Documents
   ```  
- Pindah ke direktori **root**:  
   ```bash
   cd /
   ```  
- Pindah ke direktori **home** pengguna:  
   ```bash
   cd ~
   ```  
- Pindah ke direktori sebelumnya:  
   ```bash
   cd -
   ```  
- Pindah ke direktori induk (satu level ke atas):  
   ```bash
   cd ..
   ```  

---





---

**Source: `RHCSA® Red Hat® Enterprise Linux® 8 (UPDATED) Training and Exam Preparation Guide, EX200, Edisi Kedua, November 2020`**

`Hal: 104-116`
