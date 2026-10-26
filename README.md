 Java CI/CD Pipeline with Jenkins, Docker, SonarQube, Kubernetes & Argo CD

 Project Overview

This project demonstrates an end-to-end **CI/CD pipeline for a Java Spring Boot application** using Jenkins, Docker, SonarQube, Docker Hub, Kubernetes (Minikube), and Argo CD.

The pipeline automates application building, testing, code quality analysis, Docker image publishing, and GitOps-based deployment to a local Kubernetes cluster.

**This project runs without an AWS EC2 instance**, using a local development environment with Minikube for Kubernetes deployment.

The goal is to implement a practical DevOps workflow that improves deployment consistency, code quality, and automation.

        Developer
            |
            v
     GitHub Application Repository
            |
            v
          Jenkins
            |
      Docker Build Agent
            |
            v
      Maven Build & Test
            |
            v
        SonarQube
      Code Quality Gate
            |
            v
      Docker Image Build
            |
            v
         Docker Hub
            |
            v
    Update GitOps Repository
            |
            v
          Argo CD
            |
            v
     Kubernetes (Minikube)
            |
            v
    Spring Boot Application
```

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Java | Application development |
| Spring Boot | Java application framework |
| Maven | Build and test automation |
| GitHub | Source code management |
| Jenkins | CI/CD pipeline orchestration |
| Docker | Containerization and build agent |
| SonarQube | Static code analysis and Quality Gate |
| Docker Hub | Container image registry |
| Kubernetes | Application orchestration |
| Minikube | Local Kubernetes cluster |
| Argo CD | GitOps-based continuous delivery |

## ⚙️ CI/CD Workflow

### 1. Source Code Management
The Spring Boot source code, `pom.xml`, `Dockerfile`, and `Jenkinsfile` are stored in GitHub.

### 2. Jenkins Pipeline
Jenkins checks out the source code and executes the pipeline using a Docker-based build agent.

### 3. Build and Test
Maven compiles the application, runs tests, and verifies the build.

```bash
mvn clean verify
```

### 4. SonarQube Code Analysis
Jenkins submits the project for static code analysis. The pipeline checks the configured Quality Gate before proceeding.

### 5. Docker Image Creation
Docker packages the Spring Boot application into a container image.

Example:

```bash
docker build -t YOUR_DOCKERHUB_USERNAME/java-application:latest .
```

### 6. Push to Docker Hub
The pipeline authenticates using Jenkins credentials and pushes the image to Docker Hub.

For traceability, the pipeline can publish a unique tag based on the Jenkins build number.

Example:

```text
YOUR_DOCKERHUB_USERNAME/java-application:BUILD_NUMBER
```

### 7. GitOps Repository Update
Jenkins updates the Kubernetes manifest in a separate GitOps repository with the newly published image tag and pushes the change to GitHub.

### 8. Argo CD Deployment
Argo CD monitors the GitOps repository and synchronizes the desired configuration with the Kubernetes cluster.

### 9. Kubernetes Deployment
Minikube runs the application as Kubernetes Pods and exposes it through a Kubernetes Service.

## 📂 Repository Structure

Example application repository:

```text
java-application/
├── src/
│   ├── main/
│   └── test/
├── pom.xml
├── Dockerfile
├── .dockerignore
├── Jenkinsfile
└── README.md
```

Example GitOps repository:

```text
java-application-gitops/
└── kubernetes/
    ├── deployment.yaml
    └── service.yaml
```

The directory names should match the actual structure of your repositories and the path configured in Argo CD.

## ☸️ Kubernetes Deployment

The Kubernetes Deployment manages the application replicas, while the Service provides network access to the application.

Example commands to inspect the deployment:

```bash
kubectl get deployments
kubectl get pods
kubectl get services
```

To inspect the Argo CD application:

```bash
kubectl get applications -n argocd
```

For local access, use the appropriate Minikube Service URL or configure port forwarding.



## 🎯 Key Learning Outcomes

- Building an automated CI/CD pipeline using Jenkins.
- Configuring a Docker-based Jenkins build agent.
- Integrating SonarQube code analysis into CI.
- Building and publishing Docker images.
- Deploying containerized applications to Kubernetes.
- Implementing GitOps with Argo CD.
- Separating application source code from Kubernetes deployment configuration.
- Running a complete local DevOps workflow without EC2.



## 📌 Project Notes

This project uses a local Minikube environment and does not require an EC2 instance.

Update the repository links, Docker Hub image name, Kubernetes paths, and other placeholders before publishing. Describe only the stages and features that have been implemented and verified.
