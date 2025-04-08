![Screenshot 2025-04-06 162534](https://github.com/user-attachments/assets/d58fec03-6fc5-4922-9aca-5708337256c3)

***🚀 CI/CD Pipeline for Spring Boot Application on Kubernetes***

This project demonstrates a fully automated CI/CD pipeline for deploying a Java-based Spring Boot application on a Kubernetes cluster. It leverages industry-standard DevOps tools to ensure a seamless workflow from development to production.

🧰 Prerequisites
GitHub – Version control for source code management

Jenkins – Automating the build, test, and deployment process

Maven – Managing dependencies and building the application

SonarQube – Ensuring code quality and security

Docker – Containerizing the application for consistency

DockerHub – Hosting and distributing Docker images

Argo CD – Enabling GitOps-driven continuous deployment

Shell Scripting – Automating various pipeline tasks

🛠️ Steps to Set Up the CI/CD Pipeline
1. Install Required Jenkins Plugins
Git plugin

Maven Integration plugin

Pipeline plugin

Kubernetes Continuous Deploy plugin

2. Create a New Jenkins Pipeline
In Jenkins, create a new pipeline job.

Configure it with the Git repository URL of your Java application.

Add a Jenkinsfile to the repository to define the pipeline stages.

3. Define the Pipeline Stages
✅ Stage 1: Checkout Source Code
Use the Git plugin to check out the source code from the Git repository.

🛠️ Stage 2: Build Application
Use the Maven Integration plugin to build the Java application.

🧪 Stage 3: Run Unit Tests
Use JUnit and Mockito plugins to execute unit tests.

🔍 Stage 4: Code Quality Analysis
Use the SonarQube plugin to analyze the code quality.

📦 Stage 5: Package Application
Use Maven to package the application into a .jar file.

🧪 Stage 6: Deploy to Test Environment
Use Helm with the Kubernetes Continuous Deploy plugin to deploy the application.

✅ Stage 7: User Acceptance Testing
Run user acceptance tests using a tool like Selenium.

🚀 Stage 8: Deploy to Production
Promote the application to production using Argo CD.

4. Set Up Argo CD
Install Argo CD on your Kubernetes cluster.

Set up a Git repository for Argo CD to track Helm charts and Kubernetes manifests.

Create a Helm chart for your Java application.

Add the Helm chart to the Git repository tracked by Argo CD.

5. Integrate Jenkins with Argo CD
Add your Argo CD API token to Jenkins credentials.

Update the Jenkinsfile to include the Argo CD deployment stage.

6. Run the Jenkins Pipeline
Trigger the Jenkins pipeline to start the CI/CD process.

Monitor each stage and resolve any issues if they arise.

![Screenshot 2025-04-04 191647](https://github.com/user-attachments/assets/109d4be9-5db2-46d6-a5f8-23601eea717c)

![Screenshot 2025-04-04 193545](https://github.com/user-attachments/assets/c674bb5e-01c9-4480-bf62-a9cba4a8f80d)

![Screenshot 2025-04-04 193938](https://github.com/user-attachments/assets/91eec171-1dfc-4049-95c8-63d3d1ecda23)



