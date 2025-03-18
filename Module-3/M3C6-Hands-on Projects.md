## **Hands-on Projects**

In this section, we will dive into two essential hands-on projects that will help you apply what you've learned about monitoring, logging, and DevOps practices in a real-world context.

### **Project 1: Implementing CI/CD Pipelines**

Continuous Integration and Continuous Deployment (CI/CD) are the backbone of modern DevOps practices, allowing for automation of the application lifecycle. By implementing CI/CD pipelines, you can streamline development, reduce the risk of errors, and ensure faster delivery of high-quality applications.

#### **Objective**:
- Implement a fully automated CI/CD pipeline using Jenkins and GitHub Actions.
- Automate testing, build, and deployment processes for a sample web application.

#### **Prerequisites**:
- Basic understanding of version control (Git).
- A working knowledge of Jenkins or GitHub Actions.
- A sample application repository on GitHub (e.g., a Node.js or Python app).

#### **Steps**:

1. **Set Up Jenkins**:
   - Install Jenkins on your system:
     ```bash
     sudo apt update
     sudo apt install openjdk-11-jdk
     wget -q -O - https://pkg.jenkins.io/keys/jenkins.io.key | sudo apt-key add -
     sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable/ / > /etc/apt/sources.list.d/jenkins.list'
     sudo apt update
     sudo apt install jenkins
     sudo systemctl start jenkins
     sudo systemctl enable jenkins
     ```
   - Access Jenkins via `http://localhost:8080` and complete the setup wizard.

2. **Integrate Jenkins with GitHub**:
   - Install the GitHub plugin in Jenkins.
   - Create a new Jenkins pipeline project.
   - Link your GitHub repository by generating a personal access token and entering it in Jenkins.

3. **Create Jenkins Pipeline**:
   - Write a `Jenkinsfile` in your GitHub repository. This file defines the steps in the pipeline.
   
   Example `Jenkinsfile`:
   ```groovy
   pipeline {
       agent any
       stages {
           stage('Checkout') {
               steps {
                   git 'https://github.com/yourusername/sample-app.git'
               }
           }
           stage('Build') {
               steps {
                   sh 'npm install'
               }
           }
           stage('Test') {
               steps {
                   sh 'npm test'
               }
           }
           stage('Deploy') {
               steps {
                   sh 'docker build -t sample-app .'
                   sh 'docker run -d -p 80:80 sample-app'
               }
           }
       }
   }
   ```

4. **Configure GitHub Actions (Alternative)**:
   If you prefer GitHub Actions over Jenkins, create a `.github/workflows/ci.yml` file in your repository.

   Example GitHub Actions workflow:
   ```yaml
   name: CI/CD Pipeline
   on:
     push:
       branches:
         - main
   jobs:
     build:
       runs-on: ubuntu-latest
       steps:
         - name: Checkout Code
           uses: actions/checkout@v2
         - name: Set up Node.js
           uses: actions/setup-node@v2
           with:
             node-version: '14'
         - name: Install dependencies
           run: npm install
         - name: Run tests
           run: npm test
         - name: Build Docker image
           run: docker build -t sample-app .
         - name: Deploy to Docker container
           run: docker run -d -p 80:80 sample-app
   ```

5. **Testing and Deployment**:
   - Push code changes to your GitHub repository and observe the automated pipeline in action.
   - Jenkins or GitHub Actions will automatically run the pipeline, executing tests, building the Docker image, and deploying the application to a container.

---

### **Project 2: Designing a Microservices Architecture and Deploying it Using Docker and Kubernetes**

Microservices architecture breaks down applications into smaller, independent services, which can be developed, deployed, and scaled independently. In this project, we will design a simple microservices-based application and deploy it using Docker and Kubernetes.

#### **Objective**:
- Design and implement a basic microservices architecture for a sample application.
- Deploy the services using Docker containers and orchestrate them using Kubernetes.

#### **Prerequisites**:
- Knowledge of Docker and Kubernetes.
- A basic understanding of microservices architecture.
- Docker and Kubernetes installed locally or on a cloud platform like AWS or GCP.

#### **Steps**:

