# AWS Monitoring Stack

## Architecture

```text
Monitoring Server (3.26.13.150)
├── Prometheus
├── Alertmanager
├── Grafana
├── Blackbox Exporter
├── Node Exporter
└── cAdvisor

Server-1 (3.27.16.72)
├── Node Exporter
└── cAdvisor

Server-2 (54.252.156.168)
├── Node Exporter
└── cAdvisor
```

## Monitoring Flow

### Metrics

```text
Server-1 Node Exporter ----┐
Server-1 cAdvisor ---------|
                           |
Server-2 Node Exporter ----|--> Prometheus --> Grafana
Server-2 cAdvisor ---------|
                           |
Monitoring Server ---------┘
```

### Alerting

```text
Prometheus
    ↓
Alertmanager
    ↓
Telegram (planned)
```

## Security Groups

### Monitoring Server (3.26.13.150)

Allowed Inbound:

- TCP 22 (SSH)
- TCP 3000 (Grafana)
- TCP 9090 (Prometheus)
- TCP 9093 (Alertmanager)
- TCP 80 (HTTP)
- TCP 443 (HTTPS)

### Server-1 and Server-2

Allowed Inbound:

- TCP 22 (SSH)
- TCP 9100 from Monitoring Server only
- TCP 8080 from Monitoring Server only

## Prometheus Targets

- monitoring-node
- monitoring-cadvisor
- server1-node
- server1-cadvisor
- server2-node
- server2-cadvisor

## Validation Commands

### Node Exporter

```bash
curl http://3.27.16.72:9100/metrics
curl http://54.252.156.168:9100/metrics
```

### cAdvisor

```bash
curl http://3.27.16.72:8080/metrics
curl http://54.252.156.168:8080/metrics
```

### Prometheus Config

```bash
docker run --rm \
-v $(pwd)/prometheus:/etc/prometheus \
--entrypoint promtool \
prom/prometheus \
check config /etc/prometheus/prometheus.yml
```

### Alert Rules

```bash
docker run --rm \
-v $(pwd)/prometheus:/etc/prometheus \
--entrypoint promtool \
prom/prometheus \
check rules /etc/prometheus/alerts.yml
```

## Current Status

- Prometheus configured
- Alert rules configured
- Server-1 monitored
- Server-2 monitored
- cAdvisor working
- Node Exporter working
- Ready for Grafana dashboards
- Ready for Telegram alerts
- Ready for Loki + Alloy integration

## Next Steps

1. Verify all targets are UP.
2. Add Grafana Prometheus datasource.
3. Import Dashboard ID 1860.
4. Configure Alertmanager Telegram notifications.
5. Deploy Loki.
6. Deploy Alloy.
7. Enable centralized logging.
8. Configure HTTPS using Traefik or Nginx.
