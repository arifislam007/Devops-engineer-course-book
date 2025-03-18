# **Chapter 2: AWS Compute Services**  

## **2.1 Introduction to AWS Compute Services**  
AWS offers a variety of **compute services** that allow users to run applications with different performance, scalability, and pricing models. Compute services include **virtual servers, containerized applications, and serverless computing** to meet various use cases.

### **Types of AWS Compute Services**  
🔹 **Amazon EC2 (Elastic Compute Cloud):** Provides scalable virtual machines.  
🔹 **Auto Scaling Groups:** Automatically adjusts the number of EC2 instances.  
🔹 **Elastic Load Balancing (ELB):** Distributes traffic across multiple EC2 instances.  
🔹 **AWS Lambda:** Serverless compute for running functions without managing infrastructure.  
🔹 **Amazon ECS (Elastic Container Service):** Containerized application management.  
🔹 **AWS Elastic Beanstalk:** PaaS for deploying web applications.  

---

## **2.2 Amazon EC2 (Elastic Compute Cloud)**  
### **What is EC2?**  
Amazon **EC2 (Elastic Compute Cloud)** provides **resizable** compute capacity in the cloud. It allows users to launch virtual machines called **instances**, configure storage, networking, and security, and scale them based on demand.

### **Key Features of EC2**  
✔ **On-demand instances:** Pay only for what you use.  
✔ **Reserved instances:** Reduce costs by committing to long-term usage.  
✔ **Spot instances:** Cost-effective option for non-critical workloads.  
✔ **Scalability:** Auto Scaling and Load Balancers for performance optimization.  
✔ **Security:** Integrated with **IAM, security groups, and VPC**.  

---

### **2.2.1 EC2 Instance Types**  
AWS offers different instance types optimized for various workloads:  

| Instance Type | Use Case | Example |  
|--------------|---------|---------|  
| **General Purpose** | Balanced compute, memory, and networking | t3.micro, m5.large |  
| **Compute Optimized** | High-performance computing | c5.large, c5.2xlarge |  
| **Memory Optimized** | High-memory applications | r5.large, x1.16xlarge |  
| **Storage Optimized** | High-speed storage requirements | i3.large, d2.xlarge |  
| **GPU Optimized** | Machine learning and gaming | g4dn.xlarge, p3.8xlarge |  

---

### **2.2.2 Launching an EC2 Instance (Hands-on Lab)**  
#### **Step 1: Login to AWS Console & Navigate to EC2**  
1. Open the **AWS Management Console**.  
2. Search for **EC2** and click **Launch Instance**.  

#### **Step 2: Configure EC2 Instance**  
- **Choose an AMI (Amazon Machine Image):** Select **Amazon Linux 2**.  
- **Choose an Instance Type:** Select **t2.micro** (Free Tier).  
- **Configure Instance Details:** Default settings are fine.  
- **Add Storage:** 8GB **EBS** volume (default).  
- **Add Tags:** Name your instance (e.g., "WebServer").  
- **Configure Security Group:** Allow **SSH (22), HTTP (80), and HTTPS (443)**.  

#### **Step 3: Launch the Instance**  
- Create a **new key pair** or use an existing one.  
- Click **Launch** and wait for the instance to start.  
- Connect using SSH:  
```bash
ssh -i my-key.pem ec2-user@<EC2-PUBLIC-IP>
```

---

## **2.3 Amazon Machine Image (AMI)**  
### **What is an AMI?**  
An **Amazon Machine Image (AMI)** is a pre-configured template used to launch EC2 instances. It includes:  
✔ The **operating system** (Linux, Windows)  
✔ Pre-installed software and configurations  
✔ Custom application setup  

### **Creating a Custom AMI**  
1. **Launch an EC2 Instance** and configure it.  
2. **Install required software and settings.**  
3. Navigate to **EC2 > Instances > Actions > Create Image (AMI)**.  
4. Provide a **name** and **description** for the AMI.  
5. Click **Create Image**, and it will be stored in **AMI section**.  

