# Day24

# Prometheus and Alertmanager Setup

## Prerequisites

1. **Infrastructure**:
   - Multiple nodes to monitor (e.g., web servers, databases).
   - Access to these nodes for installation and configuration.

2. **Tools**:
   - **Prometheus**: Monitoring system and time-series database.
   - **Node Exporter**: Exporter for system-level metrics.
   - **MySQL Exporter**: Exporter for MySQL metrics (optional).
   - **Alertmanager**: Handles alerts sent by Prometheus.
   - **Consul** (Optional): Service discovery tool.
   - **Kubernetes** (Optional): For dynamic service discovery.

3. **Software**:
   - `curl` or `wget`: For downloading packages.
   - `tar`: For extracting downloaded files.
   - `vim` or `nano`: For editing configuration files.

4. **Networking**:
   - Ensure network connectivity between Prometheus, nodes, and Alertmanager.
   - Open necessary ports (e.g., 9090 for Prometheus, 9093 for Alertmanager).

## Deployment Steps

### 1. Configuring Jobs and Targets

**Task**: Set up a Prometheus server to monitor multiple services.

**Deliverables**:
- Configure Prometheus with jobs for monitoring different services.
- Define static and dynamic targets using file-based and service discovery methods.

**Instructions**:
1. **Install Prometheus**:
   ```sh
   wget https://github.com/prometheus/prometheus/releases/download/v2.42.0/prometheus-2.42.0.linux-amd64.tar.gz
   tar xvf prometheus-2.42.0.linux-amd64.tar.gz
   cd prometheus-2.42.0.linux-amd64
   ```
   
2. **Configure prometheus.yml:**

 - Refer to the repo.

3. **Start Prometheus:**
- ./prometheus --config.file=prometheus.yml

### 2. Using Exporters (Node Exporter)
Task: Use Node Exporter to monitor system-level metrics.

Deliverables:

Install and configure Node Exporter on all nodes.
Ensure metrics are being scraped by Prometheus.
Instructions:

Install Node Exporter:
```
wget https://github.com/prometheus/node_exporter/releases/download/v1.6.1/node_exporter-1.6.1.linux-amd64.tar.gz
tar xvf node_exporter-1.6.1.linux-amd64.tar.gz
cd node_exporter-1.6.1.linux-amd64
```
Start Node Exporter:
`./node_exporter`

### 3. Hands-on Exercise: Setting Up Exporters
Task: Configure Node Exporter and another exporter (e.g., MySQL Exporter).

Deliverables:

Demonstrate data collection from both exporters.
Create a basic Prometheus dashboard.
Instructions:

Install MySQL Exporter (if using):
```
wget https://github.com/prometheus/mysqld_exporter/releases/download/v0.13.0/mysqld_exporter-0.13.0.linux-amd64.tar.gz
tar xvf mysqld_exporter-0.13.0.linux-amd64.tar.gz
cd mysqld_exporter-0.13.0.linux-amd64
```

Configure MySQL Exporter:
```export DATA_SOURCE_NAME="user:password@tcp(mysqlserver:3306)/"
./mysqld_exporter
```
Create a Basic Dashboard:

Use Grafana or Prometheus’s built-in visualization tools.

### 4. Introduction to PromQL
Task: Learn and implement basic PromQL queries.

Deliverables:

Write queries for CPU usage, memory consumption, and disk I/O.
Instructions:

Access Prometheus Web UI:

### Go to http://localhost:9090
Example Queries:

```Average CPU usage: avg(rate(node_cpu_seconds_total[5m])) by (instance)
Memory consumption: node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes
Disk I/O: rate(node_disk_io_time_seconds_total[5m])
```

### 5. Basic Queries (Selectors, Functions, Operators)
Task: Create PromQL queries using selectors, functions, and operators.

Deliverables:

Write queries to calculate the 95th percentile of CPU usage.
Use functions like rate(), increase(), and histogram_quantile().
Instructions:

