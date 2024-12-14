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

### 1. **Menampilkan File dan Direktori (ls)**
Perintah `ls` digunakan untuk menampilkan daftar file dan direktori. Berikut beberapa opsi umum:

| Opsi | Deskripsi |
|------|-----------|
| `-a` | Menampilkan file/direktori tersembunyi. |
| `-l` | Menampilkan daftar panjang dengan informasi detail. |
| `-ld` | Menampilkan detail direktori tanpa isi. |
| `-lh` | Menampilkan ukuran file dalam format ramah manusia. |
| `-lt` | Menyortir berdasarkan tanggal dan waktu (terbaru di atas). |
| `-ltr` | Menyortir berdasarkan tanggal dan waktu (terlama di atas). |
| `-R` | Menampilkan isi direktori dan subdirektori secara rekursif. |

**Contoh Penggunaan:**  
- Melihat semua file dan folder:  
   ```bash
   ls
   ```  
- Melihat file secara **detail**:  
   ```bash
   ls -l
   ```  
- Melihat file termasuk yang **tersembunyi** (dimulai dengan titik `.`):  
   ```bash
   ls -a
   ```  
- Gabungan semua opsi: melihat file tersembunyi dan detailnya:  
   ```bash
   ls -la
   ```  
- Melihat file dalam **direktori tertentu**:  
   ```bash
   ls /home/user/Documents
   ```  

---

### **2. Melihat Lokasi Saat Ini: `pwd` (Print Working Directory)**  
Perintah `pwd` digunakan untuk melihat lokasi atau direktori tempat kita berada saat ini.  

**Sintaks:**  
```bash
pwd
```

---

### **3. Pindah Direktori: `cd` (Change Directory)**  
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

### **4. Melihat Manual Perintah: `man`**  
Perintah `man` digunakan untuk menampilkan **manual** atau panduan dari suatu perintah. Ini membantu kita memahami cara menggunakan perintah dan opsi-opsinya.  

**Sintaks:**  
```bash
man [nama_perintah]
```

**Contoh Penggunaan:**  
- Melihat manual perintah `ls`:  
   ```bash
   man ls
   ```  
- Melihat manual perintah `cd`:  
   ```bash
   man cd
   ```  

---

### 5. **Identifikasi File Perangkat Terminal (tty)**
Perintah `tty` digunakan untuk mengidentifikasi terminal aktif saat ini.

**Contoh:**

```bash
root@server:/# tty
/dev/pts/0
root@server:/#
```
Output menunjukkan file perangkat terminal aktif, `/dev/pts/0`.

---

### 6. **Melihat Uptime dan Beban CPU (uptime)**
Perintah `uptime` menampilkan waktu sistem, durasi aktif, jumlah pengguna, dan rata-rata beban CPU.

**Contoh:**

```bash
root@server:/# uptime
04:08:13 up 35 days, 23:06, 75 users,  load average: 1.77, 2.15, 4.90
root@server:/#
```

Output:
- `04:08:13` Waktu sistem.
- `up 35 days, 23:06` Durasi aktif.
- `75 users` Jumlah pengguna login.
- `1.77, 2.15, 4.90` Rata-rata beban CPU dalam 1, 5, dan 15 menit terakhir.

---

### 7. **Membersihkan Layar Terminal (clear)**
Perintah `clear` membersihkan layar terminal.

**Contoh:**

```bash
root@server:/# clear
root@server:/#
```

**Alternatif:** Gunakan shortcut `Ctrl+l`.

---

### 8. **Menentukan Jalur Perintah (which, whereis, type)**
Untuk mengetahui jalur absolut suatu perintah:

**Contoh:**

