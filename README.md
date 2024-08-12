# Prometheus and Node Exporter Setup

## Prerequisites

1. **Install Prometheus**:
   Follow the guide to install Prometheus on your Ubuntu machine: [Install Prometheus on Ubuntu](https://www.cherryservers.com/blog/install-prometheus-ubuntu)

2. **Install Node Exporter**:
   Follow the official documentation to install Node Exporter: [Node Exporter Guide](https://prometheus.io/docs/guides/node-exporter/)

## Prometheus Configuration

Ensure your `prometheus.yml` configuration file is set up as follows to scrape metrics from Node Exporter:

```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets: []

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  # - "first_rules.yml"
  # - "second_rules.yml"

# Scrape configuration for Prometheus
scrape_configs:
  - job_name: "prometheus"
    static_configs:
      - targets: ["localhost:9090"]

  - job_name: "node_exporter"
    static_configs:
      - targets: ["<NODE_EXPORTER_IP>:9100"]
      
 ```     
# Configuration and Monitoring Setup

## Firewall Configuration

### Allow Ports in UFW

To configure the firewall using UFW (Uncomplicated Firewall), run the following commands to allow traffic on ports 9100 and 9090:

```bash
sudo ufw allow 9100/tcp
sudo ufw allow 9090/tcp
sudo ufw reload
```
# Network Security Group (NSG) Rules (for Azure VMs)
Ensure that your Network Security Group (NSG) rules allow inbound traffic on the necessary ports:

### Allow inbound traffic on port 9100.
### Allow inbound traffic on port 9090.

## Dashboard
- ![image](https://github.com/user-attachments/assets/78576620-dc1c-43ff-9ae1-1ae566ecac63)
- ![image](https://github.com/user-attachments/assets/e5fe4863-d7a5-4787-8e80-5e22bd7fd7ef)

# Prometheus Query Language (PromQL) Basic Queries

## CPU Usage
```
Query: 100 - (avg by (instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)
```
- ![image](https://github.com/user-attachments/assets/c15ffd3c-d156-44d8-99fd-5bdf0ff7628e)
- ![image](https://github.com/user-attachments/assets/aeca7e62-fec6-40d2-8551-fbb9f1a93dbe)


### Description: Calculates the percentage of CPU usage by subtracting idle CPU time from 100%.

## Memory Usage
```
Query: node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes
```
- ![image](https://github.com/user-attachments/assets/55b46c5f-3151-49bc-80d2-7e37934dddcd)
- ![image](https://github.com/user-attachments/assets/db577e82-cc37-4527-a36a-fe1cdedda065)


### Description: Shows the amount of memory in use by subtracting available memory from the total memory.

## Disk I/O
```
Query: rate(node_disk_io_time_seconds_total[5m])
```
- ![image](https://github.com/user-attachments/assets/2047d25c-770d-446c-84a3-6f3fce263c67)
- ![image](https://github.com/user-attachments/assets/be3ed879-d7cc-448a-9dc5-5c066b0c3cf4)


### Description: Measures the rate of disk I/O operations over the past 5 minutes.

## Network Traffic
```
Query: rate(node_network_receive_bytes_total[5m])
```
- ![image](https://github.com/user-attachments/assets/1b6997a7-78bf-40a1-a738-bba03eb18fec)
- ![image](https://github.com/user-attachments/assets/e7091453-f7ef-4e5c-8182-a42ca6fe3910)


### Description: Displays the rate of incoming network traffic over the past 5 minutes.

## System Load
```
Query: node_load1
```
- ![image](https://github.com/user-attachments/assets/98e3b764-0c19-4c94-8686-db2b8890dbea)
- ![image](https://github.com/user-attachments/assets/aaf51d8f-7bd3-433e-b525-f644af963807)


### Description: Shows the 1-minute load average of the system.
