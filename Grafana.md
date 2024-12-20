### Grafana needs to be installed and configured only on the Monitoring Server, not on the monitored servers.
**OS:** Ubuntu 22.04

**Grafana Install and Configure step by step**

**Step-1 Download and install Grafana package:**
> Download the latest Grafana package for Ubuntu and download the Grafana GPG key and add it to the list of trusted keys on your system. This allows your package manager (APT) to verify the authenticity of Grafana packages when you install them.

`sudo apt install -y software-properties-common`

`sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"`

`sudo curl https://packages.grafana.com/gpg.key | sudo apt-key add -`


**Step-2 System update and  Install grafana:**

`sudo apt update`

`sudo apt install grafana`

**Step 3 service start and enable:**

`systemctl start grafana-server`

`systemctl enable grafana-server`

**Step-4 Enable and allow ufw port**

`sudo ufw status`  "If UFW is not active, enable it using below command:"

`sudo ufw enable`

`sudo ufw allow 3000`

**Step-5 Verify the installation**

`systemctl status grafana-server`

**Or**

Open your favorite browser and search in url- http://"your server IP":3000 **(default user and password is admin)** you will see an interface like below:

![image](https://github.com/user-attachments/assets/8f9aa53d-0931-47d8-9525-38e6dfa65eca)


## Grafana Dashboard Design

**Grafana Dashboard Data collection:**
> Click Home button and follow the process:

![image](https://github.com/user-attachments/assets/c1e02a7a-a3c4-41b5-b565-e239a4cd74cb)

- **Search option type Prometheus and click that**
- **You will find “Connection”**
    - **Prometheus server URL: http://prometheus Server IP:9090**

**Then Click save & Test**

**Create a New Dashboard**
- Navigate to Dashboards:
  - Click on the "+" icon on the left-hand menu and select Dashboard.
- Add a Panel:
  - Click on Add new panel.
- Select Prometheus as the Data Source:
  - In the query editor, ensure Prometheus is selected as the data source.
- Visualize the Data:
  - Choose a visualization type (e.g., Graph, Gauge, Table) from the options above the query editor.
- Save the Panel:
  - Provide a title for the panel and save it.

-Go to your browser and type in url, **http://"grafana server IP":3000** (You can see a good dashboard, Example as like below)

![image](https://github.com/user-attachments/assets/1722df93-f88b-49c7-8c7c-9c30aeb45afc)

**NB: You may customized your dashboard, Go to your browser and open new tab, just search Grafana dashboard and copy data source & Collator ID then import to your public grafana dashboard will see exact data.**
