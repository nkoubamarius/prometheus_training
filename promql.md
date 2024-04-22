##  PromQL: Filtres sur les Labels

les labels permettent de faire du filtrage

- Equivalent a une clause WHERE 
- utlise les Regex  GO
- Conseils : https://prometheus.io/docs/practices/naming/

Rename labels

```
scrape_configs:
  - job_name: Consul
    consul_sd_configs:
      - server: '192.168.57.10:8500'
        datacenter: 'mydc'
    relabel_configs:
      - source_labels: [__meta_consul_service]
        target_label: job
```

### Requêtes:

```
up{job="node"}
up{job="node_exporter"}
node_network_receive_bytes_total{device="ens33"}
```

Different de 
```
node_network_receive_bytes_total{device!="ens33"}
```

Regex
```
node_network_receive_bytes_total{device=~"ens.*"}
node_network_receive_bytes_total{device=~"ens33|lo"}
```

Multiple filtres 
```
node_network_receive_bytes_total{instance=~"localhost:.+", device=~"ens33|lo"}
```

## PromQl: Group By

Operation d'aggregation: count , sum 

cluse = by ()
(cpu, instance)

```
count(node_cpu_seconds_total) 

count(node_cpu_seconds_total) by(instance)
count(node_cpu_seconds_total) by(instance, cpu)

count(count(node_cpu_seconds_total) by(instance, cpu)) by (instance)
```

## PromQl: Les Intervalles de temps

Prometheus scrape que la dernière value connue

- Range Vector : []
  - cherche tous les timeseries sur u interval de temps
  - par defaut par rapport a maintenant 
```
node_load1[1m]
```
- Offset : offset 3m
 - change la date a laquelle on recherche la timeseries 

```
node_load1[1m] offset 3m
```

- Conversion
 date -d "@1711004584.27"


## PromQL : Offset

```
node_load1 - node_load5 offset 10m
```

- Offset permet de deplacer son point de reference
- ideal pour comparer  2 periodes
node_load1 - node_load1 offset 30m
node_load1 - sum_over_time(node_load1[5m] offset 5m)


