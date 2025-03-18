# **Chapter 1: Version Control**  

## **Introduction to Version Control**  
Version control is a system that helps track changes to code, documents, and files over time. It allows multiple developers to collaborate, maintain a history of changes, and revert to previous versions if needed.  

### **Types of Version Control Systems (VCS)**  
1. **Local Version Control** – Stores file changes on a local machine (e.g., RCS).  
2. **Centralized Version Control (CVCS)** – Uses a central server to track changes (e.g., SVN).  
3. **Distributed Version Control (DVCS)** – Each user has a complete copy of the repository (e.g., Git).  

### **Why Git?**  
Git is the most widely used **Distributed Version Control System (DVCS)** due to its:  
✔ Speed and efficiency.  
✔ Branching and merging capabilities.  
✔ Offline work support.  
✔ Strong community and integration with CI/CD pipelines.  

---

## **Getting Started with Git**  

### **Installing Git**  
To install Git on Linux, use:  
```bash
sudo apt update && sudo apt install git -y  # Ubuntu/Debian
sudo yum install git -y                     # CentOS/RHEL
```
Verify the installation:  
```bash
git --version
```  

### **Basic Git Configuration**  
Set up your name and email for commits:  
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```  
Check the configuration:  
```bash
git config --list
```

---

## **Git Repository Management**  

### **Initializing a Repository**  
Create a new Git repository:  
```bash
git init
```  
Clone an existing repository from GitHub/GitLab:  
```bash
git clone https://github.com/user/repo.git
```  

### **Adding and Committing Files**  
```bash
git add filename    # Stage a specific file
git add .           # Stage all changes
git commit -m "Initial commit"
```

### **Viewing Repository History**  
```bash
git log               # View commit history
git status            # Check current changes
git diff              # Show differences before committing
```

---

## **Branching Strategies**  

### **Creating and Switching Branches**  
```bash
git branch feature-branch    # Create a new branch
git checkout feature-branch  # Switch to the new branch
git switch main              # Switch back to the main branch (alternative to checkout)
```

### **Merging Branches**  
```bash
git checkout main
git merge feature-branch
```
Resolve merge conflicts if any occur.  

### **Rebasing for a Cleaner Commit History**  
```bash
git checkout feature-branch
git rebase main
```
This rewrites the commit history and applies changes sequentially.  

---

## **Collaborating with GitHub and GitLab**  

### **Connecting a Local Repository to Remote**  
```bash
git remote add origin https://github.com/user/repo.git
git push -u origin main
```

### **Pulling and Pushing Changes**  
```bash
git pull origin main   # Get the latest changes
git push origin main   # Push local commits to remote
```

### **Forking and Pull Requests (PRs)**  
1. Fork a repository on GitHub/GitLab.  
2. Make changes in your fork.  
3. Open a **Pull Request (PR)** to merge changes into the original repository.  

---

## **Git Workflow Strategies**  

### **1. Feature Branch Workflow**  
- Each new feature is developed in a separate branch.  
- Merged into `main` after testing.  

### **2. Gitflow Workflow**  
- Uses **main**, **develop**, **feature**, **release**, and **hotfix** branches.  
- Helps in structured software release management.  

### **3. GitHub Flow**  
- Uses **main** and **feature branches**.  
- Simple workflow, ideal for CI/CD.  

---

## **Hands-on Exercises**  

### **Exercise 1: Create a Git Repository and Commit Changes**  
1. Initialize a Git repository.  
2. Create a file, add content, and commit it.  
3. Modify the file, commit changes, and view commit history.  

### **Exercise 2: Work with Branches**  
1. Create a new branch for a feature.  
2. Make changes and commit them.  
3. Merge the feature branch into the main branch.  

### **Exercise 3: Push and Pull from GitHub/GitLab**  
1. Create a GitHub/GitLab repository.  
2. Push local commits to the remote repository.  
3. Pull changes from a collaborator’s repository.  

---

## **Summary**  
✔ Git enables efficient version control and collaboration.  
✔ Branching and merging strategies help manage workflows.  
✔ GitHub/GitLab enhance team-based development.  