```bash
root@server:/# which ls
/usr/bin/ls
root@server:/# whereis ls
ls: /usr/bin/ls
root@server:/# type ls
ls is aliased to `ls --color=auto'
root@server:/#
```

---

### 9. **Melihat Informasi Sistem (uname)**
Perintah `uname` digunakan untuk mendapatkan informasi tentang kernel Linux, sedangkan `uname -a` memberikan rincian lengkap sistem seperti versi kernel, hostname, arsitektur, dan lainnya. Ini sering digunakan untuk memeriksa versi sistem operasi atau mendebug masalah kompatibilitas perangkat lunak.

**Contoh:**

```bash
root@server:/# uname 
Linux
root@server:/# uname -a 
Linux server6.8.0-48-generic #48-Ubuntu SMP PREEMPT_DYNAMIC Fri Sep 27 14:04:52 UTC 2024 x86_64 x86_64 x86_64 GNU/Linux 
root@server:/# 
```
  



**Informasi yang diberikan:**
- **`uname`**: Perintah ini digunakan untuk menampilkan **nama sistem operasi**.
- **Output**: `Linux` menunjukkan bahwa sistem operasi yang digunakan adalah Linux.

Perintah `uname -a` menampilkan **semua informasi terkait sistem** dalam satu baris. Berikut adalah rincian setiap bagian dari output:

- **`Linux`**: Nama sistem operasi (OS) yang sedang berjalan.
- **`server`**: Nama host atau hostname dari mesin/server.
- **`6.8.0-48-generic`**: Versi kernel Linux yang digunakan.
    - `6.8.0` → Versi utama kernel.
    - `48-generic` → Ini adalah versi kernel yang dikompilasi untuk distribusi umum (generic).
- **`#48-Ubuntu`**: 
    - `#48` → Ini adalah build atau revisi kernel ke-48.
    - `Ubuntu` → Distribusi Linux yang digunakan adalah Ubuntu.
- **`SMP`**: Simmetric Multi-Processing.
    - Kernel ini mendukung sistem multi-core atau multi-CPU.
- **`PREEMPT_DYNAMIC`**:
    - Kernel mendukung preemption (interupsi proses berjalan) yang dinamis.
    - Berguna untuk meningkatkan performa sistem real-time.
- **`Fri Sep 27 14:04:52 UTC 2024`**:
    - Tanggal dan waktu saat kernel ini dikompilasi (UTC - Universal Coordinated Time).
- **`x86_64`**:
    - Ini adalah **arsitektur prosesor** yang digunakan.
    - `x86_64` menunjukkan bahwa sistem berjalan pada prosesor 64-bit.
- **`GNU/Linux`**:
    - Ini menunjukkan sistem berbasis kernel Linux dan menggunakan perangkat lunak GNU.

**Penjelasan Ringkas Perintah `uname` dan `uname -a`**

| Perintah       | Keterangan                                        |
|----------------|---------------------------------------------------|
| `uname`       | Menampilkan nama sistem operasi (misalnya, Linux). |
| `uname -a`    | Menampilkan semua informasi sistem, termasuk:     |
|               | - Nama OS                                          |
|               | - Hostname                                        |
|               | - Versi kernel                                    |
|               | - Tanggal kompilasi kernel                        |
|               | - Arsitektur prosesor                             |

---

### 9. **Melihat Spesifikasi CPU (lscpu)**
Perintah `lscpu` menampilkan informasi arsitektur CPU, mode operasi, vendor, model, kecepatan, cache, dan dukungan virtualisasi.

**Contoh:**

```bash
root@server:/# lscpu
Architecture:             x86_64
  CPU op-mode(s):         32-bit, 64-bit
  Address sizes:          45 bits physical, 48 bits virtual
  Byte Order:             Little Endian
CPU(s):                   4
  On-line CPU(s) list:    0-3
Vendor ID:                GenuineIntel
  BIOS Vendor ID:         GenuineIntel
  Model name:             Intel(R) Xeon(R) Gold 6240 CPU @ 2.60GHz
    BIOS Model name:      Intel(R) Xeon(R) Gold 6240 CPU @ 2.60GHz  CPU @ 2.4GHz
    BIOS CPU family:      2
    CPU family:           6
    Model:                85
    Thread(s) per core:   1
    Core(s) per socket:   4
    Socket(s):            1
    Stepping:             7
    BogoMIPS:             5187.81
    Flags:                fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss ht syscall nx pdpe1gb rdtscp lm constant_tsc arch_perfmon nopl xt
                          opology tsc_reliable nonstop_tsc cpuid tsc_known_freq pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand
                           hypervisor lahf_lm abm 3dnowprefetch ssbd ibrs ibpb stibp ibrs_enhanced fsgsbase tsc_adjust bmi1 avx2 smep bmi2 invpcid avx512f avx512dq rdseed adx smap clflushopt c
                          lwb avx512cd avx512bw avx512vl xsaveopt xsavec xgetbv1 xsaves arat pku ospke avx512_vnni md_clear flush_l1d arch_capabilities
Virtualization features:
  Hypervisor vendor:      VMware
  Virtualization type:    full
Caches (sum of all):
  L1d:                    128 KiB (4 instances)
  L1i:                    128 KiB (4 instances)
  L2:                     4 MiB (4 instances)
  L3:                     24.8 MiB (1 instance)
NUMA:
  NUMA node(s):           1
  NUMA node0 CPU(s):      0-3
Vulnerabilities:
  Gather data sampling:   Unknown: Dependent on hypervisor status
  Itlb multihit:          KVM: Mitigation: VMX unsupported
  L1tf:                   Not affected
  Mds:                    Not affected
  Meltdown:               Not affected
  Mmio stale data:        Vulnerable: Clear CPU buffers attempted, no microcode; SMT Host state unknown
  Reg file data sampling: Not affected
  Retbleed:               Mitigation; Enhanced IBRS
  Spec rstack overflow:   Not affected
  Spec store bypass:      Mitigation; Speculative Store Bypass disabled via prctl
  Spectre v1:             Mitigation; usercopy/swapgs barriers and __user pointer sanitization
  Spectre v2:             Mitigation; Enhanced / Automatic IBRS; IBPB conditional; RSB filling; PBRSB-eIBRS SW sequence; BHI SW loop, KVM SW loop
  Srbds:                  Not affected
  Tsx async abort:        Not affected
root@server:/#
```
**Output mencakup:**

