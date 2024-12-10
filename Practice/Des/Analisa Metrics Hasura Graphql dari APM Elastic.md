# Analisa Metrics Hasura Graphql dari APM Elastic
Analisa dilakukan dengan melihat data pada **`apm elastic`** setelah dilakukan query graphql hasura
![image](https://github.com/user-attachments/assets/ca1ca11c-8e15-43fe-996d-f3fce42fa933)

## Throughput dan Transactions
**APM Elastic** menyediakan observabilitas terhadap performa aplikasi. Berikut penjelasan mengenai Throughput dan Transactions yang terlihat di dashboard APM:

**1. Throughput**
    - **Definisi**: Throughput mengukur **jumlah transaksi atau request** yang diproses oleh aplikasi dalam satuan waktu tertentu.
    - **Satuan**: Biasanya dalam **transactions per minute (tpm).**
    - **Arti**: 
      - Semakin tinggi throughput, semakin banyak request yang diproses oleh aplikasi.
      - Throughput mencerminkan load atau beban kerja pada aplikasi.
    - **Grafik**: Menunjukkan jumlah transaksi per menit dalam rentang waktu tertentu.
    
![image](https://github.com/user-attachments/assets/4e2bb3ed-c9fe-4823-ae30-8f4ab0f008c4)

![image](https://github.com/user-attachments/assets/32515e0f-2f7e-4537-ada8-7152a30d44a8)

![image](https://github.com/user-attachments/assets/ee69c138-7858-4c39-99b9-5f67de8626ed)

![image](https://github.com/user-attachments/assets/0d6610b8-5783-47c8-9eec-30848e2ca835)

## Metadata

![image](https://github.com/user-attachments/assets/42514182-12fd-41f4-a1dc-22580c99fd8b)

![image](https://github.com/user-attachments/assets/cf160cd0-f7e5-4f12-886b-b0c2709c1e55)

![image](https://github.com/user-attachments/assets/a4d31bf1-d42f-45b2-a19b-71f72b8841ad)

![image](https://github.com/user-attachments/assets/36ff3925-025c-429d-8ca4-3e3eb988d88e)

## Timeline **/v1/graphql**


View transaction in Discover
![image](https://github.com/user-attachments/assets/994bfb48-67ed-40f6-8af9-170f9071b825)

```json
{
  "_index": "apm-7.17.18-transaction-000001",
  "_id": "u2l3r5MB2LTZdF1KamMS",
  "_version": 1,
  "_source": {
    "observer": {
      "hostname": "worker1.k8s.alldataint.com",
      "id": "4fa9447e-2492-4e9b-af43-0977fa67cb28",
      "type": "apm-server",
      "ephemeral_id": "f1168f81-ff63-485a-a3de-7bad197ee4f4",
      "version": "7.17.18",
      "version_major": 7
    },
    "agent": {
      "name": "otlp",
      "version": "unknown"
    },
    "trace": {
      "id": "fe75ad67ea3f85dd40b48cf819cdbaee"
    },
    "@timestamp": "2024-12-10T07:22:49.236Z",
    "ecs": {
      "version": "1.12.0"
    },
    "service": {
      "framework": {
        "name": "hasura",
        "version": "v2.42.0"
      },
      "name": "hasura",
      "language": {
        "name": "unknown"
      }
    },
    "event": {
      "ingested": "2024-12-10T07:27:39.026596459Z",
      "outcome": "success"
    },
    "processor": {
      "name": "transaction",
      "event": "transaction"
    },
    "transaction": {
      "duration": {
        "us": 435
      },
      "result": "Success",
      "name": "/v1/graphql",
      "id": "540bd2d697c0aa8a",
      "type": "custom",
      "sampled": true
    },
    "labels": {
      "session_variables": "{\"x-hasura-role\":\"admin\"}",
      "enduser_role": "admin",
      "graphql_operation_name": "TrigetUser",
      "request_id": "00866697-d793-42c1-a693-df18a8c34000",
      "http_response_content_length": "165"
    },
    "timestamp": {
      "us": 1733815369236887
    }
  },
  "fields": {
    "transaction.name.text": [
      "/v1/graphql"
    ],
    "service.framework.version": [
      "v2.42.0"
    ],
    "labels.request_id": [
      "00866697-d793-42c1-a693-df18a8c34000"
    ],
    "service.language.name": [
      "unknown"
    ],
    "transaction.result": [
      "Success"
    ],
    "transaction.sampled": [
      true
    ],
    "transaction.id": [
      "540bd2d697c0aa8a"
    ],
    "trace.id": [
      "fe75ad67ea3f85dd40b48cf819cdbaee"
    ],
    "processor.event": [
      "transaction"
    ],
    "agent.name": [
      "otlp"
    ],
    "event.outcome": [
      "success"
    ],
    "service.name": [
      "hasura"
    ],
    "service.framework.name": [
      "hasura"
    ],
    "processor.name": [
      "transaction"
    ],
    "transaction.duration.us": [
      435
    ],
    "observer.version_major": [
      7
    ],
    "observer.hostname": [
      "worker1.k8s.alldataint.com"
    ],
    "labels.session_variables": [
      "{\"x-hasura-role\":\"admin\"}"
    ],
    "transaction.type": [
      "custom"
    ],
    "event.ingested": [
      "2024-12-10T07:27:39.026Z"
    ],
    "observer.id": [
      "4fa9447e-2492-4e9b-af43-0977fa67cb28"
    ],
    "timestamp.us": [
      1733815369236887
    ],
    "@timestamp": [
      "2024-12-10T07:22:49.236Z"
    ],
    "labels.graphql_operation_name": [
      "TrigetUser"
    ],
    "labels.http_response_content_length": [
      "165"
    ],
    "observer.ephemeral_id": [
      "f1168f81-ff63-485a-a3de-7bad197ee4f4"
    ],
    "ecs.version": [
      "1.12.0"
    ],
    "observer.type": [
      "apm-server"
    ],
    "observer.version": [
      "7.17.18"
    ],
    "agent.version": [
      "unknown"
    ],
    "transaction.name": [
      "/v1/graphql"
    ],
    "labels.enduser_role": [
      "admin"
    ]
  }
}
```
