# **Chapter 5: Monitoring and Logging**

## **Introduction to Monitoring and Logging**

In a modern DevOps environment, monitoring and logging are critical for ensuring the reliability, performance, and availability of applications and infrastructure. By continuously tracking metrics, logs, and other system information, you can detect issues early, analyze performance bottlenecks, and ensure your systems run smoothly.

This chapter will explore three powerful tools commonly used for monitoring and logging in DevOps workflows:

1. **Prometheus**: A powerful open-source system monitoring and alerting toolkit.
2. **Grafana**: An open-source platform for data visualization and monitoring, often used alongside Prometheus.
3. **ELK Stack** (Elasticsearch, Logstash, and Kibana): A set of tools used for logging, analysis, and visualization.

Together, these tools provide a comprehensive solution for monitoring system health, detecting issues, and visualizing data in real-time.

---

## **Prometheus: Monitoring and Alerting Toolkit**

### **What is Prometheus?**

Prometheus is an open-source system monitoring and alerting toolkit designed for reliability and scalability. It collects and stores metrics as time-series data, which are key-value pairs with a timestamp, often used for tracking metrics such as CPU usage, memory consumption, and request counts.

Prometheus is particularly popular in cloud-native environments for monitoring microservices, containers, and Kubernetes clusters. It works by scraping metrics from applications, services, and systems via HTTP endpoints.

### **Core Concepts in Prometheus**

1. **Time Series Data**: Prometheus stores data in the form of time-series, which are series of data points collected at regular intervals.
2. **Metrics**: Metrics in Prometheus are categorized into four types:
   - **Counter**: A metric that only increases (e.g., the number of requests served).
   - **Gauge**: A metric that can go up or down (e.g., memory usage).
   - **Histogram**: Measures the distribution of a set of values (e.g., request durations).
   - **Summary**: Provides a way to track the count, sum, and quantiles of a set of values.
3. **Scraping**: Prometheus scrapes metrics from HTTP endpoints exposed by applications and services.
4. **Query Language (PromQL)**: Prometheus provides a powerful query language called **PromQL** (Prometheus Query Language) for querying and manipulating time-series data.

### **Setting Up Prometheus**

1. **Installing Prometheus**:
   To install Prometheus on a Linux system, follow these steps:
   ```bash
   # Download the Prometheus binary
   wget https://github.com/prometheus/prometheus/releases/download/v2.30.3/prometheus-2.30.3.linux-amd64.tar.gz

   # Extract the tar file
   tar -xvzf prometheus-2.30.3.linux-amd64.tar.gz
   cd prometheus-2.30.3.linux-amd64

   # Start Prometheus
   ./prometheus --config.file=prometheus.yml
   ```

2. **Configuring Prometheus**:
   Prometheus configuration is done via the `prometheus.yml` file. Here's a simple example of scraping a target (e.g., a Node exporter for system metrics):

   ```yaml
   global:
     scrape_interval: 15s

   scrape_configs:
     - job_name: 'node'
       static_configs:
         - targets: ['localhost:9100']
   ```

3. **Accessing Prometheus**:
   After starting Prometheus, you can access the web interface at `http://localhost:9090`. From here, you can view metrics, run queries, and create alerts.

### **Prometheus Monitoring Example**

1. Install a **Node Exporter** to expose system metrics:
   ```bash
   # Download Node Exporter
   wget https://github.com/prometheus/node_exporter/releases/download/v1.3.1/node_exporter-1.3.1.linux-amd64.tar.gz
   tar -xvzf node_exporter-1.3.1.linux-amd64.tar.gz
   cd node_exporter-1.3.1.linux-amd64

   # Start Node Exporter
   ./node_exporter
   ```

2. In `prometheus.yml`, add the target `localhost:9100` to scrape Node Exporter metrics.

3. Visit Prometheus web interface and run queries to view system metrics, such as CPU usage:
   ```promql
   node_cpu_seconds_total
   ```

### **Prometheus Alerts**

Prometheus also supports alerting, where you can define alert rules based on your queries and receive notifications when specific conditions are met.

An example alerting rule in `prometheus.yml` could look like this:

```yaml
alerting:
  alertmanagers:
    - static_configs:
        - targets: ['localhost:9093']

rule_files:
  - 'alerts.yml'

scrape_configs:
  # Scraping and other configurations...
```

---

## **Grafana: Data Visualization and Dashboards**

### **What is Grafana?**

Grafana is an open-source visualization platform that allows you to create dashboards and graphs from your data. It is commonly used to visualize data from monitoring tools like Prometheus, Elasticsearch, and others.

