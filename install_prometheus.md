# Prometheus 

### Mettre à jour les packages système

```sh
sudo apt update
```

### Créer un utilisateur système pour Prometheus
```sh
sudo groupadd --system prometheus
sudo useradd -s /sbin/nologin --system -g prometheus prometheus
```
### Créer des répertoires pour Prometheus
```sh
sudo mkdir /etc/prometheus
sudo mkdir /var/lib/prometheus
```

### Téléchargez et extraire Prometheus
```sh
wget  https://github.com/prometheus/prometheus/releases/download/v2.51.1/prometheus-2.51.1.linux-amd64.tar.gz

tar vxf prometheus*.tar.gz

cd prometheus*/
```
### Déplacez les fichiers binaires
```sh
sudo mv prometheus /usr/local/bin
sudo mv promtool /usr/local/bin
sudo chown prometheus:prometheus /usr/local/bin/prometheus
sudo chown prometheus:prometheus /usr/local/bin/promtool
```

### Déplacer les fichiers de configuration 
```sh
sudo mv consoles /etc/prometheus
sudo mv console_libraries /etc/prometheus
sudo mv prometheus.yml /etc/prometheus

sudo chown prometheus:prometheus /etc/prometheus
sudo chown -R prometheus:prometheus /etc/prometheus/consoles
sudo chown -R prometheus:prometheus /etc/prometheus/console_libraries
sudo chown -R prometheus:prometheus /var/lib/prometheus

sudo nano /etc/prometheus/prometheus.yml
```

### Créer le service Prometheus Systemd

```sh
sudo nano /etc/systemd/system/prometheus.service
```

```sh
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
    --config.file /etc/prometheus/prometheus.yml \
    --storage.tsdb.path /var/lib/prometheus/ \
    --web.console.templates=/etc/prometheus/consoles \
    --web.console.libraries=/etc/prometheus/console_libraries

[Install]
WantedBy=multi-user.target
```

### Reload Systemd
```sh
sudo systemctl daemon-reload
```

###  Start Prometheus Service
```sh
sudo systemctl enable prometheus
sudo systemctl start prometheus

sudo systemctl status prometheus
```

### Access Prometheus Web Interface
```sh
sudo ufw allow 9090/tcp
```