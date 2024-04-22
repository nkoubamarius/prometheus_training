# Grafana from APT repository

https://grafana.com/docs/grafana/latest/setup-grafana/installation/debian/

### Install the prerequisite packages
```sh
sudo apt-get install -y apt-transport-https software-properties-common wget
```

### Import the GPG key
```sh
sudo mkdir -p /etc/apt/keyrings/
wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
```

### To add a repository for stable releases, run the following command
```sh
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

### To add a repository for beta releases, run the following command:
```sh
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com beta main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

### Run the following command to update the list of available packages:
```sh
sudo apt-get update
```

### To install Grafana OSS, run the following command:
```sh
sudo apt-get install grafana
```

### To install Grafana Enterprise, run the following command:
```sh
sudo apt-get install grafana-enterprise
```

### Start the service
```sh
sudo systemctl daemon-reload
sudo systemctl start grafana-server
sudo systemctl status grafana-server
```

### Configure the Grafana server to start at boot using systemd
```sh
sudo systemctl enable grafana-server.service
```