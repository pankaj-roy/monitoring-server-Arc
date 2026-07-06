# Server-1 and Server-2 Setup

## Servers
- Server-1: 3.27.16.72
- Server-2: 54.252.156.168

## Installed Components
- Node Exporter
- cAdvisor

## Node Exporter
Port:
```text
9100
```

Validation:
```bash
curl http://SERVER_IP:9100/metrics
```

## cAdvisor
Port:
```text
8080
```

Validation:
```bash
curl http://SERVER_IP:8080/metrics
```

## Monitoring Flow
```text
Server -> Exporters -> Prometheus -> Grafana
```

## Security
Only monitoring server should access:
- 9100
- 8080
