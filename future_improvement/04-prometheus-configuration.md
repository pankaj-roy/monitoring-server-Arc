# Prometheus Configuration

## Jobs
- monitoring-node
- monitoring-cadvisor
- server1-node
- server1-cadvisor
- server2-node
- server2-cadvisor

## Validation
```bash
promtool check config prometheus.yml
promtool check rules alerts.yml
```
