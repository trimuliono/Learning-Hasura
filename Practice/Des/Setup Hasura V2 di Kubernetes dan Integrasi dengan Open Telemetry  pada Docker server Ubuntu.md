# Setup Hasura V2 di Kubernetes dengan Integrasi OpenTelemetry

## 1. Deployment Hasura V2 di Kubernetes

Langkah-langkah untuk melakukan **deployment Hasura V2 di Kubernetes** telah dijelaskan secara lengkap pada [panduan ini](https://github.com/trimuliono/Learning-Hasura/blob/main/Practice/Des/Panduan%20Koneksi%20VPN%2C%20Akses%20Rancher%2C%20dan%20Deployment%20Hasura.md).

---

## 2. Install OpenTelemetry Collector

### A. Akses Server

Sebelum kita mulai, pastikan bahwa kita menginstall **OpenTelemetry** pada server yang terpisah dari server Hasura. Anda akan mengakses server tersebut menggunakan **Windows Powershell** atau **Command Prompt**.

### B. Install Docker

Untuk menginstall **OpenTelemetry**, kita akan menggunakan **Docker**. Pastikan bahwa **Docker** sudah terinstall di server yang akan digunakan. Jika Docker belum terpasang, ikuti langkah-langkah berikut untuk menginstalnya.

#### 1. Prasyarat

Pastikan server yang digunakan menjalankan **Ubuntu** atau distribusi Linux turunannya. Panduan ini juga berlaku untuk distribusi seperti Linux Mint, namun Anda mungkin perlu menggunakan `UBUNTU_CODENAME` alih-alih `VERSION_CODENAME` ketika menambahkan repository Docker ke sumber Apt.

#### 2. Langkah-Langkah Instalasi Docker Engine

##### a. Tambahkan Repository Apt Docker

1. **Perbarui Daftar Paket dan Instal Dependensi**:
   Jalankan perintah berikut untuk memperbarui daftar paket dan menginstal dependensi yang diperlukan:
   ```bash
   sudo apt-get update
   sudo apt-get install ca-certificates curl
   ```

2. **Tambahkan GPG Key Resmi Docker**:
   Tambahkan kunci GPG Docker untuk memastikan bahwa paket yang diunduh berasal dari sumber yang sah:
   ```bash
   sudo install -m 0755 -d /etc/apt/keyrings
   sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
   sudo chmod a+r /etc/apt/keyrings/docker.asc
   ```

3. **Tambahkan Repository Docker ke Sumber Apt**:
   Jalankan perintah ini untuk menambahkan repository Docker ke daftar sumber apt:
   ```bash
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```

4. **Perbarui Daftar Paket**:
   Perbarui kembali daftar paket agar repository Docker yang baru dapat digunakan:
   ```bash
   sudo apt-get update
   ```

##### b. Instal Paket Docker

1. **Instal Docker Engine**:
   Jalankan perintah berikut untuk menginstal Docker Engine dan komponen terkait:
   ```bash
   sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
   ```

2. **Verifikasi Instalasi Docker**:
   Untuk memastikan Docker telah terinstal dengan benar, jalankan perintah berikut untuk menjalankan container uji coba `hello-world`:
   ```bash
   sudo docker run hello-world
   ```

Jika perintah ini berhasil, Anda akan melihat pesan konfirmasi bahwa Docker telah berhasil terinstal dan berjalan dengan baik.

---

### C. Verifikasi Instalasi Docker

Jika instalasi berhasil, Anda akan melihat output yang menunjukkan bahwa Docker Engine telah terinstal dengan benar dan siap digunakan. Jika Anda belum melihat pesan tersebut, pastikan Anda mengikuti setiap langkah dengan benar.

Baca referensi lengkapnya di: [Docker Installation on Ubuntu](https://docs.docker.com/engine/install/ubuntu/).

---

## 3. Install OpenTelemetry Collector

Setelah Docker terpasang, kita akan menginstal **OpenTelemetry Collector** (OTEL) untuk memonitor dan mengekspor data telemetri.

### A. Persiapan Folder dan File Konfigurasi

1. **Buat Folder untuk OpenTelemetry**  
   Buat folder bernama **OTEL** di server untuk menyimpan konfigurasi OpenTelemetry:
   ```bash
   mkdir OTEL
   ```

2. **Masuk ke Folder OTEL**  
   Arahkan terminal Anda ke folder **OTEL**:
   ```bash
   cd OTEL
   ```

3. **Buat File Konfigurasi OpenTelemetry**  
   Buat file konfigurasi untuk OpenTelemetry Collector:
   ```bash
   touch otel-collector-config.yaml
   ```

4. **Edit File Konfigurasi**  
   Gunakan editor teks (seperti `nano`) untuk mengedit file **otel-collector-config.yaml**:
   ```bash
   nano otel-collector-config.yaml
   ```

   Kemudian masukkan konfigurasi berikut untuk OpenTelemetry Collector:

   ```yaml
   receivers:
     otlp:
       protocols:
         grpc:
           endpoint: 0.0.0.0:4317
         http:
           endpoint: 0.0.0.0:4318

   processors:
     batch:

   exporters:
     debug: {}
     verbosity: detailed

   extensions:
     health_check:
     pprof:
       endpoint: 0.0.0.0:1777
     zpages:
       endpoint: 0.0.0.0:55679

   service:
     pipelines:
       traces:
         receivers: [otlp]
         processors: [batch]
         exporters: [debug, otlp]
       metrics:
         receivers: [otlp]
         processors: [batch]
         exporters: [debug, otlp]
       logs:
         receivers: [otlp]
         processors: [batch]
         exporters: [debug, otlp]
   ```

   Tekan `Ctrl + X` untuk keluar dan pilih "Yes" untuk menyimpan file.

### B. Verifikasi File Konfigurasi

Periksa apakah file konfigurasi **otel-collector-config.yaml** telah dibuat dengan benar:
```bash
ls -ll
```

### C. Jalankan OpenTelemetry Collector

1. **Unduh Docker Image untuk OpenTelemetry Collector**  
   Gunakan perintah berikut untuk mengunduh image OpenTelemetry Collector:
   ```bash
   docker pull otel/opentelemetry-collector-contrib:0.114.0
   ```

2. **Jalankan OpenTelemetry Collector**  
   Jalankan container dengan menggunakan konfigurasi yang telah dibuat:
   ```bash
   docker run -d -v $(pwd)/otel-collector-config.yaml:/root/OTEL/otel-collector-config.yaml otel/opentelemetry-collector-contrib:0.114.0
   ```

Baca dokumentasi lebih lanjut mengenai instalasi dan konfigurasi Collector di [OpenTelemetry Collector Installation](https://opentelemetry.io/docs/collector/installation/) dan [Collector Configuration](https://opentelemetry.io/docs/collector/configuration/).

---

## 4. Install OpenTelemetry Collector (otelcol)

Jika Anda ingin menginstal OpenTelemetry Collector sebagai service di server, lakukan langkah-langkah berikut:

1. **Cek apakah `otelcol` sudah terpasang**:
   ```bash
   which otelcol
   ```

   Jika perintah di atas tidak memberikan hasil, berarti **otelcol** belum terpasang.

2. **Instal OpenTelemetry Collector**  
   Jalankan perintah berikut untuk mengunduh dan menginstal **otelcol**:
   ```bash
   curl -sL https://github.com/open-telemetry/opentelemetry-collector-releases/releases/download/v0.81.0/otelcol_0.81.0_linux_amd64.deb -o otelcol.deb
   sudo dpkg -i otelcol.deb
   ```

3. **Buat file konfigurasi untuk `otelcol`**  
   Buat file service untuk OpenTelemetry Collector agar bisa dijalankan sebagai service di systemd:
   ```bash
   sudo nano /etc/systemd/system/otelcol.service
   ```

   Masukkan konfigurasi berikut:
   ```ini
   [Unit]
   Description=OpenTelemetry Collector
   After=network.target

   [Service]
   Type=simple
   ExecStart=/usr/local/bin/otelcol --config=/etc/otelcol-config.yaml
   Restart=always
   RestartSec=10
   User=otel
   Group=otel

   [Install]
   WantedBy=multi-user.target
   ```

4. **Lihat Log `otelcol`**  
   Untuk memeriksa apakah **otelcol** berjalan dengan baik, gunakan perintah berikut untuk melihat log:
   ```bash
   journalctl -u otelcol -f
   ```

---

## 5. Integrasi OpenTelemetry dengan Hasura pada Rancher

1. **Buka Hasura di Rancher**  
   Masuk ke antarmuka Rancher dan pilih proyek Hasura Anda.

2. **Pilih Pengaturan**  
   Klik pada **Settings** dan pilih opsi **OpenTelemetry Exporter**.

   ![image](https://github.com/user-attachments/assets/8163f19c-0a65-41f0-8eaf-f1551906986d)

3. **Masukkan Endpoint OpenTelemetry**  
   Di

 kolom konfigurasi **OpenTelemetry Exporter**, masukkan endpoint yang sesuai, dalam hal ini adalah port `4318` yang kita tentukan dalam file konfigurasi OTEL.

   ![image](https://github.com/user-attachments/assets/f0becc6c-669f-46bb-b45a-2cee508e7b13)

4. **Lakukan Pengujian**  
   Setelah konfigurasi selesai, lakukan pengujian dengan menjalankan query Hasura yang dapat memicu telemetry, misalnya query terhadap tabel **todo**.

   ![image](https://github.com/user-attachments/assets/47d8e418-403c-42a8-a1ad-e83a5bef489f)
```
