# Grafana Configuration Setup AWS EC2 & DROPLET Instance

- grafana installation

```
sudo apt-get install -y apt-transport-https
sudo apt-get install -y software-properties-common wget
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
sudo apt-get update
sudo apt-get install grafana
```
<br>

- clone or download prometheus linux 64-bit from github release official repo
```
ln -s /home/zero/Documents/grafana/prometheus/prometheus /usr/local/bin/prometheus
```
<br>

- download loki linux-64 bit binary from github release official repo and run /port 3100/metrics
- download node_exporter from official prometheus.io official website and run / port 9100/metrics
- download promtail linux-64 bit binary from github release official repo and run / port 9090/metrics
- extract both files using tar -xzf <file.tar.gz>
- chmod a+x loki and chmod a+x promtail
- create and configure /etc/systemd/system/prometheus.service via code editor choice
```
[Unit]
Description=Prometheus service
After=network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/prometheus --config.file=/home/zero/Documents/grafana/prometheus/prometheus.yml

[Install]
WantedBy=multi-user.target
```

<br>

- create and configure /etc/systemd/system/loki.service via code editor choice
```
[Unit]
Description=Loki service
After=network.target

[Service]
Type=simple
ExecStart=/home/zero/Documents/grafana/loki -config.file /opt/grafana/loki/local-loki.yml

[Install]
WantedBy=multi-user.target
```

<br>

- create and configure /etc/systemd/system/promtail.service via code editor choice

```
[Unit]
Description=Promtail service
After=network.target

[Service]
Type=simple
ExecStart=/home/zero/Documents/grafana/promtail -config.file /opt/grafana/loki/promtail.yml

[Install]
WantedBy=multi-user.target
```
<br>

- run service and stop
```
sudo systemctl daemon-reload
sudo service prometheus start
sudo service prometheus stop
sudo service loki start
sudo service loki stop
sudo service promtail start
sudo service promtail stop
```
<br> 

`/opt/grafana/loki/*.yml file configuration are located`
