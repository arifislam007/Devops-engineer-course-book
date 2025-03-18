# **Chapter 3: Continuous Integration/Continuous Deployment (CI/CD)**

## **Introduction to CI/CD**

Continuous Integration (CI) and Continuous Deployment (CD) are practices that automate the processes of integrating code changes into a shared repository and deploying applications in a continuous and automated way. CI/CD pipelines are at the core of DevOps practices, ensuring that software is built, tested, and deployed efficiently, while reducing human error and increasing collaboration between development and operations teams.

- **Continuous Integration (CI)**: The practice of merging all developer working copies to a shared mainline several times a day. This helps in detecting integration bugs early and improves the quality of software.
- **Continuous Deployment (CD)**: The practice of automatically deploying the integrated code to production without manual intervention. This ensures that updates are continuously pushed to the live environment.

## **CI/CD Pipeline Overview**

A CI/CD pipeline automates the stages of software delivery, making sure that every change is tested and deployed efficiently. A typical pipeline might include:

1. **Source Code Management**: Code is committed to a version control system like Git.
2. **Build**: The code is compiled, dependencies are installed, and a build artifact is generated.
3. **Test**: Automated tests are run to check the quality and functionality of the code.
4. **Deploy**: After passing tests, the code is deployed to different environments such as staging, testing, and production.

In this chapter, we’ll cover the most commonly used tools for CI/CD—**Jenkins** and **GitHub Actions**—and guide you through setting up automated pipelines for building, testing, and deploying applications.

---

## **Jenkins: A Powerful CI/CD Tool**

### **What is Jenkins?**

Jenkins is an open-source automation server that facilitates continuous integration and continuous delivery (CI/CD). It enables developers to build, test, and deploy applications in an automated fashion. Jenkins supports a wide range of plugins that make it extendable for a variety of programming languages and environments.

### **Setting Up Jenkins**

1. **Installing Jenkins**
   Jenkins can be installed on a variety of operating systems, including Linux, macOS, and Windows. The easiest method is to use the `.war` file to run Jenkins.

   - Download the Jenkins WAR file:
     ```bash
     wget http://updates.jenkins-ci.org/download/war/2.277.1/jenkins.war
     ```
   - Run Jenkins:
     ```bash
     java -jar jenkins.war
     ```

2. **Configuring Jenkins**
   After installing Jenkins, you can access the Jenkins dashboard at `http://localhost:8080`. The first time you access Jenkins, you'll need to unlock it using the initial admin password located in the `/var/jenkins_home/secrets/initialAdminPassword` file.

3. **Installing Plugins**
   Jenkins supports many plugins that provide functionality for various CI/CD tasks. Some commonly used plugins include:
   - Git Plugin: For interacting with Git repositories.
   - Pipeline Plugin: For defining multi-step pipelines.
   - Docker Plugin: For integrating Jenkins with Docker.

   You can install plugins by navigating to **Manage Jenkins > Manage Plugins**.

### **Creating a Jenkins Pipeline**

1. **Pipeline as Code**: 
   Jenkins allows you to define your CI/CD pipeline using a `Jenkinsfile`, which is stored in your source code repository. The `Jenkinsfile` defines the steps of the pipeline in a declarative or scripted format.

   A basic `Jenkinsfile` might look like this:

   ```groovy
   pipeline {
       agent any
       stages {
           stage('Build') {
               steps {
                   echo 'Building application...'
                   sh 'mvn clean install'
               }
           }
           stage('Test') {
               steps {
                   echo 'Running tests...'
                   sh 'mvn test'
               }
           }
           stage('Deploy') {
               steps {
                   echo 'Deploying application...'
                   sh './deploy.sh'
               }
           }
       }
   }
   ```

2. **Running the Pipeline**: 
   Once your `Jenkinsfile` is committed to your Git repository, Jenkins will automatically pick it up and run the defined stages. The Jenkins job will appear in the Jenkins dashboard, where you can monitor the progress of your pipeline.

---

## **GitHub Actions: Automating CI/CD with GitHub**

### **What are GitHub Actions?**

GitHub Actions is a powerful CI/CD tool integrated directly into GitHub. It allows you to automate workflows, such as testing, building, and deploying applications, directly from your GitHub repositories. GitHub Actions provides a YAML-based configuration for defining workflows that are triggered by events like pushes, pull requests, or on a schedule.

