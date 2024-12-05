# Monitoring-Toolkit

**Date: May-2024**

Install &amp; configure infra/system monitoring tools.

<img width="314" alt="image" src="https://github.com/user-attachments/assets/f4655071-628e-48e3-bd55-d161ab8cf362">

> The diagram represents a theoretical monitoring setup in a network environment using Grafana, Prometheus, and Node Exporter for system health and performance monitoring.

Here's the explanation:

**Components and Roles**

**1. Monitoring Server:**

* Acts as the central node for monitoring the networked servers.
* Hosts monitoring tools such as:
  * Grafana: A visualization tool used to create dashboards and graphs.
  * Prometheus: A monitoring system that collects metrics from configured targets at given intervals.
  * Node Exporter: An agent installed on servers to expose system metrics to Prometheus.

**2. Monitored Servers:** These are the servers in the network that are monitored by the Monitoring Server. Each runs a Node Exporter instance to expose metrics such as CPU, memory, disk usage, and network statistics to Prometheus.

* **App Server:** Hosts applications critical for business operations.
* **E-mail Server:** Manages and routes email communications.
* **Database Server:** Stores and manages the database used by applications or other systems.
* **Database Backup Server:** Provides redundancy by storing backups of the database server.

**Network Setup**
* All servers are interconnected within a private subnet (192.168.10.X).
* The Monitoring Server communicates with the monitored servers over the network to collect metrics.
* Dashed lines represent network connections between the Monitoring Server and the monitored servers.

**Monitoring Workflow**
* **Node Exporter:** Installed on each monitored server, it collects server-specific metrics like CPU load, disk space, memory usage, and more.
* **Prometheus:** Periodically scrapes these metrics from the Node Exporter instances running on the monitored servers.
* **Grafana:** Connects to Prometheus to visualize the collected data in the form of dashboards, providing real-time insights into the health and performance of the network.

**Practical Applications**
* **Proactive Monitoring:** Allows administrators to detect and address potential issues (e.g., high CPU usage or low disk space) before they become critical.
* **Centralized Insights:** Provides a single pane of glass to monitor multiple servers across the network.
* **Historical Analysis:** Helps in analyzing trends and patterns over time using the metrics stored by Prometheus.

> This setup is commonly used in modern DevOps practices to ensure the reliability, performance, and scalability of IT infrastructure.
