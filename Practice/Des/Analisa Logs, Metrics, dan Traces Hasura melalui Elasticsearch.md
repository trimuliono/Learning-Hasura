# Analisa Logs, Metrics, dan Traces Hasura melalui Elasticsearch
Untuk Melakukan analisa diatas, terlebih dahulu dilakukan konfigurasi antara Hasura dengan Otel Collector. Selanjutnya untuk membaca dan menganalisa dilakukan export dari Otelcol menuju Elastic

## Mengakses Graphical User Interface (GUI) Elastic
Untuk mengakse GUI Elastic dilakukan dengan memasukkan `Username` dan `Password` pada login form elastic.
![image](https://github.com/user-attachments/assets/accb4ea6-466b-437d-bd82-fb05f261fdf1)

Setelah berhasil masuk, ketik `data view` pada `Search bar` untuk mengakses `Kibana - Data 
views`
![image](https://github.com/user-attachments/assets/9de481db-7ccf-4b23-aaac-06759b9b6478)



## Melakukan filter search

### host.hostname
```KQL
host.hostname :"hasura-tri-xxxx-xxxx:port"
```

### status
```KQL
status :"miss" 
```
### host.hostname join status
```KQL
host.hostname :"hasura-tri-xxxx-xxxx:port" and status :"miss" 
```

