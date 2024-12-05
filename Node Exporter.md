### Node Exporter needs to be installed and configured on all monitored servers to collect metrics.

**OS:** Ubuntu 22

**Installation and Configuration step by step:**

 **Node Exporter Installation:**

**Step -1 Download Node Exporter:** 

Download the Node Exporter binary. Find the appropriate version for your architecture, you may get from below link.

`sudo wget https://github.com/prometheus/node_exporter/releases/download/v1.8.0/node_exporter-1.8.0.linux-amd64.tar.gz`

**Step-2 Extract the Binary:** 

Once downloaded, extract the Node Exporter binary from the compressed file you need to untar.

`sudo tar xvfz node_exporter-1.8.0.linux-amd64.tar.gz`

**Step-3 Move the Binary:** 

Move the extracted binary to a directory of your choice, typically somewhere in your system's **bin** directory or **/usr/local/bin** for Linux systems.

`sudo mv node_exporter-1.8.0.linux-amd64/node_exporter /usr/local/bin/`

**Then create user and give permission:**

`sudo useradd -rs /bin/false node_exporter`

`sudo chmod +x /usr/local/bin/node_exporter`

**Step-4 Create a Systemd Service File:** 

Create a systemd service file to manage Node Exporter as a service. Here's a basic example to Create a file named **node_exporter.service** in **/etc/systemd/system/**

`sudo vim /etc/systemd/system/node_exporter.service` (add bellow commands in your file)

```
Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
```

**Step-5 Start and Enable the Service**

`sudo systemctl daemon-reload`

`sudo systemctl start node_exporter`

`sudo systemctl enable node_exporter`

**Step-6 Enable and allow ufw port**

`sudo ufw status`  "If UFW is not active, enable it using below command:"

`sudo ufw enable`

`sudo ufw allow 3000`

**Step-7: Verify Installation:** 

Check the status of the Node Exporter service to ensure it's running without any issues

`sudo systemctl status node_exporter`

**Or**

Open your favorite browser and search in url- **http://"your server IP":9100** (you will get output as like below)
![image](https://github.com/user-attachments/assets/2bfc2616-3af3-4b9f-ae48-e06b1dbf8163)








