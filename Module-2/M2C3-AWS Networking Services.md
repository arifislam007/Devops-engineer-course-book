# **Chapter 3: AWS Networking Services**  

## **3.1 Introduction to AWS Networking**  
AWS provides **highly scalable, secure, and flexible networking** services that allow users to design cloud infrastructure with **customized network topologies**.  

### **Key AWS Networking Services**  
🔹 **Amazon VPC (Virtual Private Cloud):** Isolated cloud network for resources.  
🔹 **Subnets:** Segmentation of a VPC for better resource organization.  
🔹 **Internet Gateway (IGW):** Provides internet access to instances in a VPC.  
🔹 **NAT Gateway:** Allows private instances to access the internet securely.  
🔹 **Route 53:** AWS-managed DNS service for domain name resolution.  
🔹 **CloudFront:** AWS CDN service to accelerate content delivery.  

---

## **3.2 Virtual Private Cloud (VPC)**  
### **What is a VPC?**  
A **Virtual Private Cloud (VPC)** is an **isolated** section of AWS, where you can launch AWS resources inside a **custom IP range**.

### **VPC Components**  
✔ **CIDR Block:** IP address range (e.g., 10.0.0.0/16).  
✔ **Subnets:** Divide VPC into smaller networks (Public & Private).  
✔ **Route Tables:** Define how traffic flows within the VPC.  
✔ **Internet Gateway (IGW):** Enables public internet access.  
✔ **NAT Gateway:** Allows private instances to access the internet.  
✔ **Security Groups:** Instance-level firewall for inbound/outbound rules.  
✔ **Network ACLs:** Subnet-level firewall for traffic filtering.  

### **Creating a Custom VPC (Hands-on Lab)**  
#### **Step 1: Create a VPC**  
1. Navigate to **AWS Console > VPC > Create VPC**.  
2. Provide a name (e.g., "MyVPC") and **CIDR block (10.0.0.0/16)**.  
3. Click **Create VPC**.  

#### **Step 2: Create Public and Private Subnets**  
1. Navigate to **Subnets > Create Subnet**.  
2. Choose **MyVPC** and define:  
   - **Public Subnet:** 10.0.1.0/24  
   - **Private Subnet:** 10.0.2.0/24  
3. Click **Create Subnet**.  

#### **Step 3: Attach an Internet Gateway (IGW)**  
1. Go to **Internet Gateways > Create IGW**.  
2. Attach IGW to **MyVPC**.  
3. Modify **Route Table** to add **0.0.0.0/0 → IGW** (for internet access).  

✔ **Outcome:** The public subnet has internet access, while the private subnet remains isolated.

---

## **3.3 Subnets and Routing in AWS**  
### **Public vs. Private Subnets**  
| Feature | Public Subnet | Private Subnet |  
|---------|--------------|--------------|  
| Internet Access | Yes (via IGW) | No |  
| Route Table | 0.0.0.0/0 → IGW | No direct internet route |  
| Use Cases | Web servers, Bastion Hosts | Databases, Application Servers |  

### **Configuring a NAT Gateway for Private Subnet**  
1. **Go to AWS Console > NAT Gateway > Create NAT Gateway**.  
2. **Attach it to the Public Subnet**.  
3. **Update Private Subnet Route Table:**  
   - **0.0.0.0/0 → NAT Gateway** (Allows outbound internet access).  

✔ **Outcome:** Private subnet instances can access the internet for updates but are **not directly accessible** from the internet.

---

## **3.4 Route 53 - AWS DNS Service**  
### **What is Route 53?**  
Route 53 is a **highly available and scalable** **Domain Name System (DNS)** service by AWS. It translates domain names into IP addresses.

### **Key Features**  
✔ **Domain Registration** – Buy and manage domain names.  
✔ **DNS Resolution** – Convert domain names into IP addresses.  
✔ **Traffic Routing** – Control how users reach applications.  
✔ **Health Checks & Failover** – Route traffic away from unhealthy instances.  

### **Configuring a Custom Domain in Route 53 (Hands-on Lab)**  
#### **Step 1: Register a Domain**  
1. Go to **Route 53 > Register Domain**.  
2. Choose a domain name (e.g., `mywebsite.com`).  
3. Complete registration and verify via email.  

#### **Step 2: Create a Hosted Zone**  
1. Navigate to **Route 53 > Hosted Zones > Create Hosted Zone**.  
2. Add **record sets** (e.g., A record pointing to an EC2 IP).  

✔ **Outcome:** Your domain is now mapped to AWS resources.

---

## **3.5 AWS CloudFront - Content Delivery Network (CDN)**  
### **What is CloudFront?**  
AWS CloudFront is a **Content Delivery Network (CDN)** that accelerates the delivery of web content by caching it at **Edge Locations** worldwide.

### **Key Features**  
✔ **Global Edge Locations:** Content cached at locations closest to users.  
✔ **Improves Performance:** Reduces latency for end users.  
✔ **Security:** Integrated with AWS Shield & Web Application Firewall (WAF).  
✔ **Supports HTTP & HTTPS:** Can deliver dynamic and static content.  

### **Configuring CloudFront for a Website (Hands-on Lab)**  
#### **Step 1: Create a CloudFront Distribution**  
1. Go to **AWS Console > CloudFront > Create Distribution**.  
2. Select **Origin Domain Name** (e.g., an S3 bucket or EC2).  
3. Set **Default Root Object** (e.g., `index.html`).  
4. Enable **HTTPS using SSL/TLS**.  
5. Click **Create Distribution**.  

✔ **Outcome:** Your website is now delivered through **CloudFront’s global CDN**, improving speed and security.

---

## **3.6 Summary**  
In this chapter, we explored:  
✔ **VPC, Subnets, Route Tables, and Internet/NAT Gateways**.  
✔ **How to configure Route 53 for domain management**.  
✔ **CloudFront CDN for accelerating content delivery**.  
✔ **Hands-on labs for setting up AWS networking services**.  

