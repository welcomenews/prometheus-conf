
### Выставить временной интервал в 1 мин.
rate(prometheus_http_requests_total[1m]) 

node_cpu_seconds_total{mode="iowait"}

### загрузка проца в процентах (floor округляет до целого значения)
floor(100 - (avg by (instance) (rate (node_cpu_seconds_total{mode="idle"}[1m])) * 100))

### доступно места на жёстком диске в директории /  в MB
node_filesystem_avail_bytes{mountpoint="/", device!="tmpfs"} / 1024 / 1024

### загрузка системы за последние 15 минут
node_load15



### Правила.
https://awesome-prometheus-alerts.grep.to/rules.html
