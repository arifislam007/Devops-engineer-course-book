# **Hands-on Projects**  

## **Project 1: Deploying a Scalable Web Application on AWS**  

### **Objective:**  
To deploy a **highly available and scalable** web application on AWS using **EC2, Auto Scaling, Load Balancing, and RDS**.  

### **AWS Services Used:**  
✔ **Amazon EC2** – To host the web application.  
✔ **Elastic Load Balancer (ELB)** – To distribute traffic across instances.  
✔ **Auto Scaling Group (ASG)** – To dynamically scale instances.  
✔ **Amazon RDS** – For a managed database service.  
✔ **Amazon Route 53** – To manage domain and DNS.  

### **Step-by-Step Implementation:**  

#### **Step 1: Launch EC2 Instances**  
1. Open the **AWS Management Console** → Navigate to **EC2**.  
2. Click **Launch Instance** and select **Amazon Linux 2 or Ubuntu**.  
3. Configure security groups to allow **HTTP (port 80) and SSH (port 22)**.  
4. Attach an **IAM Role** for AWS services (e.g., S3 access).  
5. Install **Apache/Nginx** and deploy your web application:  
   ```bash
   sudo apt update -y
   sudo apt install apache2 -y
   echo "Hello from AWS Web Server" | sudo tee /var/www/html/index.html
   sudo systemctl start apache2
   sudo systemctl enable apache2
   ```  

#### **Step 2: Configure Elastic Load Balancer (ELB)**  
1. Go to **EC2 Dashboard** → Select **Load Balancers**.  
2. Click **Create Load Balancer** → Choose **Application Load Balancer (ALB)**.  
3. Configure **Target Groups** and add EC2 instances.  

#### **Step 3: Set Up Auto Scaling Group**  
1. Create an **Auto Scaling Group** under **EC2**.  
2. Define **minimum (2), maximum (5), and desired (3) instances**.  
3. Attach the **Load Balancer** to ensure automatic scaling.  

#### **Step 4: Deploy Amazon RDS for Database**  
1. Open **RDS Console** → Create a new **MySQL/PostgreSQL database**.  
2. Enable **Multi-AZ Deployment** for high availability.  
3. Connect the web application to the database using the RDS endpoint.  

#### **Step 5: Configure Amazon Route 53 for Domain Management**  
1. Register a domain or use an existing one.  
2. Create an **A Record** to point to the Load Balancer.  

### **Outcome:**  
✔ A **highly available, scalable** web application is deployed with **auto-healing capabilities**.  

---

## **Project 2: Creating a Disaster Recovery Framework Using AWS**  

### **Objective:**  
To design a **fault-tolerant, disaster recovery solution** using AWS services like **S3, Route 53, RDS, and AWS Backup**.  

### **AWS Services Used:**  
✔ **Amazon S3 & Glacier** – For data backups.  
✔ **Amazon Route 53** – For failover routing.  
✔ **Amazon RDS Multi-AZ & Read Replicas** – For database failover.  
✔ **AWS Backup** – For scheduled backups.  

### **Step-by-Step Implementation:**  

#### **Step 1: Configure Multi-AZ RDS for High Availability**  
1. Open **AWS RDS Console** → Create a **Multi-AZ** RDS database.  
2. Enable **Read Replicas** for faster recovery.  

#### **Step 2: Enable S3 Backups and Lifecycle Policies**  
1. Create an **S3 Bucket** for **daily database backups**.  
2. Configure **Lifecycle Rules** to move backups to Glacier for long-term storage.  

#### **Step 3: Implement Route 53 Failover Routing**  
1. Create a **primary and secondary** region setup.  
2. Set up **Route 53 Failover Routing Policy** to redirect traffic in case of failure.  

#### **Step 4: Automate Backups with AWS Backup**  
1. Open **AWS Backup Console** → Create a **Backup Plan**.  
2. Select **RDS, EC2, and S3** as backup resources.  
3. Set backup frequency and retention period.  

### **Outcome:**  
✔ **Automated failover and backup strategy** to recover quickly from disasters.  
