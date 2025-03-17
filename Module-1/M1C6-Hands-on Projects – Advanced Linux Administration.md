# **Chapter 6: Hands-on Projects – Advanced Linux Administration**  

## **Introduction**  
Hands-on experience is crucial for mastering Linux system administration. This chapter provides **practical projects** based on the advanced Linux topics covered in the previous chapter. Each project includes a detailed **objective, step-by-step implementation, and expected outcome**.  

These projects will reinforce your understanding of:  
✅ **SSH security and key-based authentication**  
✅ **Firewall configuration (UFW and Firewalld)**  
✅ **Disk partitioning and file system management**  
✅ **Backup and recovery automation**  

---

## **Project 1: Secure Remote Access with SSH Key-Based Authentication**  

### **Objective**  
🔹 Configure a Linux system for secure remote SSH access using key-based authentication.  

### **Requirements**  
🟢 Two Linux machines (one as a server, one as a client).  
🟢 A user account with `sudo` privileges.  

### **Implementation Steps**  
#### **Step 1: Install and Start SSH Service**  
On the server:  
```bash
sudo apt install openssh-server -y   # Ubuntu
sudo yum install openssh-server -y   # CentOS
sudo systemctl start ssh
sudo systemctl enable ssh
```

#### **Step 2: Generate SSH Key on the Client Machine**  
```bash
ssh-keygen -t rsa -b 4096
```
Press **Enter** for default locations.

#### **Step 3: Copy Public Key to the Server**  
```bash
ssh-copy-id user@server-ip
```
Alternatively, copy manually:  
```bash
scp ~/.ssh/id_rsa.pub user@server-ip:~/
ssh user@server-ip 'mkdir -p ~/.ssh && cat id_rsa.pub >> ~/.ssh/authorized_keys'
```

#### **Step 4: Disable Password Authentication on Server**  
Edit SSH config:  
```bash
sudo nano /etc/ssh/sshd_config
```
Modify these lines:  
```
PasswordAuthentication no
PermitRootLogin no
```
Restart SSH service:  
```bash
sudo systemctl restart ssh
```

#### **Step 5: Connect Securely from the Client**  
```bash
ssh user@server-ip
```

### **Expected Outcome**  
✅ You can log in to the server **without entering a password**.  
✅ Password-based authentication is disabled for better security.  

---

## **Project 2: Firewall Hardening for a Web Server**  

### **Objective**  
🔹 Configure firewall rules to allow only SSH, HTTP (80), and HTTPS (443) traffic.  

### **Requirements**  
🟢 A Linux server with `UFW` (Ubuntu) or `Firewalld` (CentOS).  
🟢 Apache/Nginx installed.  

### **Implementation Steps**  

#### **Step 1: Enable and Configure UFW (Ubuntu)**  
```bash
sudo ufw enable
sudo ufw allow 22/tcp   # SSH
sudo ufw allow 80/tcp   # HTTP
sudo ufw allow 443/tcp  # HTTPS
sudo ufw deny 23        # Block Telnet
sudo ufw status
```

#### **Step 2: Enable and Configure Firewalld (CentOS/RHEL)**  
```bash
sudo systemctl start firewalld
sudo systemctl enable firewalld
sudo firewall-cmd --permanent --add-service=ssh
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
sudo firewall-cmd --reload
sudo firewall-cmd --list-all
```

#### **Step 3: Test Firewall Rules**  
Try accessing the server using:  
✅ `curl http://server-ip` (should work)  
✅ `telnet server-ip 23` (should fail)  

### **Expected Outcome**  
✅ Only SSH, HTTP, and HTTPS are accessible.  
✅ Other services are blocked for enhanced security.  

---

## **Project 3: Disk Partitioning and Automatic Mounting**  

### **Objective**  
🔹 Add a new disk, create a partition, format it, and set up **permanent mounting**.  

### **Requirements**  
🟢 A new disk (`/dev/sdb`).  
🟢 Root or `sudo` access.  

### **Implementation Steps**  

#### **Step 1: Identify Available Disks**  
```bash
lsblk
fdisk -l
```

#### **Step 2: Create a Partition**  
```bash
sudo fdisk /dev/sdb
```
- Press **n** (new partition).  
- Select primary partition **(p)**.  
- Choose default size (or specify).  
- Press **w** to save and exit.  

#### **Step 3: Format the Partition**  
```bash
sudo mkfs.ext4 /dev/sdb1
```

#### **Step 4: Create a Mount Point and Mount the Partition**  
```bash
sudo mkdir /mnt/data
sudo mount /dev/sdb1 /mnt/data
df -h   # Verify mounting
```

#### **Step 5: Make the Mount Permanent in `/etc/fstab`**  
Add this line:  
```
/dev/sdb1  /mnt/data  ext4  defaults  0  0
```
Apply changes:  
```bash
sudo mount -a
```

### **Expected Outcome**  
✅ The new disk is partitioned, formatted, and mounted automatically on reboot.  

---

## **Project 4: Automating Backups Using Cron and Rsync**  

### **Objective**  
🔹 Automate **daily backups** of `/home/user/` to `/backup/` using cron jobs.  

### **Requirements**  
🟢 A Linux system with `tar` and `rsync` installed.  
🟢 Root or `sudo` privileges.  

### **Implementation Steps**  

#### **Step 1: Create a Backup Script**  
```bash
sudo nano /usr/local/bin/backup.sh
```
Add:  
```bash
#!/bin/bash
tar -czf /backup/home_backup_$(date +%F).tar.gz /home/user/
```
Save and exit. Make it executable:  
```bash
sudo chmod +x /usr/local/bin/backup.sh
```

#### **Step 2: Schedule the Script in Crontab**  
```bash
crontab -e
```
Add:  
```
0 2 * * * /usr/local/bin/backup.sh
```
(Backup runs at **2 AM daily**).  

#### **Step 3: Use Rsync for Remote Backups**  
```bash
rsync -avz /backup/ user@remote-server:/backup/
```

### **Expected Outcome**  
✅ Automated daily backups with timestamps.  
✅ Files safely copied to a remote server.  

---

## **Conclusion**  
These **hands-on projects** reinforce real-world Linux system administration. By completing them, you will:  
✅ Improve your **SSH security**  
✅ Configure **firewalls** to allow only necessary traffic  
✅ Master **disk management and partitioning**  
✅ Implement **automated backups and disaster recovery**  

### **Next Steps**  
🔹 Practice these tasks in a **virtual lab** (e.g., VirtualBox, AWS EC2).  
🔹 Apply them in **real-world Linux server environments**.  
🔹 Proceed to **AWS Cloud Technologies** in the next module. 🚀
