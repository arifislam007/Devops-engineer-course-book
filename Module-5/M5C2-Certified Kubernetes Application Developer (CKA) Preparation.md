# **Certified Kubernetes Application Developer (CKA) Preparation**  

The **Certified Kubernetes Application Developer (CKA)** certification validates your ability to design, build, and deploy cloud-native applications using Kubernetes. This section provides a structured study plan, key concepts, exam strategies, and resources to help you pass the CKA exam with confidence.  

---

## **1. Exam Overview**  

### **Certification Details:**  
- **Exam Name:** Certified Kubernetes Application Developer (CKA)  
- **Format:** Performance-based (hands-on tasks in a live Kubernetes environment)  
- **Duration:** 2 hours  
- **Cost:** $395 USD  
- **Passing Score:** 66%  
- **Prerequisites:** Basic knowledge of Linux, Docker, and Kubernetes fundamentals  
- **Exam Mode:** Online proctored  

### **Who Should Take This Exam?**  
- DevOps engineers  
- Cloud engineers  
- Kubernetes practitioners  
- Developers deploying and maintaining Kubernetes applications  

---

## **2. Exam Domains & Weightage**  

The CKA exam is divided into different domains:  

| Domain | Description | Weightage |
|--------|------------|-----------|
| **1. Application Design & Build** | Creating and managing Kubernetes workloads | 20% |
| **2. Application Environment, Configuration, and Security** | ConfigMaps, Secrets, Security, and RBAC | 25% |
| **3. Application Deployment** | Deployments, Rollbacks, and Helm Charts | 20% |
| **4. Services & Networking** | Service discovery, Ingress, Network Policies | 20% |
| **5. Troubleshooting** | Debugging applications and cluster issues | 15% |

---

## **3. Key Study Areas**  

### **Domain 1: Application Design & Build (20%)**  
- Understand **Pods, Deployments, ReplicaSets, and StatefulSets**  
- Create and manage **ConfigMaps and Secrets**  
- Use **kubectl run, create, apply, delete**  
- Manage **initContainers and sidecar containers**  

### **Domain 2: Application Environment, Configuration, and Security (25%)**  
- Use ConfigMaps and Secrets for environment configurations  
- Set up **RBAC (Role-Based Access Control)**  
- Manage Kubernetes **Service Accounts**  
- Apply **Network Policies**  

### **Domain 3: Application Deployment (20%)**  
- Deploy applications using **kubectl** and **YAML manifests**  
- Perform rolling updates and rollbacks  
- Use **Helm** to manage Kubernetes applications  

### **Domain 4: Services & Networking (20%)**  
- Configure and troubleshoot **ClusterIP, NodePort, LoadBalancer, and ExternalName Services**  
- Configure and use **Ingress controllers**  
- Implement **Network Policies**  

### **Domain 5: Troubleshooting (15%)**  
- Debug failing Pods using **kubectl logs, describe, exec**  
- Identify issues in **CrashLoopBackOff, ErrImagePull, and Pending Pods**  
- Analyze **Resource Limits and Requests**  

---

## **4. Study Plan (2-Week Preparation Guide)**  

| Day | Study Topics | Hands-on Practice |
|-----|-------------|-------------------|
| **Day 1-2** | Kubernetes architecture, API objects, kubectl basics | Create and manage Pods, Deployments |
| **Day 3-4** | ConfigMaps, Secrets, Environment Variables | Store and retrieve sensitive data |
| **Day 5-6** | Deployments, StatefulSets, Rolling Updates | Deploy and rollback apps |
| **Day 7-8** | Services, Ingress, Load Balancing | Expose apps via Ingress |
| **Day 9-10** | RBAC, Network Policies, Security | Implement role-based access |
| **Day 11-12** | Troubleshooting, Debugging Applications | Debug failing Pods and events |
| **Day 13** | Practice Exam 1 | Full-length exam simulation |
| **Day 14** | Practice Exam 2 | Full-length exam simulation |

---

## **5. Sample Questions & Commands**  

### **Question 1:**  
How do you create a Deployment with 3 replicas using `nginx` image?  

✅ **Command:**  
```bash
kubectl create deployment nginx --image=nginx --replicas=3
```

---

### **Question 2:**  
How do you expose a Deployment as a ClusterIP Service on port 80?  

✅ **Command:**  
```bash
kubectl expose deployment nginx --port=80 --target-port=80 --type=ClusterIP
```

---

### **Question 3:**  
How do you view logs of a failing pod?  

✅ **Command:**  
```bash
kubectl logs <pod-name> -n <namespace>
```

---

### **Question 4:**  
How do you debug a container using `kubectl exec`?  

✅ **Command:**  
```bash
kubectl exec -it <pod-name> -- /bin/sh
```

---

## **6. Exam Tips & Best Practices**  

✅ **Use kubectl shortcuts** – Time is critical in the exam.  
✅ **Bookmark the Kubernetes documentation** – You can use it during the test.  
✅ **Practice YAML files** – Writing manifests quickly saves time.  
✅ **Know common debugging techniques** – Using `kubectl logs`, `describe`, and `exec`.  
✅ **Work on time management** – Prioritize easier questions first.  
✅ **Use aliases and autocomplete** – `kubectl get po -A` instead of `kubectl get pods --all-namespaces`.  

---

## **7. Additional Learning Resources**  

📌 **Kubernetes Documentation:** [https://kubernetes.io/docs/](https://kubernetes.io/docs/)  
📌 **CKA Exam Guide:** [Linux Foundation](https://training.linuxfoundation.org/certification/certified-kubernetes-application-developer-cka/)  
📌 **Hands-on Labs:** Katacoda, Play with Kubernetes  
📌 **Mock Exams:** Killer.sh (Recommended for real exam experience)  

---

## **Final Thoughts**  
By following this study plan, practicing hands-on labs, and solving sample questions, you will be well-prepared to pass the **CKA Exam**.  
