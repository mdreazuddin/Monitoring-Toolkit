### Prometheus needs to be installed and configured only on the Monitoring Server, not on the monitored servers.

**OS: Ubuntu 22.04**

**Prometheus Install and Configure step by step**

**Step-1 Download Prometheus package:** 

You can download Prometheus required version from the official website or use the below link.

```
sudo wget https://github.com/prometheus/prometheus/releases/download/v2.33.0/prometheus-2.33.0.linux-amd64.tar.gz
```

`sudo apt update`

**Step-2 Extract the Binary:** 

Once downloaded, extract the Node Exporter binary from the compressed file you need to untar.

`sudo tar xvfz prometheus-2.33.1.linux-amd64.tar.gz`

**Step 3 File move then useradd and set permission:**

`sudo mv prometheus-2.33.1.linux-amd64 /usr/local/bin/prometheus`

`sudo useradd -rs /bin/false prometheus`

`sudo chown -R prometheus:prometheus /usr/local/bin/prometheus/`

`sudo vim /usr/local/bin/prometheus/prometheus.yml` (This is Prometheus configuration file, you may edit as your requirement)

**Step-4 Now create a systemd service file for Prometheus:**

`sudo vim /etc/systemd/system/prometheus.service`  (Add below command this file)
```
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus/prometheus --config.file=/usr/local/bin/prometheus/prometheus.yml --storage.tsdb.path=/usr/local/bin/prometheus/data --web.console.templates=/usr/local/bin/prometheus/consoles --web.console.libraries=/usr/local/bin/prometheus/console_libraries
Restart=always

[Install]
WantedBy=multi-user.target
```

**Step 5 System service reload and enable:**

`sudo systemctl daemon-reload`

`sudo systemctl enable --now prometheus.service`

`sudo systemctl start prometheus.service`

**Step-4 Enable and allow ufw port**

`sudo ufw status` (If UFW is not active, enable it using below command)

`sudo ufw enable`

`sudo ufw allow 9090`

**Step-6 Verify Installation:**

`sudo systemctl status prometheus.service`

**Or**

Open your favorite browser and search in url- http://your_VM_IP:9090 (you will get output as like below)

![image](https://github.com/user-attachments/assets/c929ee4b-7f71-40a4-bb2b-eed8162b3578)

## Installation done now need to Configuration:

> Prometheus is configured using a prometheus.yml file, which defines how it scrapes metrics, configures alerting rules, and manages other settings. Here's an example of a basic scrapes metrics configuration.

`sudo vim /usr/local/bin/prometheus/prometheus.yml`

```
# Global configuration
global:
  scrape_interval: 15s  # How often to scrape targets by default
  evaluation_interval: 15s  # How often to evaluate rules by default

# Scrape configurations
scrape_configs:
  # The job name is added as a label (`job=<job_name>`) to the metrics scraped
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost/"promethues Server IP":9090']  # Monitor the Prometheus server itself

  # Example of scraping a node exporter
  - job_name: 'node_exporter'
    static_configs:
      - targets: ['192.168.1.X:9100'] # Monitor the App,DB,Email server, where installed Node exporter.
```

> Prometheus configuration is done, You may change configuration as your requirements.

**Now we will design our Grafana Dashboard, Check from Grafana.md file.**



