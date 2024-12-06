# Analisa Logs, Metrics, dan Traces Hasura melalui Elastic
Untuk Melakukan analisa diatas, terlebih dahulu dilakukan konfigurasi antara Hasura dengan Otel Collector. Selanjutnya untuk membaca dan menganalisa dilakukan export dari Otelcol menuju Elastic

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

