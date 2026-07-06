# Monitoring Server Setup

## Server
- Monitoring Server IP: 3.26.13.150

## Components
- Prometheus
- Alertmanager
- Grafana
- Blackbox Exporter
- Node Exporter
- cAdvisor

## Prometheus Responsibilities
- Scrape local exporters
- Scrape Server-1 exporters
- Scrape Server-2 exporters
- Evaluate alert rules
- Send alerts to Alertmanager

## Grafana
- Datasource: Prometheus
- Dashboard ID: 1860 (Node Exporter Full)

## Validation
```bash
http://3.26.13.150:9090/targets
```
All targets should be UP.

## Next Phase
- Telegram alerts
- Loki
- Alloy
- HTTPS via Traefik/Nginx
