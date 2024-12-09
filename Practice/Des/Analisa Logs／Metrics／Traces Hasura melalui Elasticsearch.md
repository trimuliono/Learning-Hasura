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

### host.hostname join operation.name join response_status
```KQL
host.name : "hasura-tri-74c8bbcb78-265mp:8080"  and response_status : "success" and operation_name : "TrigetUser" 
```
![image](https://github.com/user-attachments/assets/a765c9b6-7865-49a8-9172-8f273ceffd9f)


## Analisa Data Metrics
Pertama kita lakukan query graphql agar data metrics baru dapat dibuat dan dilihat
```graphql
query TrigetUser{
  Users {
    id
    username
    email
  }
}
```
untuk memudahka pencarian langsung kita gunakan filter search join disertakan `operation.name`
```KQL
host.name : "hasura-tri-74c8bbcb78-265mp:8080"  and operation_name : "TrigetUser"
```
![image](https://github.com/user-attachments/assets/3f7198d0-245e-4121-9a57-c5c6b0345cd7)

```json
{
  "_index": ".ds-metrics-generic-default-2024.12.06-000001",
  "_id": "s66fqpMBPHAcfhWRWhsI",
  "_version": 1,
  "_source": {
    "@timestamp": "2024-12-09T08:48:15.864314850Z",
    "data_stream": {
      "dataset": "generic",
      "namespace": "default",
      "type": "metrics"
    },
    "hasura_graphql_requests_total": 2,
    "host": {
      "hostname": "hasura-tri-74c8bbcb78-265mp:8080",
      "name": "hasura-tri-74c8bbcb78-265mp:8080"
    },
    "operation_name": "TrigetUser",
    "operation_type": "query",
    "parameterized_query_hash": "ee02ea2d91f16dbf0d6e094072abac4fcf487782",
    "response_status": "success",
    "service": {
      "name": "hasura"
    }
  },
  "fields": {
    "operation_name": [
      "TrigetUser"
    ],
    "parameterized_query_hash": [
      "ee02ea2d91f16dbf0d6e094072abac4fcf487782"
    ],
    "@timestamp": [
      "2024-12-09T08:48:15.864Z"
    ],
    "operation_type": [
      "query"
    ],
    "response_status": [
      "success"
    ],
    "service.name": [
      "hasura"
    ],
    "data_stream.namespace": [
      "default"
    ],
    "data_stream.dataset": [
      "generic"
    ],
    "host.hostname": [
      "hasura-tri-74c8bbcb78-265mp:8080"
    ],
    "host.name": [
      "hasura-tri-74c8bbcb78-265mp:8080"
    ],
    "data_stream.type": [
      "metrics"
    ],
    "hasura_graphql_requests_total": [
      2
    ]
  }
}
```
### Metadata Utama
- **`_index`**:  
  Nilai ini menunjukkan indeks data stream di Elasticsearch.  
  **Contoh**: `.ds-metrics-generic-default-2024.12.06-000001`  
  - `metrics-generic`: Dataset yang digunakan.  
  - `default`: Namespace default.  
  - `2024.12.06`: Tanggal pembuatan indeks pertama.  

- **`_id`**:  
  ID unik dokumen yang di-generate oleh Elasticsearch.  
  **Contoh**: `s66fqpMBPHAcfhWRWhsI`  

- **`_version`**:  
  Versi dokumen dalam Elasticsearch.  
  **Contoh**: `1`  

---

### **@timestamp**  
Waktu ketika data dikumpulkan dalam format ISO8601.  
**Contoh**: `2024-12-09T08:48:15.864314850Z`  
- Digunakan untuk analisis time series.

---

### **Data Stream**  
Menjelaskan struktur data stream.  
- **`dataset`**: Nama dataset.  
  **Contoh**: `"generic"`  
- **`namespace`**: Namespace yang digunakan.  
  **Contoh**: `"default"`  
- **`type`**: Jenis data stream (metrics, logs, dll).  
  **Contoh**: `"metrics"`

---

### **hasura_graphql_requests_total**  
Jumlah total permintaan GraphQL yang diterima.  
**Contoh**: `2`  
- Digunakan untuk mengukur tingkat aktivitas query GraphQL.

---

### **Host**  
Informasi tentang host atau node yang menjalankan layanan.  
- **`hostname`**: Nama lengkap host termasuk port.  
  **Contoh**: `"hasura-tri-74c8bbcb78-265mp:8080"`  
- **`name`**: Nama host sama seperti `hostname`.  
  **Contoh**: `"hasura-tri-74c8bbcb78-265mp:8080"`

---

### **operation_name**  
Nama operasi GraphQL yang dijalankan.  
**Contoh**: `"TrigetUser"`  
- Berguna untuk mengidentifikasi jenis query atau mutasi yang dipanggil.

---

### **operation_type**  
Jenis operasi GraphQL: `query`, `mutation`, atau `subscription`.  
**Contoh**: `"query"`  

---

### **parameterized_query_hash**  
Hash dari query GraphQL untuk query parameterized.  
**Contoh**: `"ee02ea2d91f16dbf0d6e094072abac4fcf487782"`  
- Memungkinkan penyamaan query yang identik dalam bentuk hash.

---

### **response_status**  
Status respons dari query Hasura.  
**Contoh**: `"success"`  
- Bisa memiliki nilai: `success`, `error`, atau `timeout`.

---

### **Service**  
Informasi layanan yang menghasilkan data metrics.  
- **`name`**: Nama layanan.  
  **Contoh**: `"hasura"`

---

### **Fields**  
Bagian ini mengulangi semua field dalam format array untuk keperluan indexing di Elasticsearch.  
Contoh:  
- **`operation_name`**: `["TrigetUser"]`  
- **`response_status`**: `["success"]`  
- **`host.hostname`**: `["hasura-tri-74c8bbcb78-265mp:8080"]`  
- **`hasura_graphql_requests_total`**: `[2]`  

Field ini berguna saat melakukan pencarian atau query kompleks di Kibana.

---

### **Kesimpulan**  
Metrics ini memberikan wawasan penting terkait:  
1. **Jumlah Query** (`hasura_graphql_requests_total`)  
2. **Waktu Query** (`@timestamp`)  
3. **Tipe Operasi** (`operation_type`)  
4. **Nama Operasi** (`operation_name`)  
5. **Status Respons** (`response_status`)  
6. **Identitas Host** (`host.hostname`)  
7. **Efisiensi Query** dengan Hash (`parameterized_query_hash`)  

