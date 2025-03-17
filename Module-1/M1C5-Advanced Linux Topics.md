# **Chapter 5: Advanced Linux Topics**  

## **Introduction**  
Advanced Linux administration involves securing remote access, managing firewalls, optimizing disk usage, and implementing backup strategies. These skills are essential for maintaining a reliable and secure Linux environment.  

In this chapter, we will cover:  
- **SSH configuration for secure remote access**  
- **Firewall management using UFW and Firewalld**  
- **Disk partitioning and file system management**  
- **Backup and recovery strategies**  

---

## **5.1 SSH Configuration**  
Secure Shell (SSH) allows secure remote access to Linux servers. SSH encrypts communication, making it a critical tool for system administrators.  

### **Installing and Enabling SSH**  
#### **Check if SSH is Installed**  
```bash
which ssh
```
If not installed, install OpenSSH:  
- **Ubuntu/Debian:**  
  ```bash
  sudo apt install openssh-server -y
  ```
- **CentOS/RHEL:**  
  ```bash
  sudo yum install openssh-server -y
  ```

#### **Start and Enable SSH Service**  
```bash
sudo systemctl start ssh
sudo systemctl enable ssh
```

#### **Allow SSH Through Firewall**  
- **Ubuntu (UFW):**  
  ```bash
  sudo ufw allow ssh
  ```
- **CentOS (Firewalld):**  
  ```bash
  sudo firewall-cmd --permanent --add-service=ssh
  sudo firewall-cmd --reload
  ```

### **Configuring SSH for Enhanced Security**  
The SSH configuration file is located at `/etc/ssh/sshd_config`.  

#### **Change the Default SSH Port (Optional for Security)**  
Edit the file:  
```bash
sudo nano /etc/ssh/sshd_config
```
Find and modify:  
```bash
Port 2222
PermitRootLogin no
PasswordAuthentication no
```
- `Port 2222` – Changes the default SSH port (use a custom number).  
- `PermitRootLogin no` – Disables direct root login.  
- `PasswordAuthentication no` – Forces key-based authentication.  

Restart SSH service:  
```bash
sudo systemctl restart ssh
```

### **Setting Up SSH Key-Based Authentication**  
Generate an SSH key pair on the client machine:  
```bash
ssh-keygen -t rsa -b 4096
```
Copy the public key to the remote server:  
```bash
ssh-copy-id user@remote-server
```
Now, log in securely:  
```bash
ssh user@remote-server
```

**Hands-on Practice:**  
1. Install and enable SSH on your Linux system.  
2. Change the SSH port and disable root login.  
3. Configure SSH key-based authentication.  

---

## **5.2 Firewall Management**  
Firewalls control incoming and outgoing traffic, providing security by restricting unauthorized access.  

### **Managing Firewalls with UFW (Ubuntu/Debian)**  
Enable UFW:  
```bash
sudo ufw enable
```
Allow specific services:  
```bash
sudo ufw allow 80/tcp     # Allow HTTP
sudo ufw allow 443/tcp    # Allow HTTPS
sudo ufw allow 2222/tcp   # Allow custom SSH port
```
Check firewall status:  
```bash
sudo ufw status
```

### **Managing Firewalls with Firewalld (CentOS/RHEL)**  
Start and enable Firewalld:  
```bash
sudo systemctl start firewalld
sudo systemctl enable firewalld
```
Allow services:  
```bash
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
```
Reload firewall rules:  
```bash
sudo firewall-cmd --reload
```
Check active rules:  
```bash
sudo firewall-cmd --list-all
```

**Hands-on Practice:**  
1. Enable and configure UFW on Ubuntu.  
2. Set up Firewalld rules on CentOS.  
3. Restrict SSH access to a specific IP range.  

---

## **5.3 Disk Management**  
Efficient disk management ensures proper storage allocation and performance optimization.  

### **Viewing Disk Information**  
List available disks and partitions:  
```bash
lsblk
fdisk -l
df -h
```
- `lsblk` – Shows block devices (disks and partitions).  
- `fdisk -l` – Displays partition tables.  
- `df -h` – Reports disk space usage.  

### **Partitioning a New Disk**  
1. **Create a New Partition**  
   ```bash
   sudo fdisk /dev/sdb
   ```
   - Press `n` for a new partition.  
   - Choose primary (`p`) or extended (`e`).  
   - Specify the partition size.  
   - Press `w` to write changes.  

2. **Format the Partition**  
   ```bash
   sudo mkfs.ext4 /dev/sdb1
   ```

3. **Mount the Partition**  
   ```bash
   sudo mkdir /mnt/data
   sudo mount /dev/sdb1 /mnt/data
   ```

4. **Make the Mount Permanent** (Edit `/etc/fstab`)  
   ```bash
   echo "/dev/sdb1 /mnt/data ext4 defaults 0 0" | sudo tee -a /etc/fstab
   ```

### **Resizing a Partition (Using LVM)**  
1. **Extend a Logical Volume**  
   ```bash
   sudo lvextend -L +10G /dev/vg_name/lv_name
   sudo resize2fs /dev/vg_name/lv_name
   ```

2. **Reduce a Logical Volume**  
   ```bash
   sudo resize2fs /dev/vg_name/lv_name 10G
   sudo lvreduce -L 10G /dev/vg_name/lv_name
   ```

**Hands-on Practice:**  
1. Create a new partition, format it, and mount it.  
2. Resize an existing partition using LVM.  
3. Configure automatic disk mounting using `/etc/fstab`.  

---

## **5.4 Backup and Recovery Strategies**  
Data loss prevention is critical for system reliability. Regular backups ensure data safety.  

### **Backup Strategies**  
- **Full Backup:** Copies all files and directories.  
- **Incremental Backup:** Saves changes since the last backup.  
- **Differential Backup:** Stores changes since the last full backup.  

### **Creating Backups Using tar**  
Backup a directory:  
```bash
tar -cvzf backup.tar.gz /home/user/
```
Restore from backup:  
```bash
tar -xvzf backup.tar.gz -C /home/user/
```

### **Automating Backups with Cron Jobs**  
Edit the cron table:  
```bash
crontab -e
```
Schedule a daily backup at 2 AM:  
```bash
0 2 * * * tar -cvzf /backup/home_backup.tar.gz /home/user/
```

### **Using Rsync for Remote Backups**  
Sync files to a remote server:  
```bash
rsync -avz /home/user/ user@backup-server:/backup/
```

### **Restoring from Backups**  
Recover files using rsync:  
```bash
rsync -avz user@backup-server:/backup/ /home/user/
```

**Hands-on Practice:**  
1. Create a tar backup and restore it.  
2. Set up a cron job for automatic backups.  
3. Use rsync to sync files to a remote server.  

---

## **Conclusion**  
In this chapter, we explored advanced Linux topics, including SSH configuration, firewall management, disk partitioning, and backup strategies. These skills are essential for securing and maintaining Linux environments efficiently.  

In the next module, we will dive into **AWS Cloud Technologies**, where we will learn about cloud computing, AWS services, and best practices for cloud infrastructure management.
