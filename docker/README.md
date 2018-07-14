# Prometheus, Alertmanager, Consul and Grafana Docker container


## deployment:
```sh
# docker build -t prom docker/
# docker run -d --name=prom -p 80:80 -p 443:443 -p 9090:9090 -p 3000:3000 -p 9093:9093 -p 8300:8300 -p 8301:8301 -p 8302:8302 prom
# docker exec -i -t $CONTAINER_ID /bin/sh
```

## Port breakdown
9090 - Prometheus daemon [should be bound to lo on Prod, only open for demo purposes]
3000 - Grafana
9093 - Alertmanager [should be bound to lo on Prod, only open for demo purposes]
830{0,1,2} - Consul