1. **Designing the Microservices Architecture**:
   In this example, we will build two microservices for an e-commerce platform: a **Product Service** and an **Order Service**. Both services will be containerized and communicate via HTTP.

   - **Product Service**: Handles product information (e.g., product name, price).
   - **Order Service**: Manages customer orders and interacts with the Product Service to fetch product details.

2. **Develop the Microservices**:
   Create two separate applications: one for the Product Service and one for the Order Service. For simplicity, you can use Node.js or Python for building the services.

   **Product Service**:
   - Create a basic API that returns product details.
   - Example `app.js` (Node.js):
   ```javascript
   const express = require('express');
   const app = express();
   const port = 3001;

   app.get('/product', (req, res) => {
       res.json({ id: 1, name: "Laptop", price: 1000 });
   });

   app.listen(port, () => {
       console.log(`Product Service listening at http://localhost:${port}`);
   });
   ```

   **Order Service**:
   - Create a basic API that creates orders.
   - Example `app.js` (Node.js):
   ```javascript
   const express = require('express');
   const axios = require('axios');
   const app = express();
   const port = 3000;

   app.get('/order', async (req, res) => {
       const productResponse = await axios.get('http://product-service:3001/product');
       res.json({ orderId: 123, product: productResponse.data });
   });

   app.listen(port, () => {
       console.log(`Order Service listening at http://localhost:${port}`);
   });
   ```

3. **Dockerizing the Microservices**:
   - Create `Dockerfile` for both services to build Docker images.
   
   Example `Dockerfile` for Product Service:
   ```dockerfile
   FROM node:14
   WORKDIR /app
   COPY . .
   RUN npm install
   EXPOSE 3001
   CMD ["node", "app.js"]
   ```

   Build the Docker images:
   ```bash
   docker build -t product-service .
   docker build -t order-service .
   ```

4. **Deploying with Kubernetes**:
   - Create Kubernetes deployment and service configuration files for both services.

   **Product Service Deployment** (`product-service-deployment.yaml`):
   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: product-service
   spec:
     replicas: 2
     selector:
       matchLabels:
         app: product-service
     template:
       metadata:
         labels:
           app: product-service
       spec:
         containers:
         - name: product-service
           image: product-service:latest
           ports:
           - containerPort: 3001
   ---
   apiVersion: v1
   kind: Service
   metadata:
     name: product-service
   spec:
     selector:
       app: product-service
     ports:
       - protocol: TCP
         port: 80
         targetPort: 3001
   ```

   **Order Service Deployment** (`order-service-deployment.yaml`):
   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: order-service
   spec:
     replicas: 2
     selector:
       matchLabels:
         app: order-service
     template:
       metadata:
         labels:
           app: order-service
       spec:
         containers:
         - name: order-service
           image: order-service:latest
           ports:
           - containerPort: 3000
   ---
   apiVersion: v1
   kind: Service
   metadata:
     name: order-service
   spec:
     selector:
       app: order-service
     ports:
       - protocol: TCP
         port: 80
         targetPort: 3000
   ```

5. **Deploy to Kubernetes**:
   - Apply the configurations to deploy the services on Kubernetes.
   ```bash
   kubectl apply -f product-service-deployment.yaml
   kubectl apply -f order-service-deployment.yaml
   ```

6. **Testing the Deployment**:
   - Expose the services through a Kubernetes ingress or use port-forwarding to test the deployed services:
   ```bash
   kubectl port-forward service/product-service 8081:80
   kubectl port-forward service/order-service 8080:80
   ```

   - Access the services:
     - **Product Service**: `http://localhost:8081/product`
     - **Order Service**: `http://localhost:8080/order`

   - Verify that the Order Service is correctly fetching product information from the Product Service.

---

## **Conclusion**

In these hands-on projects, you have successfully implemented CI/CD pipelines using Jenkins and GitHub Actions and designed a microservices architecture, deploying it with Docker and Kubernetes. These projects provide you with practical experience in automating application delivery and deploying containerized applications in a scalable manner, which are essential skills in the modern DevOps landscape.

By completing these projects, you’ve gained valuable insights into the real-world application of DevOps tools and techniques that are fundamental to delivering high-quality software quickly and efficiently.
