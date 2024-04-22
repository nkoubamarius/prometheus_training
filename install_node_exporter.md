# Node Exporter

 Node Exporter : https://github.com/prometheus/node_exporter

 Préparation 
```
sudo useradd -rs /bin/false node_exporter
https://prometheus.io/download/#node_exporter
wget https://github.com/prometheus/node_exporter/releases/download/v1.7.0/node_exporter-1.7.0.linux-amd64.tar.gz
tar -xvzf node_exporter-1.7.0.linux-amd64.tar.gz
sudo mv node_exporter-1.7.0.linux-amd64/node_exporter /usr/local/bin/
sudo chown node_exporter:node_exporter /usr/local/bin/node_exporter

```

Installer le service systemd pour notre node Exporter

```
sudo nano /etc/systemd/system/node_exporter.service
```

```
[Unit]
Description=Node Exporter
After=network-online.target
[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter --web.listen-address=:7676
[Install]
WantedBy=multi-user.target
```

Demarer le service Node-Exporter

```
sudo systemctl daemon-reload
sudo systemctl enable node_exporter
sudo systemctl start node_exporter
```

Ajouter la config de Scraping a prometheus

```
sudo nano /etc/prometheus/prometheus.yml
```

```
 - job_name: node-exporter
   static_configs:
      - targets: ['192.168.50.103:7676']
```

```
sudo systemctl restart prometheus
```

## Ajouter des Métriques

Node Exporter Dashboard ID : 1860
![Alt text](<./screenshots/node_exporter.png>)
