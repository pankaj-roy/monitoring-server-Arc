# Troubleshooting Runbook

## Check Containers
```bash
docker ps
```

## Check Prometheus
```bash
docker logs prometheus
```

## Check Connectivity
```bash
curl http://SERVER:9100/metrics
curl http://SERVER:8080/metrics
```

## Check Targets
Open /targets in Prometheus and verify all targets are UP.