### **Setting Up GitHub Actions**

1. **Creating a Workflow File**  
   In a GitHub repository, workflows are defined in `.github/workflows/` directory. You can define the workflow in a `.yml` file.

   For example, a simple GitHub Actions workflow file for a Node.js application might look like this:

   ```yaml
   name: Node.js CI/CD Pipeline

   on:
     push:
       branches:
         - main

   jobs:
     build:
       runs-on: ubuntu-latest
       steps:
         - name: Checkout code
           uses: actions/checkout@v2

         - name: Set up Node.js
           uses: actions/setup-node@v2
           with:
             node-version: '14'

         - name: Install dependencies
           run: npm install

         - name: Run tests
           run: npm test

         - name: Deploy to Production
           run: ./deploy.sh
           if: github.ref == 'refs/heads/main'
   ```

   In this example:
   - The pipeline triggers on a push to the `main` branch.
   - It checks out the code, sets up Node.js, installs dependencies, runs tests, and deploys to production.

2. **Running the Workflow**  
   After you push the `.yml` workflow file to your repository, GitHub Actions automatically runs the pipeline on the specified events. You can monitor the workflow’s progress under the **Actions** tab in the repository.

---

## **Automated Testing and Deployment**

### **Automated Testing in CI/CD**

Automated testing ensures that your application functions correctly before it is deployed. It’s an essential part of the CI/CD pipeline, as it helps identify bugs early in the process.

1. **Unit Tests**: These tests verify the correctness of small units of code (such as functions or methods).
2. **Integration Tests**: These tests verify that different components of the system work together as expected.
3. **End-to-End Tests**: These tests simulate real user interactions to verify the overall functionality of the application.

Automated tests can be integrated into Jenkins and GitHub Actions pipelines to run after the build stage. Below is an example of running tests in a Jenkins pipeline:

```groovy
stage('Test') {
    steps {
        echo 'Running unit tests...'
        sh 'npm test'
    }
}
```

Similarly, in GitHub Actions, the test stage can be added to the workflow:

```yaml
- name: Run tests
  run: npm test
```

### **Automated Deployment**

Once the application passes the tests, it’s time to deploy it to production (or other environments like staging or QA). This is done by automating the deployment step in the CI/CD pipeline.

1. **Deploying to Cloud Providers**: Both Jenkins and GitHub Actions can deploy applications to cloud platforms like AWS, Azure, or Google Cloud, using CLI commands or infrastructure-as-code tools such as Terraform.
   
   In Jenkins:
   ```groovy
   stage('Deploy') {
       steps {
           echo 'Deploying to AWS'
           sh 'aws s3 cp build/ s3://my-bucket/ --recursive'
       }
   }
   ```

   In GitHub Actions:
   ```yaml
   - name: Deploy to AWS
     run: aws s3 cp build/ s3://my-bucket/ --recursive
   ```

2. **Deploying Containers**: You can also deploy Docker containers to container orchestration platforms like Kubernetes or Amazon ECS.

   For example, to deploy a Docker container on AWS ECS in a GitHub Actions workflow:
   ```yaml
   - name: Deploy to ECS
     run: |
       ecs-cli configure --region us-east-1 --access-key ${{ secrets.AWS_ACCESS_KEY_ID }} --secret-key ${{ secrets.AWS_SECRET_ACCESS_KEY }}
       ecs-cli compose --file docker-compose.yml service up
   ```

---

## **Hands-on Exercise**

### **Exercise 1: Set Up a Jenkins Pipeline**

1. Install Jenkins and create a simple Jenkins pipeline for a Node.js application.
2. Integrate the pipeline with GitHub.
3. Add stages for build, test, and deploy in the `Jenkinsfile`.

### **Exercise 2: Set Up a GitHub Actions Workflow**

1. Create a GitHub repository and set up a basic GitHub Actions workflow for continuous integration and deployment.
2. Include stages for code checkout, building, testing, and deploying the application.

---

## **Summary**

- **CI/CD** practices help automate the software delivery lifecycle by integrating code continuously and deploying it automatically.
- **Jenkins** and **GitHub Actions** are powerful tools for implementing CI/CD pipelines.
- Automated testing ensures that code is always verified before being deployed.
- Automated deployment pushes applications to production seamlessly.

By adopting these practices, teams can improve the quality and speed of their software development processes.
