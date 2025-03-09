### **Easy Hinglish Notes on Prometheus**  

#### **1. Prometheus Kya Hai?**  
Prometheus ek **monitoring tool** hai jo **metrics collect** karta hai aur **alert bhejta hai** jab kuch issue hota hai. Ye **cloud, Kubernetes, aur microservices** ke liye best hai.  

---

#### **2. Prometheus Ke Features**  

✔️ **Time-Series Data** – Data **time ke basis pe store** hota hai.  
✔️ **Pull Model** – Prometheus **metrics khud fetch** karta hai.  
✔️ **PromQL** – Query likh ke metrics ko analyze kar sakte hain.  
✔️ **Alerting** – Alert bhejne ka system Alertmanager ke saath aata hai.  
✔️ **Service Discovery** – Kubernetes aur cloud services se **automatic target detect** kar sakta hai.  

---

#### **3. Prometheus Setup (Linux)**  

📌 **Step 1: Install Prometheus**  
```sh
wget https://github.com/prometheus/prometheus/releases/download/v2.50.1/prometheus-2.50.1.linux-amd64.tar.gz
tar -xvf prometheus-2.50.1.linux-amd64.tar.gz
cd prometheus-2.50.1.linux-amd64
./prometheus --config.file=prometheus.yml
```

📌 **Step 2: Configure `prometheus.yml`**  
```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: "node_exporter"
    static_configs:
      - targets: ["localhost:9100"]
```

📌 **Step 3: Start Prometheus Service**  
```sh
sudo systemctl start prometheus
sudo systemctl enable prometheus
```

---

#### **4. PromQL Queries (Data Fetch Karne Ke Liye)**  

✅ **Check Running Targets:**  
```sh
up
```
✅ **CPU Usage:**  
```sh
node_cpu_seconds_total
```
✅ **Last 5 Min CPU Usage:**  
```sh
rate(node_cpu_seconds_total[5m])
```
✅ **Total HTTP Requests Count:**  
```sh
http_requests_total
```

---

#### **5. Exporters (Extra Data Collect Karne Ke Liye)**  

🛠️ **Node Exporter** – System ka CPU, RAM, Disk check karta hai.  
🛠️ **Blackbox Exporter** – Websites aur APIs ko monitor karta hai.  
🛠️ **MySQL Exporter** – MySQL database ka status check karta hai.  

📌 **Node Exporter Install Karna:**  
```sh
wget https://github.com/prometheus/node_exporter/releases/download/v1.7.0/node_exporter-1.7.0.linux-amd64.tar.gz
tar -xvf node_exporter-1.7.0.linux-amd64.tar.gz
cd node_exporter-1.7.0.linux-amd64
./node_exporter
```
🔗 Access Node Exporter: **http://localhost:9100/metrics**  

---

#### **6. Alert Setup (Alertmanager Se Notification Bhejna)**  

📌 **Step 1: Install Alertmanager**  
```sh
wget https://github.com/prometheus/alertmanager/releases/download/v0.27.0/alertmanager-0.27.0.linux-amd64.tar.gz
tar -xvf alertmanager-0.27.0.linux-amd64.tar.gz
cd alertmanager-0.27.0.linux-amd64
./alertmanager --config.file=alertmanager.yml
```

📌 **Step 2: `alertmanager.yml` Configure Karna**  
```yaml
route:
  receiver: "email_alert"

receivers:
  - name: "email_alert"
    email_configs:
      - to: "admin@example.com"
        from: "prometheus@example.com"
        smarthost: "smtp.example.com:587"
```

📌 **Step 3: Alert Rule Set Karna (`alert.rules.yml`)**  
```yaml
groups:
  - name: CPU_Alerts
    rules:
      - alert: HighCPUUsage
        expr: avg(rate(node_cpu_seconds_total[5m])) > 0.8
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "High CPU Usage Detected"
          description: "CPU usage 80% se zyada hai 5 minute se."
```

---

#### **7. Grafana Integration (Graph Banane Ke Liye)**  

📌 **Step 1: Install Grafana**  
```sh
sudo apt install grafana
sudo systemctl start grafana-server
```
📌 **Step 2: Prometheus Ko Grafana Me Add Karna**  
- Grafana UI pe jao (`http://localhost:3000`)  
- **Settings > Data Sources > Prometheus Add Karo**  
- Dashboards create karke metrics visualize karo  