---

## **2.4 Auto Scaling Groups (ASG)**  
### **What is Auto Scaling?**  
Auto Scaling ensures **high availability and cost efficiency** by automatically adjusting the number of running EC2 instances based on traffic or demand.

### **Key Features of Auto Scaling**  
✔ **Dynamic Scaling:** Adds/removes instances based on CPU, RAM, or network usage.  
✔ **Predictive Scaling:** Uses machine learning to predict future traffic.  
✔ **Scheduled Scaling:** Adjusts capacity at specific times.  
✔ **Health Monitoring:** Detects failed instances and replaces them.  

### **Creating an Auto Scaling Group (Hands-on Lab)**  
#### **Step 1: Create a Launch Template**  
1. Go to **EC2 > Launch Templates**.  
2. Click **Create Launch Template**.  
3. Select an **AMI**, instance type, and security group.  
4. Click **Create Launch Template**.  

#### **Step 2: Configure Auto Scaling Group**  
1. Navigate to **Auto Scaling Groups > Create Auto Scaling Group**.  
2. Select the **Launch Template** you just created.  
3. Configure the **desired capacity** (e.g., Min: 1, Max: 5).  
4. Set **Scaling Policies** (e.g., scale up if CPU > 60%).  
5. Click **Create Auto Scaling Group**.  

---

## **2.5 Elastic Load Balancing (ELB)**  
### **What is ELB?**  
Elastic Load Balancer **distributes incoming traffic** across multiple EC2 instances, ensuring **high availability and fault tolerance**.

### **Types of Load Balancers**  
🔹 **Application Load Balancer (ALB):** Best for **HTTP/HTTPS applications**.  
🔹 **Network Load Balancer (NLB):** Best for **TCP, UDP, and high-performance workloads**.  
🔹 **Classic Load Balancer (CLB):** Legacy option, used for **simple traffic distribution**.  

### **Hands-on: Configuring an ALB**  
#### **Step 1: Create a Load Balancer**  
1. Go to **EC2 > Load Balancers > Create Load Balancer**.  
2. Select **Application Load Balancer**.  
3. Define **Listeners** (e.g., HTTP/HTTPS).  
4. Assign the **VPC and subnets**.  
5. Create a **Target Group** and register EC2 instances.  

#### **Step 2: Attach to Auto Scaling Group**  
1. Navigate to **Auto Scaling Groups**.  
2. Select the ASG and click **Edit Load Balancing**.  
3. Attach the **Application Load Balancer**.  

✔ **Expected Outcome:** Incoming traffic is now evenly distributed across multiple EC2 instances.

---

## **2.6 Serverless Computing with AWS Lambda**  
### **What is AWS Lambda?**  
AWS Lambda is a **serverless compute service** that runs code in response to events without provisioning or managing servers.

### **Benefits of Lambda**  
✔ **Pay only for execution time (per request).**  
✔ **Automatic scaling** based on demand.  
✔ **Supports multiple programming languages** (Python, Node.js, Java, etc.).  

### **Hands-on: Create a Simple Lambda Function**  
#### **Step 1: Create a Lambda Function**  
1. Go to **AWS Lambda** and click **Create Function**.  
2. Select **Author from Scratch** and choose **Python**.  
3. Define a function name and execution role.  

#### **Step 2: Write a Simple Function**  
```python
def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': 'Hello from AWS Lambda!'
    }
```

✔ **Expected Outcome:** Function runs **without requiring a server**.

---

## **Summary**  
In this chapter, you learned:  
✔ **EC2 instances, AMIs, and instance types.**  
✔ **How to configure Auto Scaling and Elastic Load Balancing.**  
✔ **Introduction to AWS Lambda and serverless computing.**  
✔ **Hands-on deployments for EC2, Auto Scaling, and Load Balancers.**  

---

## **Next Steps**  
👉 Proceed to **Chapter 3: AWS Networking Services**, where you will learn how to configure **VPC, subnets, route tables, and security groups**! 🚀
