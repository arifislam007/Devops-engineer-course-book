# **Chapter 6: AWS Security and Identity Services**  

## **6.1 Introduction to AWS Security and Identity Management**  
Security is a **core pillar** of AWS cloud services. AWS provides various security tools to **control access, monitor activity, and protect resources** from cyber threats.  

### **Key AWS Security Services Covered in This Chapter**  
✔ **AWS Identity and Access Management (IAM):** Manages users, roles, and permissions.  
✔ **AWS Key Management Service (KMS):** Encrypts sensitive data.  
✔ **AWS Shield:** Protects against DDoS attacks.  
✔ **AWS Web Application Firewall (WAF):** Blocks malicious traffic.  
✔ **AWS CloudTrail:** Tracks API activity for auditing.  

---

## **6.2 AWS Identity and Access Management (IAM)**  
### **What is IAM?**  
AWS IAM allows you to **control user access** to AWS services and resources.  

### **IAM Key Concepts**  
| **Component**  | **Description**  |  
|---------------|----------------|  
| **Users** | Individual identities with credentials. |  
| **Groups** | Collection of users with shared permissions. |  
| **Roles** | Temporary access for AWS services or external users. |  
| **Policies** | JSON documents that define permissions. |  

### **Hands-on: Creating an IAM User with Permissions**  
#### **Step 1: Create an IAM User**  
1. Open **AWS Console** → Go to **IAM**.  
2. Click **Users** → **Add User**.  
3. Enter **Username** → Select **Programmatic Access** (for CLI/API).  
4. Attach **AdministratorAccess** policy (for full permissions).  
5. Click **Create User** → Download **Access Key ID & Secret Key**.  

#### **Step 2: Configure AWS CLI with IAM Credentials**  
1. On your local machine, run:  
   ```sh
   aws configure
   ```  
2. Enter **Access Key ID & Secret Key** from IAM.  
3. Verify by listing S3 buckets:  
   ```sh
   aws s3 ls
   ```  

✔ **Outcome:** The IAM user can now interact with AWS services using the CLI.  

---

## **6.3 AWS Key Management Service (KMS)**  
### **What is AWS KMS?**  
AWS KMS is a **fully managed encryption service** that helps encrypt sensitive data using **customer-managed keys (CMKs)**.  

### **Key Features**  
✔ **Data Encryption:** Encrypts data stored in **S3, RDS, EBS, and more**.  
✔ **Key Rotation:** Automatically rotates encryption keys.  
✔ **Access Control:** Integrated with IAM for permission management.  

### **Hands-on: Encrypting an S3 Bucket with KMS**  
#### **Step 1: Create a KMS Key**  
1. Open **AWS Console** → Go to **KMS**.  
2. Click **Create Key** → Select **Symmetric** key.  
3. Add a description (e.g., `"S3 Encryption Key"`).  
4. Assign IAM users who can **use** the key.  
5. Click **Create Key**.  

#### **Step 2: Enable Encryption for an S3 Bucket**  
1. Open **S3 Console** → Select a bucket.  
2. Click **Properties** → Enable **Default Encryption**.  
3. Choose **AWS KMS** and select the key created.  
4. Save changes.  

✔ **Outcome:** All new files uploaded to the S3 bucket are encrypted using **KMS keys**.  

---

## **6.4 AWS Shield – DDoS Protection**  
### **What is AWS Shield?**  
AWS Shield is a **managed Distributed Denial-of-Service (DDoS) protection** service that safeguards applications from attacks.  

### **AWS Shield Plans**  
| **Plan**  | **Features**  |  
|-----------|--------------|  
| **AWS Shield Standard** | Free, protects against common DDoS attacks. |  
| **AWS Shield Advanced** | Paid, real-time attack detection & mitigation. |  

### **Hands-on: Enabling AWS Shield for an Application Load Balancer (ALB)**  
1. Open **AWS Console** → Go to **EC2**.  
2. Click **Load Balancers** → Select an **ALB**.  
3. Navigate to **AWS Shield** → Enable **Shield Advanced**.  
4. Configure **Notifications & Alarms**.  

✔ **Outcome:** The ALB is now protected from **DDoS attacks**.  

---

## **6.5 AWS Web Application Firewall (WAF)**  
### **What is AWS WAF?**  
AWS WAF **filters and blocks malicious web traffic** based on security rules.  

### **Key Features**  
✔ **Prevents SQL Injection & XSS Attacks.**  
✔ **Blocks IPs & Restricts Access Based on Country.**  
✔ **Works with CloudFront, ALB, and API Gateway.**  

### **Hands-on: Creating a WAF Rule to Block Bad Traffic**  
#### **Step 1: Create a Web ACL**  
1. Open **AWS Console** → Go to **AWS WAF**.  
2. Click **Create Web ACL** → Select **CloudFront** or **ALB**.  
3. Define a **Rule** (e.g., Block requests from `Russia` or `China`).  
4. Click **Save** → Attach WAF to the web service.  

✔ **Outcome:** Only allowed traffic can access the application.  

---

## **6.6 AWS CloudTrail – Auditing AWS Activity**  
### **What is AWS CloudTrail?**  
AWS CloudTrail **records API activity** across your AWS account for security auditing.  

### **Key Features**  
✔ **Tracks all AWS API Calls (via Console, SDK, CLI).**  
✔ **Stores Logs in S3 for Analysis.**  
✔ **Works with AWS CloudWatch for Real-time Alerts.**  

### **Hands-on: Enabling CloudTrail for an AWS Account**  
#### **Step 1: Create a CloudTrail**  
1. Open **AWS Console** → Go to **CloudTrail**.  
2. Click **Create Trail** → Enter **Trail Name**.  
3. Select **Management Events** → Enable **Read & Write Logging**.  
4. Choose an **S3 Bucket** for log storage.  
5. Click **Create Trail**.  

#### **Step 2: View CloudTrail Logs**  
1. Open **S3 Bucket** → Locate the log file.  
2. Download and open it to see recorded AWS API activities.  

✔ **Outcome:** You can track who accessed which AWS resources and when.  

---

## **6.7 Summary**  
In this chapter, we covered:  
✔ **IAM:** Managing AWS users, roles, and permissions.  
✔ **KMS:** Encrypting data using customer-managed keys.  
✔ **AWS Shield:** Protecting applications from **DDoS attacks**.  
✔ **AWS WAF:** Blocking malicious web traffic.  
✔ **CloudTrail:** Auditing AWS API activity.  
