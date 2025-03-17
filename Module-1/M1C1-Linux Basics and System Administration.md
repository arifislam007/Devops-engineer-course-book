# **Module 1: Linux Fundamentals**  
## **Chapter 1: Linux Basics and System Administration**  

### **Introduction to Linux**  
Linux is an open-source, Unix-like operating system that powers everything from smartphones to supercomputers. Unlike proprietary operating systems like Windows and macOS, Linux is free and allows users to modify and distribute it as they see fit. It is widely used in server environments, cloud computing, DevOps, cybersecurity, and embedded systems.  

This chapter will introduce you to the fundamental concepts of Linux, including its history, architecture, installation process, and essential system administration tasks.  

---

## **1.1 History and Evolution of Linux**  
### **Origins of Unix and the Birth of Linux**  
Before Linux, the **Unix operating system** was developed in the late 1960s at Bell Labs by Ken Thompson and Dennis Ritchie. Unix became popular for its portability, multitasking, and multi-user capabilities. However, it was mostly proprietary, meaning organizations had to purchase licenses to use it.  

In 1991, **Linus Torvalds**, a Finnish computer science student, started a personal project to create a Unix-like kernel. This project became **Linux**, and with the help of a global open-source community, it rapidly grew into one of the most widely used operating systems today.  

### **Key Milestones in Linux Development**  
- **1991**: Linus Torvalds released the first Linux kernel version 0.01.  
- **1992**: The Linux kernel was licensed under the GNU General Public License (GPL), making it freely available for modification and distribution.  
- **2000s**: Linux gained popularity in enterprise environments with distributions like Red Hat, Debian, and Ubuntu.  
- **Present Day**: Linux powers **servers, cloud platforms (AWS, Google Cloud, Azure), IoT devices, Android smartphones, and supercomputers**.  

---

## **1.2 Understanding Linux Distributions**  
A **Linux distribution (distro)** is a complete operating system that includes the **Linux kernel** along with system utilities, libraries, and software packages. Different distributions are designed for different purposes, such as desktop computing, server management, and security.  

### **Popular Linux Distributions**  
- **Ubuntu**: Beginner-friendly, widely used for desktops and cloud computing.  
- **CentOS/Rocky Linux**: Used in enterprise environments and server applications.  
- **Debian**: Stable and community-driven; the foundation for Ubuntu.  
- **Red Hat Enterprise Linux (RHEL)**: A commercial Linux distribution used in enterprise and cloud environments.  
- **Arch Linux**: Lightweight, rolling-release, and highly customizable for advanced users.  

| **Feature**        | **Ubuntu** | **CentOS/Rocky Linux** | **Debian** | **RHEL** |
|--------------------|-----------|----------------------|----------|---------|
| **Ease of Use**   | High      | Moderate            | Moderate | Moderate |
| **Package Manager** | APT       | YUM/DNF             | APT      | YUM/DNF |
| **Best For**      | Beginners, cloud, servers | Enterprise, stability | Developers, stability | Enterprise, commercial support |

---

## **1.3 Installing Linux (Ubuntu & CentOS/Rocky Linux)**  
### **System Requirements for Linux Installation**  
Before installing Linux, ensure that your system meets the minimum requirements:  
- **Processor**: 64-bit x86 or ARM  
- **RAM**: At least 2GB (4GB+ recommended for better performance)  
- **Storage**: At least 20GB free disk space  
- **Internet Connection**: Required for downloading packages and updates  

### **Installation Methods**  
Linux can be installed using:  
1. **Bare-metal installation** (on a physical machine).  
2. **Virtual Machine (VM)** using software like VirtualBox, VMware, or KVM.  
3. **Cloud Instances** on AWS, Google Cloud, or Azure.  

### **Step-by-Step Guide to Installing Ubuntu**  
#### **Method 1: Installing Ubuntu on a Physical Machine**  
1. **Download Ubuntu ISO** from [Ubuntu’s official website](https://ubuntu.com/download).  
2. **Create a Bootable USB Drive** using **Rufus (Windows)** or **dd command (Linux/Mac)**.  
3. **Boot from USB Drive**: Restart your computer and boot into the Ubuntu installation USB.  
4. **Select Installation Type**: Choose **"Install Ubuntu"** and follow the on-screen instructions.  
5. **Partitioning**: Choose **automatic partitioning** for beginners or **manual partitioning** for custom setups.  
6. **Set Up User Credentials**: Create a username and password.  
7. **Finish Installation**: Restart the system, remove the USB drive, and boot into your new Ubuntu system.  

#### **Method 2: Installing Ubuntu on a Virtual Machine**  
1. **Install VirtualBox or VMware Workstation.**  
2. **Create a New Virtual Machine.**  
3. **Assign System Resources**: Allocate at least **2GB RAM and 20GB storage**.  
4. **Attach Ubuntu ISO** and start the VM.  
5. **Follow the same installation steps as the physical machine setup.**  

### **Step-by-Step Guide to Installing CentOS/Rocky Linux**  
1. **Download the CentOS or Rocky Linux ISO** from their official website.  
2. **Create a Bootable USB Drive** using Rufus or the `dd` command.  
3. **Boot from USB Drive** and select **"Install CentOS/Rocky Linux"**.  
4. **Choose Installation Destination** and configure partitioning.  
5. **Set Up Root Password and User Account.**  
6. **Complete Installation and Reboot.**  

After installation, you can access Linux via the **Graphical User Interface (GUI)** or **Command Line Interface (CLI)** using a terminal.  

---

## **1.4 Understanding the Linux File System**  
The Linux file system follows a hierarchical structure where all files and directories stem from the **root directory (`/`)**.  

### **Common Linux Directories**  
| **Directory** | **Description** |
|-------------|----------------|
| `/`         | Root directory (top-level directory). |
| `/home`     | User home directories. |
| `/etc`      | System configuration files. |
| `/var`      | Log files and variable data. |
| `/usr`      | User applications and libraries. |
| `/bin`      | Essential binary executables. |
| `/sbin`     | System binaries (used by the root user). |

---

## **1.5 Essential Linux System Administration Commands**  
### **User and Group Management**
- `whoami` – Check the current user.  
- `adduser <username>` – Add a new user.  
- `passwd <username>` – Change a user's password.  
- `groupadd <groupname>` – Create a new group.  
- `usermod -aG <group> <username>` – Add a user to a group.  
- `deluser <username>` – Delete a user.  

### **File and Directory Management**
- `ls -l` – List files with details.  
- `cd <directory>` – Change directory.  
- `mkdir <directory>` – Create a new directory.  
- `rm -rf <directory>` – Remove a directory.  

### **Process Management**
- `ps aux` – List active processes.  
- `kill <PID>` – Terminate a process.  
- `htop` – Interactive process viewer.  

### **Networking Basics**
- `ip a` – Display IP addresses.  
- `ping google.com` – Check network connectivity.  
- `netstat -tulnp` – View open network ports.  

---

## **Conclusion**  
This chapter introduced the fundamental concepts of Linux, including its history, distributions, installation process, and essential system administration tasks. Mastering these basics will prepare you for advanced topics such as scripting, automation, and cloud integration in later modules.  

In the next chapter, we will dive deeper into **Linux File Systems and Navigation**, where you will learn about file permissions, directory structures, and managing files efficiently using the command line.
