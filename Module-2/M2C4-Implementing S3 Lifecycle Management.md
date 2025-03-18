# **Chapter 4: AWS Storage Services**  

## **4.1 Introduction to AWS Storage**  
AWS provides a variety of **scalable and secure** storage solutions for different use cases. The three primary storage services we will focus on are:  
- **Amazon S3 (Simple Storage Service):** Object storage for storing and retrieving data.  
- **Amazon EBS (Elastic Block Store):** Block storage for EC2 instances.  
- **Amazon Glacier & S3 Glacier:** Low-cost archival storage for long-term data retention.  

Each of these services serves different needs, from hosting static websites to providing high-performance storage for applications.  

---

## **4.2 Amazon S3 – Object Storage Service**  
### **What is Amazon S3?**  
Amazon S3 is a **fully managed, scalable, and highly durable** object storage service used for **storing any type of data**, such as images, videos, backups, and static web content.

### **Key Features**  
✔ **Scalability:** Stores unlimited data with automatic scaling.  
✔ **Durability & Availability:** 99.999999999% (11 9’s) durability.  
✔ **Storage Classes:** Optimize costs with different pricing tiers.  
✔ **Security & Access Control:** IAM policies, bucket policies, and encryption.  
✔ **Static Website Hosting:** Serve static websites directly from an S3 bucket.  
✔ **Lifecycle Management:** Automate data movement between storage classes.  

### **Hands-on: Creating an S3 Bucket**  
#### **Step 1: Create a Bucket**  
1. Go to **AWS Console > S3 > Create Bucket**.  
2. Enter a **unique bucket name** (e.g., `my-storage-bucket`).  
3. Choose an **AWS region** (closest to your users).  
4. Enable/disable **public access** based on security needs.  
5. Click **Create Bucket**.  

#### **Step 2: Upload an Object**  
1. Open the bucket and click **Upload**.  
2. Select a file (e.g., `image.jpg`) and click **Upload**.  

---

## **4.3 Amazon EBS – Block Storage for EC2**  
### **What is Amazon EBS?**  
Amazon Elastic Block Store (EBS) is **persistent block storage** used with **EC2 instances**. Unlike S3, which stores files as objects, EBS provides **disk-like volumes** that can be attached to EC2 instances.

### **Key Features**  
✔ **Performance:** High-speed storage for databases and applications.  
✔ **Persistent Storage:** Data is retained even after EC2 instances stop.  
✔ **Snapshots:** Backup volumes with **EBS snapshots** stored in S3.  
✔ **Encryption:** Secure data with AWS Key Management Service (KMS).  

### **Hands-on: Creating and Attaching an EBS Volume**  
#### **Step 1: Create an EBS Volume**  
1. Navigate to **AWS Console > EC2 > Elastic Block Store > Create Volume**.  
2. Choose a **size** (e.g., 20GB) and a **type** (e.g., gp3 for general SSD).  
3. Select the **availability zone** matching your EC2 instance.  
4. Click **Create Volume**.  

#### **Step 2: Attach Volume to an EC2 Instance**  
1. Go to **EC2 > Volumes**, select the created volume.  
2. Click **Actions > Attach Volume**.  
3. Choose an **EC2 instance** and confirm the attachment.  

#### **Step 3: Mount the Volume in Linux**  
1. SSH into the EC2 instance and list available disks:  
   ```sh
   lsblk
   ```  
2. Format and mount the volume:  
   ```sh
   sudo mkfs -t ext4 /dev/xvdf  
   sudo mkdir /data  
   sudo mount /dev/xvdf /data  
   ```  

✔ **Outcome:** The EBS volume is now ready for use as additional storage.

---

## **4.4 Amazon Glacier & S3 Glacier – Archival Storage**  
### **What is Glacier?**  
Amazon S3 Glacier is a **low-cost storage solution** designed for long-term archival storage. It is ideal for storing **data that is rarely accessed**, such as compliance records and backups.

### **Key Features**  
✔ **Extremely Low Cost:** Cheaper than S3 standard storage.  
✔ **Data Retrieval Options:** Instant, Expedited, Standard, and Bulk.  
✔ **Highly Secure:** Supports encryption and access control policies.  

### **Glacier vs. S3 Standard Storage**  
| Feature | Amazon S3 | Amazon Glacier |  
|---------|------------|----------------|  
| Use Case | Frequently accessed data | Long-term archival storage |  
| Retrieval Time | Instant | Minutes to hours |  
| Cost | Higher | Lower |  
| Lifecycle Management | Moves objects between storage classes | Designed for long-term retention |  

---

## **4.5 Setting Up a Static Website on S3**  
AWS S3 allows users to host **static websites** (HTML, CSS, JavaScript) directly from an S3 bucket.

### **Hands-on: Deploying a Static Website on S3**  
#### **Step 1: Enable Static Website Hosting**  
1. Go to **S3 Console > Select Bucket > Properties**.  
2. Scroll to **Static website hosting** and click **Edit**.  
3. Select **Enable** and set the **index document** (e.g., `index.html`).  
4. Click **Save Changes**.  

#### **Step 2: Upload Website Files**  
1. Upload `index.html` and any assets (CSS, images, JS).  
2. Set bucket permissions to **public-read** (or use CloudFront for security).  

#### **Step 3: Test the Website**  
1. Copy the **bucket website endpoint** (e.g., `http://my-bucket.s3-website-us-east-1.amazonaws.com`).  
2. Open in a browser to verify.  

✔ **Outcome:** Your website is now live using AWS S3 as the hosting backend.

---

## **4.6 Implementing S3 Lifecycle Management**  
To optimize costs, AWS S3 allows **lifecycle policies** to automatically transition objects between different storage classes.

### **Configuring Lifecycle Rules (Hands-on Lab)**  
#### **Step 1: Create a Lifecycle Rule**  
1. Navigate to **S3 Console > Select Bucket > Management > Lifecycle Rules**.  
2. Click **Create Rule** and define:  
   - Move objects to **S3 Glacier after 30 days**.  
   - Delete objects **after 365 days**.  
3. Save and activate the rule.  

✔ **Outcome:** Data storage costs are reduced by **automatically moving less accessed files** to cheaper storage tiers.

---

## **4.7 Summary**  
In this chapter, we covered:  
✔ **Amazon S3:** Object storage for scalable data storage.  
✔ **Amazon EBS:** Block storage for EC2 instances.  
✔ **Amazon Glacier:** Low-cost archival storage for long-term backups.  
✔ **Static Website Hosting:** Hosting simple websites using S3.  
✔ **Lifecycle Management:** Automating data movement to save costs.  

---

## **Next Steps**  
👉 Proceed to **Chapter 5: AWS Database Services**, where we explore **RDS, DynamoDB, and Aurora** for database management in AWS! 🚀