---

#### **8. Prometheus Use Cases**  

✔️ **System Monitoring** – CPU, RAM, Disk usage check karne ke liye  
✔️ **Kubernetes Monitoring** – Pods aur nodes ki health track karne ke liye  
✔️ **Application Performance** – API response time aur failures check karne ke liye  
✔️ **Database Monitoring** – MySQL, PostgreSQL performance analyze karne ke liye  

---

### **Conclusion**  
Prometheus ek **powerful monitoring tool** hai jo **real-time data collect** karta hai aur **alerts bhejta hai jab kuch issue hota hai**. Agar aap **server, cloud ya Kubernetes** use kar rahe ho to Prometheus **best choice** hai.  


### **Easy Hinglish Notes on Grafana**  

#### **1. Grafana Kya Hai?**  
Grafana ek **open-source visualization tool** hai jo **data ko graphs aur dashboards** ke form me dikhata hai. Iska use **monitoring aur alerting** ke liye hota hai.  

✅ **Popular Monitoring Tools ke saath kaam karta hai:** Prometheus, InfluxDB, MySQL, Elasticsearch, AWS CloudWatch, etc.  
✅ **Real-time Data Visualization** karta hai.  
✅ **Custom Dashboards** bana sakte hain.  

---

#### **2. Grafana Ke Features**  

✔️ **Interactive Dashboards** – Custom graphs aur charts bana sakte hain.  
✔️ **Multiple Data Sources** – Prometheus, MySQL, PostgreSQL, Elasticsearch, etc.  
✔️ **Alerting System** – Jab koi issue ho, email ya Telegram pe alert bhej sakte hain.  
✔️ **User Authentication** – Role-based access control (RBAC) milta hai.  
✔️ **Plugins Support** – Extra features ke liye plugins add kar sakte hain.  

---

#### **3. Grafana Installation (Linux)**  

📌 **Step 1: Install Grafana**  
```sh
sudo apt update
sudo apt install -y grafana
```
📌 **Step 2: Start Grafana Service**  
```sh
sudo systemctl start grafana-server
sudo systemctl enable grafana-server
```
📌 **Step 3: Open Grafana UI**  
🔗 **http://localhost:3000** (Default username: `admin`, password: `admin`)  

---

#### **4. Prometheus Ko Grafana Me Add Karna**  

📌 **Step 1: Login to Grafana**  
- Open **http://localhost:3000**  
- Username/Password: **admin/admin**  

📌 **Step 2: Data Source Add Karna**  
- **Settings > Data Sources > Add New Data Source**  
- **Select "Prometheus"**  
- URL: **http://localhost:9090**  
- **Save & Test** button click karo  

📌 **Step 3: Dashboard Create Karna**  
- **Create > Dashboard > Add New Panel**  
- **Query likho (PromQL use karke)**  
- Example:  
  ```sh
  node_cpu_seconds_total
  rate(node_cpu_seconds_total[5m])
  ```
- Graph show hoga, **Save Dashboard** button dabao  

---

#### **5. Alert Setup in Grafana**  

📌 **Step 1: Alert Rule Create Karo**  
- Dashboard me jao  
- **Edit Panel > Alert > Create Alert Rule**  
- **Condition Set Karo:**  
  ```sh
  avg(rate(node_cpu_seconds_total[5m])) > 0.8
  ```
- **For: 5m (Agar 5 min tak issue rahe to alert bhejo)**  

📌 **Step 2: Notification Channel Set Karo**  
- **Alerting > Notification Channels**  
- **Telegram, Slack, Email, Webhook** set kar sakte ho  

---

#### **6. Grafana Use Cases**  

✔️ **Server Monitoring** – CPU, RAM, Disk usage check karna  
✔️ **Application Performance** – API response time aur errors track karna  
✔️ **Kubernetes Monitoring** – Pods aur nodes ki health track karna  
✔️ **Database Monitoring** – MySQL, PostgreSQL performance analyze karna  

---

### **Conclusion**  
Grafana ek **powerful monitoring tool** hai jo **real-time data visualize** karta hai aur **alerts bhejta hai jab kuch issue hota hai**. Agar aap **Prometheus, Kubernetes, ya MySQL** use kar rahe ho to Grafana **best choice** hai.  