#### **Informasi Umum**
1. **Architecture**: 
   - **`x86_64`** → Sistem menggunakan arsitektur 64-bit, mendukung mode 32-bit dan 64-bit.

2. **CPU op-mode(s)**: 
   - Mendukung operasi 32-bit dan 64-bit.

3. **Address sizes**: 
   - Mendukung 45-bit untuk alamat fisik dan 48-bit untuk alamat virtual.

4. **Byte Order**: 
   - **`Little Endian`** → Urutan penyimpanan data dalam memori dari byte terkecil ke byte terbesar.


#### **CPU dan Konfigurasi**
5. **CPU(s)**: 
   - Jumlah total CPU virtual/logis adalah **4**.

6. **On-line CPU(s) list**: 
   - CPU yang aktif: **0-3**.

7. **Vendor ID**: 
   - **`GenuineIntel`** → CPU berasal dari Intel.

8. **Model name**: 
   - **Intel(R) Xeon(R) Gold 6240 CPU @ 2.60GHz** → Model prosesor yang digunakan.

9. **Core(s) per socket**: 
   - Ada **4 core** per soket.

10. **Thread(s) per core**: 
    - Setiap core hanya memiliki **1 thread**.

11. **Socket(s)**: 
    - Jumlah soket adalah **1**.

12. **Stepping, Model, CPU family**: 
    - Detil spesifik prosesor: Stepping 7, Model 85, CPU Family 6.

13. **BogoMIPS**: 
    - Kecepatan CPU virtual: **5187.81 BogoMIPS** (indikasi relatif dari performa CPU).


#### **Fitur CPU**
14. **Flags**: 
    - Menampilkan daftar fitur yang didukung CPU, seperti:
      - **`sse4_1, sse4_2, avx, avx512f`** → Mendukung instruksi SIMD modern.
      - **`hypervisor`** → Berjalan di lingkungan virtualisasi (VMware).
      - **`aes`** → Mendukung akselerasi enkripsi AES.
      - **`bmi1, bmi2`** → Instruksi manipulasi bit untuk performa tinggi.
      - **`fma`** → Mendukung operasi matematika floating-point cepat.


#### **Fitur Virtualisasi**
15. **Hypervisor vendor**: 
    - Sistem berjalan di **VMware** hypervisor.

16. **Virtualization type**: 
    - Tipe virtualisasi adalah **full**.

---

#### **Cache CPU**
17. **L1d, L1i**: 
    - Cache Level 1 Data dan Instruction masing-masing: **128 KiB** (4 instance).
18. **L2**: 
    - Cache Level 2: **4 MiB** (4 instance).
19. **L3**: 
    - Cache Level 3: **24.8 MiB** (1 instance).


#### **NUMA**
20. **NUMA node(s)**: 
    - Sistem memiliki **1 node NUMA**, dengan CPU pada node tersebut: **0-3**.


#### **Kerentanan dan Mitigasi**
21. **Meltdown, Spectre, Retbleed**: 
    - Sistem **tidak terpengaruh** atau **dimitigasi** dengan fitur-fitur keamanan:
      - **Spectre v1, v2** → Dilindungi dengan mitigasi seperti Enhanced IBRS.
      - **Meltdown** → Tidak terpengaruh.
22. **Mmio stale data**:
    - Rentan terhadap beberapa kerentanan, tetapi mitigasi telah dicoba.



---

**Source: `RHCSA® Red Hat® Enterprise Linux® 8 (UPDATED) Training and Exam Preparation Guide, EX200, Edisi Kedua, November 2020`**

`Hal: 104-116`
