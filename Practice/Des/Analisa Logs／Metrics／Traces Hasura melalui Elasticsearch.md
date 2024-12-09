# Analisa Logs/Metrics/Traces Hasura melalui Elasticsearch
Untuk Melakukan analisa diatas, terlebih dahulu dilakukan konfigurasi antara Hasura dengan Otel Collector. Selanjutnya untuk membaca dan menganalisa dilakukan export dari Otelcol menuju Elastic

## Mengakses Graphical User Interface (GUI) Elastic
Untuk mengakse GUI Elastic dilakukan dengan memasukkan `Username` dan `Password` pada login form elastic.
![image](https://github.com/user-attachments/assets/accb4ea6-466b-437d-bd82-fb05f261fdf1)

Setelah berhasil masuk, klik `Burger bar` di pojok kiri atas, kemudian klik menu `Discover` untuk mengakses `Logs/metrics/traces`
![image](https://github.com/user-attachments/assets/3a122f1b-2bd5-4282-b5ed-746f2bcef246)

Setelah berada pada menu `discover` klik dropdown di pojok kiri atas pada `data view` dan pilih `metrics` untuk melihat data metrics
![image](https://github.com/user-attachments/assets/196143b7-d589-4d50-8a9a-3c795141f476)


## Melakukan filter search
*Kibana Query Language (KQL)*, yaitu bahasa kueri yang digunakan di Kibana untuk melakukan pencarian data dan memfilter hasil pada indeks di Elasticsearch. KQL memiliki fitur `auto complitation` sehingga user cukup mengetikkan beberapa kata kunci awal dan sistem akan menampilkan saran complitation nya.

### host.hostname
untuk mencari metrics berdasrkan hostname, user cukup mengetikan `host.name :` dan sistem akan menampilkan saran completition
![image](https://github.com/user-attachments/assets/1cc6329a-e365-444a-99c9-9d0d21d5a727)
```KQL
host.hostname :"hasura-tri-74c8bbcb78-265mp:8080"
```
![image](https://github.com/user-attachments/assets/10d326d6-0351-44c0-b7a6-d97634a68756)

### status
```KQL
status :"miss" 
```
### host.hostname join status
```KQL
host.hostname :"hasura-tri-xxxx-xxxx:port" and status :"miss" 
```

