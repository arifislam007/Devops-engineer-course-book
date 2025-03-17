# **Chapter 4: System Administration**  

## **Introduction**  
System administration is a fundamental skill for managing Linux environments. It involves installing and managing software, monitoring system performance, and ensuring security and stability. This chapter provides a step-by-step guide on:  
- Package management using `apt` and `yum`  
- Managing system processes  
- Monitoring system performance  

---

## **4.1 Package Management in Linux**  
Linux distributions use package managers to install, update, and remove software efficiently. The most common package managers are:  
- **APT (Advanced Package Tool)** – Used in Debian-based distributions (Ubuntu, Debian).  
- **YUM (Yellowdog Updater, Modified) / DNF** – Used in RHEL-based distributions (CentOS, Fedora).  

### **Using APT in Ubuntu/Debian**  
#### **Updating Package Repositories**  
```bash
sudo apt update
```
#### **Upgrading Installed Packages**  
```bash
sudo apt upgrade -y
```
#### **Installing a Package**  
```bash
sudo apt install nginx -y
```
#### **Removing a Package**  
```bash
sudo apt remove nginx -y
```
#### **Searching for a Package**  
```bash
apt search apache2
```

### **Using YUM in CentOS/RHEL**  
#### **Updating Package Repositories**  
```bash
sudo yum update -y
```
#### **Installing a Package**  
```bash
sudo yum install httpd -y
```
#### **Removing a Package**  
```bash
sudo yum remove httpd -y
```
#### **Checking Installed Packages**  
```bash
yum list installed | grep nginx
```

**Hands-on Practice:**  
1. Install and remove a package using APT and YUM.  
2. Search for available versions of `nginx` in the repository.  
3. Update all installed packages on your system.  

---

## **4.2 Managing System Processes**  
Processes are programs that are currently running on the system. Linux provides tools to manage and monitor processes.  

### **Viewing Running Processes**  
#### **Using `ps` Command**  
```bash
ps aux
```
- `a` – Shows processes from all users  
- `u` – Displays user information  
- `x` – Lists background processes  

#### **Using `top` Command**  
```bash
top
```
- Displays real-time system resource usage  
- Press `q` to exit  

#### **Using `htop` (Enhanced `top`)**  
```bash
sudo apt install htop -y
htop
```

### **Managing Processes**  
#### **Killing a Process**  
Find the process ID (PID) using `ps` or `top`, then:  
```bash
kill <PID>
```
Force kill:  
```bash
kill -9 <PID>
```

#### **Stopping and Restarting Services**  
```bash
sudo systemctl stop nginx
sudo systemctl start nginx
sudo systemctl restart nginx
```

**Hands-on Practice:**  
1. List all running processes using `ps` and `top`.  
2. Find and kill a process by its PID.  
3. Stop and restart a service like `nginx`.  

---

## **4.3 System Monitoring Tools**  
Monitoring helps maintain system performance and detect issues.  

### **Checking System Resource Usage**  
#### **CPU and Memory Usage**  
```bash
free -m
vmstat 5 10
```
- `free -m` – Displays memory usage in MB  
- `vmstat 5 10` – Displays CPU and memory statistics every 5 seconds for 10 times  

#### **Disk Usage**  
```bash
df -h
du -sh /var/log/
```
- `df -h` – Shows disk space usage  
- `du -sh /var/log/` – Displays disk usage of a directory  

#### **Network Monitoring**  
```bash
ifconfig
netstat -tulnp
```
- `ifconfig` – Displays network interfaces  
- `netstat -tulnp` – Lists open network ports  

### **Logging System Events**  
#### **Checking System Logs**  
```bash
sudo journalctl -xe
tail -f /var/log/syslog
```
- `journalctl -xe` – Shows systemd logs  
- `tail -f /var/log/syslog` – Monitors system logs in real-time  

**Hands-on Practice:**  
1. Check CPU and memory usage using `free -m`.  
2. Find disk usage of the `/var` directory.  
3. List open network ports using `netstat`.  

---

## **Conclusion**  
In this chapter, we covered essential system administration skills, including package management, process management, and system monitoring. These skills are crucial for troubleshooting and maintaining a stable Linux environment.  

In the next chapter, we will explore **Advanced Linux Topics**, including SSH configuration, firewall management, and backup strategies.
