```
## Выставить временной интервал в 1 мин.
rate(prometheus_http_requests_total[1m]) 

node_cpu_seconds_total{mode="iowait"}

## загрузка проца в процентах (floor округляет до целого значения)
floor(100 - (avg by (instance) (rate (node_cpu_seconds_total{mode="idle"}[1m])) * 100))

## доступно места на жёстком диске в директории /  в MB
node_filesystem_avail_bytes{mountpoint="/", device!="tmpfs"} / 1024 / 1024

## загрузка системы за последние 15 минут
node_load15

## Disk read and write
Graph old
irate(windows_logical_disk_read_bytes_total{job=~"$job",instance=~"$instance"}[5m])   Legend: read {{volume}}
irate(windows_logical_disk_write_bytes_total{job=~"$job",instance=~"$instance"}[5m])  Legend: write {{volume}}


## 
Disk IO 
Graph old
irate(windows_logical_disk_reads_total{job=~"$job",instance=~"$instance"}[5m])  Legend: read {{volume}}
irate(windows_logical_disk_writes_total{job=~"$job",instance=~"$instance"}[5m]) Legend: write {{volume}}

## Network usage 
Graph old
(irate(windows_net_bytes_total{job=~"$job",instance=~"$instance",nic!~'isatap.*|VPN.*'}[5m]) * 8 / windows_net_current_bandwidth{job=~"$job",instance=~"$instance",nic!~'isatap.*|VPN.*'}) * 100          Legend: {{nic}}

## Free disk space
Graph old
windows_logical_disk_free_bytes{job=~"$job",instance=~"$instance"}   Legend: Remaining space {{volume}}
windows_logical_disk_size_bytes{job=~"$job",instance=~"$instance"}   Legend: Total space {{volume}}

## Memory Details
Graph old
windows_cs_physical_memory_bytes{job=~"$job",instance=~"$instance"}  Legend: Total physical memory
windows_os_physical_memory_free_bytes{job=~"$job",instance=~"$instance"}  Legend: Remaining physical memory
windows_os_virtual_memory_bytes{job=~"$job",instance=~"$instance"}    Legend: Virtual memory
windows_os_virtual_memory_free_bytes{job=~"$job",instance=~"$instance"}  Legend: Free virtual memory

## Network Details
Graph old
irate(windows_net_bytes_sent_total{job=~"$job",instance=~"$instance",nic!~'isatap.*|VPN.*'}[5m])*8>0  Legend: {{nic}}-Sent-Upload
irate(windows_net_bytes_received_total{job=~"$job",instance=~"$instance",nic!~'isatap.*|VPN.*'}[5m])*8  Legend: {{nic}}-Received-Download

## Number of Processes
Graph old
windows_os_processes{job=~"$job",instance=~"$instance"}  Legend: Number of Processes

## Service Status
Graph old
sum(windows_service_state{job=~"$job",instance=~"$instance"}) by (state)  Legend: {{state}}

## CPU коэффициент использования
Graph old
100 - avg(irate(windows_cpu_time_total{job=~"$job",instance=~"$instance",mode="idle"}[5m]))*100  Legend: CPU коэффиц. использования

## Details of the maximum disk IO of each host
Graph old
-max by (instance) (irate(windows_logical_disk_reads_total[2m]))  Legend: {{instance}}_Read
max by (instance) (irate(windows_logical_disk_writes_total[2m]))  Legend: {{instance}}_write

## The maximum disk read and write details of each host
Graph old
-max by (instance) (irate(windows_logical_disk_read_bytes_total[2m]))  Legend: {{instance}}_Read
max by (instance) (irate(windows_logical_disk_write_bytes_total[2m]))  Legend: {{instance}}_write




```


#### Правила.
https://awesome-prometheus-alerts.grep.to/rules.html
