# Monitoring & observability

## Overview
Tugas kali ini yaitu membuat koneksi observability pada hasura dengan Open Telemetry

### 1. Go to the Settings tab (⚙) in the console 
click on OpenTelemetry Exporter. After adding appropriate values to the parameters, click Update and then toggle the Status button to enable the integration.

![image](https://github.com/user-attachments/assets/122151c5-a783-4b29-b18d-e16f023f0e36)

### Cek Log Open Telemetry Collector
- Konek ke server Open Telemetry
- jalankan command:
  ```bash
  journalctl -u otelcol -f
  ```
- jalankan query di hasura console
- jalankan command `Ctrl + C` di server

Berikut contoh tampilan tangkapan logs Open Telemetry:
![image](https://github.com/user-attachments/assets/40356f6b-5565-46f4-8ee9-af79bbe99e45)