Example Queries:
```
95th percentile of CPU usage: histogram_quantile(0.95, sum(rate(node_cpu_seconds_total[5m])) by (instance, le))
Rate of increase: rate(node_network_receive_bytes_total[5m])
```

### 6. Advanced Queries and Aggregations
Task: Perform advanced data aggregation using PromQL.

Deliverables:

Calculate total memory usage and maximum disk space usage.
Instructions:

Example Queries:
```
Total memory usage: sum(node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes)
Maximum disk space usage: max(node_filesystem_size_bytes - node_filesystem_free_bytes)
```
### 7. Configuring Alertmanager
Task: Set up Alertmanager to handle alerts.

Deliverables:

Configure Alertmanager with Prometheus.
Create routing rules for alerts.
Instructions:

Install Alertmanager:
```
wget https://github.com/prometheus/alertmanager/releases/download/v0.25.0/alertmanager-0.25.0.linux-amd64.tar.gz
tar xvf alertmanager-0.25.0.linux-amd64.tar.gz
cd alertmanager-0.25.0.linux-amd64
```

Configure alertmanager.yml:
- Refer the alertmanage.yml fromrepo.

## Output:

![Screenshot from 2024-08-12 17-22-59](https://github.com/user-attachments/assets/508bdfd9-abea-4580-b72d-95a87d3049b4)

![image](https://github.com/user-attachments/assets/a9283256-f17a-4b3b-a710-1a74b8debd59)
![image](https://github.com/user-attachments/assets/e756d072-49e2-418d-be4d-6e0afcd9326f)
![image](https://github.com/user-attachments/assets/294d97b9-315c-448e-a77e-0d1b61f29964)
![image](https://github.com/user-attachments/assets/2c796485-e3f2-493c-864a-f12d6bbcc664)
![image](https://github.com/user-attachments/assets/e2fa2f1a-03c7-4b6f-96d3-083e2df1fccf)
![image](https://github.com/user-attachments/assets/459f6dbf-71e5-4624-ae1b-32b027b61bb8)
![image](https://github.com/user-attachments/assets/810a3159-43d9-4706-8853-0cf87a2927c8)
![image](https://github.com/user-attachments/assets/786ad759-ca8f-4c8e-9ed6-dc6bdbbfef93)
![image](https://github.com/user-attachments/assets/bc9f4692-da60-481b-b228-1216d157e53d)

![image](https://github.com/user-attachments/assets/cd1e30f1-117f-416f-afbd-1e6d9da9f7ab)
![image](https://github.com/user-attachments/assets/a45f607d-292c-40a3-aa8f-89659f6e9557)

![image](https://github.com/user-attachments/assets/23e219ff-3bcf-4bfb-b74a-7c3082f16640)
![image](https://github.com/user-attachments/assets/ff117cb5-6851-4297-84e5-962d649207e9)

![image](https://github.com/user-attachments/assets/0a936e66-5763-4bfb-bc6d-d6f763850260)
![image](https://github.com/user-attachments/assets/326c2173-8123-4a40-b8c3-66db3d6e71ca)

![image](https://github.com/user-attachments/assets/7c56e7f9-f54e-468a-860d-e6a03c8ebc0e)


![image](https://github.com/user-attachments/assets/511cd59c-7ce8-459e-aab1-f056cc0afaad)


## Prometheus alert:

![image](https://github.com/user-attachments/assets/59492525-1a5e-4d31-8da4-0ff495a25144)
![image](https://github.com/user-attachments/assets/c3e77a3c-fff4-46f8-9036-156ac362f741)

![image](https://github.com/user-attachments/assets/0d3c6dd4-7d4f-4cb5-a28c-638771abb282)
![image](https://github.com/user-attachments/assets/92c03a7f-e4f6-4216-a2e1-db9d107155fd)
![image](https://github.com/user-attachments/assets/9ea0cc9c-7911-462c-a3b3-e414002c0087)

## Firing Alerts on Slack:
![Uploading image.png…]()
![Uploading image.png…]()
