Grafana provides interactive visualizations and an easy-to-use interface to build real-time dashboards that can help you monitor application and infrastructure health.

### **Setting Up Grafana**

1. **Installing Grafana**:
   You can install Grafana on Linux using the package manager:
   ```bash
   sudo apt-get install -y software-properties-common
   sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
   sudo apt-get update
   sudo apt-get install grafana

   # Start the Grafana service
   sudo systemctl start grafana-server
   sudo systemctl enable grafana-server
   ```

2. **Accessing Grafana**:
   By default, Grafana runs on port `3000`. You can access it by visiting `http://localhost:3000`. The default login credentials are `admin/admin`.

3. **Adding Prometheus as a Data Source**:
   To integrate Prometheus with Grafana, add it as a data source:
   - Go to **Configuration** -> **Data Sources**.
   - Select **Prometheus** and enter `http://localhost:9090` as the URL.

4. **Creating Dashboards**:
   Once Prometheus is added as a data source, you can start building dashboards. For example, to visualize CPU usage:
   - Create a new dashboard.
   - Add a new panel and set the query to `node_cpu_seconds_total`.

### **Visualizing Prometheus Metrics in Grafana**

1. **Creating Custom Dashboards**: Grafana allows you to create custom dashboards and panels to display real-time metrics.
   
2. **Using Pre-built Dashboards**: Grafana has a community marketplace where you can find pre-built dashboards for Prometheus, Kubernetes, and other services.

---

## **ELK Stack (Elasticsearch, Logstash, and Kibana) for Logging**

### **What is the ELK Stack?**

The **ELK Stack** consists of three tools that work together for logging and log analysis:

- **Elasticsearch**: A distributed search and analytics engine, used for storing and searching logs.
- **Logstash**: A server-side data processing pipeline that ingests logs, processes them, and sends them to Elasticsearch.
- **Kibana**: A data visualization tool that provides a web interface to search and visualize logs stored in Elasticsearch.

### **Setting Up the ELK Stack**

1. **Installing Elasticsearch**:
   Follow the [installation guide](https://www.elastic.co/guide/en/elasticsearch/reference/current/install-elasticsearch.html) to install Elasticsearch on your system.

2. **Installing Logstash**:
   Follow the [installation guide](https://www.elastic.co/guide/en/logstash/current/installing-logstash.html) to install Logstash.

3. **Installing Kibana**:
   Follow the [installation guide](https://www.elastic.co/guide/en/kibana/current/install.html) to install Kibana.

4. **Configuring Logstash to Send Logs to Elasticsearch**:
   Here’s a basic Logstash configuration (`logstash.conf`) to send logs to Elasticsearch:
   
   ```plaintext
   input {
     file {
       path => "/var/log/syslog"
       type => "syslog"
     }
   }
   
   output {
     elasticsearch {
       hosts => ["http://localhost:9200"]
       index => "syslog-%{+YYYY.MM.dd}"
     }
   }
   ```

5. **Accessing Kibana**:
   Once everything is set up, you can access Kibana by visiting `http://localhost:5601` to explore and visualize your logs.

### **Using Kibana to Visualize Logs**

1. **Creating Dashboards in Kibana**: Kibana allows you to create interactive dashboards to visualize log data.
2. **Searching Logs**: Use Kibana’s search functionality to query and analyze logs for troubleshooting and insights.

---

## **Hands-on Exercise**

### **Exercise 1: Setting Up Prometheus and Grafana**

1. Install Prometheus and Grafana on your local machine.
2. Configure Prometheus to scrape metrics from Node Exporter.
3. Create a Grafana dashboard to visualize metrics such as CPU usage, memory usage, and disk I/O.

### **Exercise 2: ELK Stack Setup**

1. Install Elasticsearch, Logstash, and Kibana.
2. Configure Logstash to ingest system logs and send them to Elasticsearch.
3. Use Kibana to create visualizations and dashboards for the ingested logs.

---

## **Summary**

In this chapter, we explored the fundamentals of monitoring and logging with three powerful tools: **Prometheus**, **Grafana**, and the **ELK Stack**. These tools provide comprehensive monitoring, visualization, and logging solutions for modern infrastructure and applications, helping you ensure system health, track performance metrics, and troubleshoot issues.

- **Prometheus** allows you to monitor system and application metrics with powerful queries and alerting.
- **Grafana** enables you to visualize metrics and create interactive dashboards for real-time monitoring.
- **ELK Stack** helps you collect, analyze, and visualize logs from various sources, providing deep insights into your systems' behavior.
