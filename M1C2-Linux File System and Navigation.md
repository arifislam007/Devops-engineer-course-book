# **Chapter 2: Linux File System and Navigation**  

## **Introduction**  
The Linux file system is a well-organized, hierarchical structure that follows a standard directory layout. Understanding how files and directories are organized and managed is essential for system administration, automation, and troubleshooting. In this chapter, we will cover:  
- The Linux directory structure  
- File and directory management commands  
- Understanding file permissions and ownership  
- Hands-on examples for file and directory navigation  

---

## **2.1 Linux File System Structure**  
Unlike Windows, which uses drive letters like **C:\**, Linux has a **single-rooted file system** that starts with the root directory (`/`). Every file and directory is placed within this structure.  

### **Common Directories in Linux**  
| **Directory**  | **Purpose**  |
|--------------|------------|
| `/`          | Root directory (all files and folders originate from here). |
| `/home`      | Stores user home directories (`/home/user`). |
| `/etc`       | Configuration files for system and applications. |
| `/var`       | Log files, caches, and variable data. |
| `/usr`       | Installed user programs and libraries. |
| `/bin`       | Essential command binaries (e.g., `ls`, `cp`, `mv`). |
| `/sbin`      | System binaries (e.g., `shutdown`, `reboot`). |
| `/tmp`       | Temporary files, deleted on reboot. |
| `/dev`       | Device files (e.g., `/dev/sda` for hard drives). |
| `/mnt`       | Mount point for external drives. |

### **Navigating the Linux File System**
Linux uses a **tree-like hierarchical structure**, where directories can contain subdirectories and files.  

#### **Absolute vs. Relative Paths**
- **Absolute Path**: Specifies the complete location starting from `/`.  
  - Example: `/home/user/Documents/file.txt`  
- **Relative Path**: Specifies location relative to the current directory.  
  - Example: `Documents/file.txt` (assuming you are in `/home/user/`)

---

## **2.2 File and Directory Management Commands**  
### **Navigating Directories**  
| **Command**  | **Description** |
|------------|--------------|
| `pwd`      | Print the current working directory. |
| `cd /path` | Change to a specific directory. |
| `cd ..`    | Move up one directory level. |
| `cd -`     | Switch back to the previous directory. |
| `ls`       | List directory contents. |
| `ls -l`    | List with detailed information (permissions, owner, size). |
| `ls -a`    | Show hidden files. |

#### **Hands-on Example**  
```bash
cd /home/user/Documents  # Navigate to Documents directory
pwd                      # Confirm current location
ls -l                    # List files with details
```

### **Creating and Managing Directories**  
| **Command**         | **Description** |
|--------------------|--------------|
| `mkdir mydir`     | Create a directory named `mydir`. |
| `mkdir -p dir1/dir2` | Create nested directories (`dir1` inside `dir2`). |
| `rmdir mydir`     | Remove an empty directory. |
| `rm -r mydir`     | Remove a directory and all its contents. |

#### **Hands-on Example**  
```bash
mkdir projects                 # Create a directory
mkdir -p projects/devops        # Create nested directories
ls -l                           # Verify directory creation
rm -r projects                  # Delete directory
```

### **Creating and Managing Files**  
| **Command**         | **Description** |
|--------------------|--------------|
| `touch file.txt`   | Create an empty file. |
| `cat file.txt`     | Display file contents. |
| `echo "Hello" > file.txt` | Create a file with text. |
| `cp file.txt /tmp/` | Copy file to another directory. |
| `mv file.txt newname.txt` | Rename or move a file. |
| `rm file.txt`     | Delete a file. |

#### **Hands-on Example**  
```bash
touch notes.txt               # Create a file
echo "This is a test" > notes.txt  # Add content
cat notes.txt                 # View content
mv notes.txt backup.txt       # Rename the file
cp backup.txt /tmp/           # Copy to another directory
rm backup.txt                 # Delete file
```

---

## **2.3 Understanding File Permissions and Ownership**  
Linux file permissions define who can read, write, or execute files and directories.  

### **File Permission Structure**  
Each file and directory has **three types of permissions** for three different user categories:  
```bash
-rwxr-xr-- 1 user group 1024 Mar 10 12:00 file.txt
```
- `r` (Read) – Allows viewing file contents.  
- `w` (Write) – Allows modifying the file.  
- `x` (Execute) – Allows executing the file as a program.  
- **Owner (`user`)** – The user who created the file.  
- **Group (`group`)** – A set of users who share permissions.  
- **Others (`---`)** – Everyone else on the system.  

| **Permission** | **Symbol** | **Octal Value** |
|--------------|---------|--------------|
| Read         | `r`     | 4            |
| Write        | `w`     | 2            |
| Execute      | `x`     | 1            |

### **Changing File Permissions**
| **Command**               | **Description** |
|--------------------------|--------------|
| `chmod 755 file.txt`     | Set **rwxr-xr-x** permissions. |
| `chmod u+x script.sh`    | Give execute permission to owner. |
| `chmod g-w file.txt`     | Remove write permission for the group. |

#### **Hands-on Example**  
```bash
touch script.sh              # Create a file
chmod +x script.sh           # Make it executable
ls -l script.sh              # Check new permissions
```

### **Changing File Ownership**
| **Command**                 | **Description** |
|----------------------------|--------------|
| `chown user file.txt`      | Change ownership to `user`. |
| `chown user:group file.txt` | Change both user and group ownership. |

#### **Hands-on Example**  
```bash
sudo chown john file.txt      # Change owner to 'john'
sudo chown john:devops file.txt  # Change owner and group
```

---

## **2.4 Finding Files and Directories**  
| **Command** | **Description** |
|------------|--------------|
| `find / -name "file.txt"` | Search for a file by name. |
| `locate file.txt` | Quickly locate files (uses a database). |
| `grep "error" /var/log/syslog` | Search for "error" in a log file. |

#### **Hands-on Example**  
```bash
find /home -name "*.txt"    # Find all text files in /home
grep "root" /etc/passwd     # Find lines containing 'root' in a file
```

---

## **Conclusion**  
In this chapter, we explored the Linux file system, directory structure, file management commands, and file permissions. Mastering these fundamentals is crucial for efficient system administration and automation tasks.  

In the next chapter, we will dive into **Shell Scripting**, where we will learn how to automate tasks using Bash scripts.
