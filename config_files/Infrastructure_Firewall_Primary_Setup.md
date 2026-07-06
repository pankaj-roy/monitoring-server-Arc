# Infrastructure, Primary Setup and Firewall

## Architecture
```text
Monitoring Server (3.26.13.150)
├── Prometheus
├── Alertmanager
├── Grafana
├── Blackbox
├── Node Exporter
└── cAdvisor

Server-1 (3.27.16.72)
└── Node Exporter + cAdvisor

Server-2 (54.252.156.168)
└── Node Exporter + cAdvisor
```

## Monitoring Ports
- 3000 Grafana
- 9090 Prometheus
- 9093 Alertmanager
- 9100 Node Exporter
- 8080 cAdvisor
- 9115 Blackbox

## Monitoring Server Security Group
- TCP 22 from your IP
- TCP 3000 from your IP
- TCP 9090 from your IP
- TCP 9093 from your IP
- TCP 80 from Internet
- TCP 443 from Internet

## Server-1 and Server-2 Security Group
- TCP 22 from your IP
- TCP 9100 from 3.26.13.150/32
- TCP 8080 from 3.26.13.150/32

## Validation Commands
```bash
curl http://3.27.16.72:9100/metrics
curl http://54.252.156.168:9100/metrics
curl http://3.27.16.72:8080/metrics
curl http://54.252.156.168:8080/metrics
```
