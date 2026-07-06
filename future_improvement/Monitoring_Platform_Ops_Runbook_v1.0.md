# Monitoring Platform Operations Runbook v1.0

## 1. Overview

Environment:
- Monitoring Server: 3.26.13.150
- Server-1: 3.27.16.72
- Server-2: 54.252.156.168

## 2. Architecture

```text
Server-1 -----------+
                    |
                    v
                Prometheus -----> Alertmanager -----> Telegram
                    |
Server-2 -----------+
                    |
                    v
                 Grafana

Future:
Alloy ---> Loki ---> Grafana
```

## 3. Components

Monitoring Server:
- Prometheus
- Grafana
- Alertmanager
- Blackbox Exporter
- Node Exporter
- cAdvisor

Node Servers:
- Node Exporter
- cAdvisor

Future:
- Loki
- Alloy
- Tenderduty
- Traefik

## 4. AWS Security Groups

Monitoring Server:
- 22/TCP
- 3000/TCP
- 9090/TCP
- 9093/TCP
- 80/TCP
- 443/TCP

Node Servers:
- 22/TCP
- 9100/TCP from monitoring server only
- 8080/TCP from monitoring server only

## 5. Prometheus Targets

- prometheus
- monitoring-node
- monitoring-cadvisor
- server1-node
- server1-cadvisor
- server2-node
- server2-cadvisor

## 6. Health Checks

Prometheus:
```bash
http://SERVER:9090/targets
```

Query:
```promql
up
```

## 7. Alert Rules

- InstanceDown
- HighCPUUsage
- HighMemoryUsage
- DiskSpaceLow

## 8. Grafana

Datasource:
```text
http://prometheus:9090
```

Recommended Dashboard:
- ID 1860

## 9. Alertmanager Roadmap

Flow:
```text
Prometheus -> Alertmanager -> Telegram
```

Required:
- Bot Token
- Chat ID

## 10. Blackbox Monitoring

Monitor:
- Grafana URL
- Public APIs
- RPC endpoints
- Websites

## 11. Loki Roadmap

```text
Alloy -> Loki -> Grafana
```

Collect:
- Docker logs
- System logs
- Application logs

## 12. Backup Strategy

Backup:
- docker-compose.yml
- prometheus.yml
- alerts.yml
- alertmanager.yml
- Grafana dashboards

Store in Git.

## 13. Disaster Recovery

1. Launch replacement EC2.
2. Install Docker.
3. Restore compose files.
4. Restore volumes.
5. Start stack.
6. Verify targets.

## 14. Upgrade Procedure

```bash
docker compose pull
docker compose up -d
```

Verify:
```bash
docker ps
```

## 15. Troubleshooting

Container status:
```bash
docker ps
```

Prometheus logs:
```bash
docker logs prometheus
```

Grafana logs:
```bash
docker logs grafana
```

Target connectivity:
```bash
curl http://3.27.16.72:9100/metrics
curl http://54.252.156.168:9100/metrics
```

## 16. Production Hardening Checklist

- [ ] Telegram alerts configured
- [ ] Grafana dashboard imported
- [ ] Loki deployed
- [ ] Alloy deployed
- [ ] HTTPS enabled
- [ ] Daily backups
- [ ] Infrastructure in Git
- [ ] Alert testing completed
- [ ] Documentation updated

## 17. Current Status

Completed:
- Monitoring server deployed
- Prometheus configured
- Alert rules configured
- Server-1 monitored
- Server-2 monitored
- Node Exporter verified
- cAdvisor verified

Next:
- Grafana dashboards
- Telegram alerts
- Loki
- Alloy
- HTTPS
