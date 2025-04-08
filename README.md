![Screenshot 2025-04-06 162534](https://github.com/user-attachments/assets/d58fec03-6fc5-4922-9aca-5708337256c3)

# 🚀 CI/CD Pipeline for Spring Boot Application on Kubernetes

## This project demonstrates a fully automated CI/CD pipeline for deploying a Java-based Spring Boot application on a Kubernetes cluster. This streamlined pipeline automates code integration, testing, security scanning, containerization, and deployment ensuring a fast, reliable, and scalable delivery process!
## 🧰 Prerequisites
````
GitHub – Version control for source code management

Jenkins – Automating the build, test, and deployment process

Maven – Managing dependencies and building the application

SonarQube – Ensuring code quality and security

Docker – Containerizing the application for consistency

DockerHub – Hosting and distributing Docker images

Argo CD – Enabling GitOps-driven continuous deployment

Shell Scripting – Automating various pipeline tasks
````

## 🛠️ Steps to Set Up the CI/CD Pipeline
 ### 1. Install Required Jenkins Plugins
```
Git plugin

Maven Integration plugin

Pipeline plugin

Kubernetes Continuous Deploy plugin
````
### 2. Create a New Jenkins Pipeline
```
In Jenkins, create a new pipeline job.

Configure it with the Git repository URL of your Java application.

Add a Jenkinsfile to the repository to define the pipeline stages.
````
 ### 3. Define the Pipeline Stages
````
pipeline {
  agent {
    docker {
      image '8217089795/maven-anjana-docker-agent:v1'
      args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // mount Docker socket to access the host's Docker daemon
    }
  }
  stages {
    stage('Checkout') {
      steps {
        sh 'echo passed'
        //git branch: 'master', url: 'https://github.com/anjana2468/Jenkins-cicd-pipeline-project.git'
      }
    }
    stage('Build and Test') {
      steps {
        sh 'ls -ltr'
        // build the project and create a JAR file
        sh 'cd spring-boot-app && mvn clean package'
      }
    }
    stage('Static Code Analysis') {
      environment {
        SONAR_URL = "http://35.167.143.245:9000/"
      }
      steps {
        withCredentials([string(credentialsId: 'sonarqube', variable: 'SONAR_AUTH_TOKEN')]) {
          sh 'cd spring-boot-app && mvn sonar:sonar -Dsonar.login=$SONAR_AUTH_TOKEN -Dsonar.host.url=${SONAR_URL}'
        }
      }
    }
    stage('Build and Push Docker Image') {
      environment {
        DOCKER_IMAGE = "8217089795/ultimate-cicd:${BUILD_NUMBER}"
        // DOCKERFILE_LOCATION = "spring-boot-app/Dockerfile"
        REGISTRY_CREDENTIALS = credentials('docker-cred')
      }
      steps {
        script {
            sh 'cd spring-boot-app && docker build -t ${DOCKER_IMAGE} .'
            def dockerImage = docker.image("${DOCKER_IMAGE}")
            docker.withRegistry('https://index.docker.io/v1/', "docker-cred") {
                dockerImage.push()
            }
        }
      }
    }
    stage('Update Deployment File') {
        environment {
            GIT_REPO_NAME = "Jenkins-cicd-pipeline-project"
            GIT_USER_NAME = "anjana2468"
        }
        steps {
            withCredentials([string(credentialsId: 'github', variable: 'GITHUB_TOKEN')]) {
                sh '''
                    git config user.email "anjanashaju1997@gmail.com"
                    git config user.name "anjana2468"
                    BUILD_NUMBER=${BUILD_NUMBER}
                    sed -i "s/replaceImageTag/${BUILD_NUMBER}/g" spring-boot-app-manifests/deployment.yml
                    git add spring-boot-app-manifests/deployment.yml
                    git commit -m "Update deployment image to version ${BUILD_NUMBER}"
                    git push https://${GITHUB_TOKEN}@github.com/${GIT_USER_NAME}/${GIT_REPO_NAME} HEAD:master
                '''
            }
        }
    }
  }
}
````
### 4. Set Up Argo CD
```
Install Argo CD on your Kubernetes cluster.
```
### 5. Integrate Jenkins with Argo CD
```
Add your Argo CD API token to Jenkins credentials.

Update the Jenkinsfile to include the Argo CD deployment stage.
```
### 6. Run the Jenkins Pipeline
```
Trigger the Jenkins pipeline to start the CI/CD process.

Monitor each stage and resolve any issues if they arise.
```
### Screenshots

![Screenshot 2025-04-04 191647](https://github.com/user-attachments/assets/109d4be9-5db2-46d6-a5f8-23601eea717c)

![Screenshot 2025-04-04 193545](https://github.com/user-attachments/assets/c674bb5e-01c9-4480-bf62-a9cba4a8f80d)

![Screenshot 2025-04-04 193938](https://github.com/user-attachments/assets/91eec171-1dfc-4049-95c8-63d3d1ecda23)



