#Important File Locations in Repository
- Backend Dockerfile: finsmartbackend-frontend-backend/Dockerfile
- Frontend Dockerfile: finsmartbackend-frontend-main/Dockerfile
- Nginx Configuration: finsmartbackend-frontend-main/nginx.conf
- MySQL Kubernetes YAML: k8s/mysql-deployment.yaml
- Backend Kubernetes YAML: k8s/backend-deployment.yaml
- Frontend Kubernetes YAML: k8s/frontend-deployment.yaml
- Frontend API Configuration: finsmartbackend-frontend-main/src/api/axiosConfig.js
- Stock API Configuration: finsmartbackend-frontend-main/src/api/stockApi.js
- Project Documentation: README.md

# FinSmart Finances – Containerization & Kubernetes Deployment

A cloud deployment project demonstrating application containerization using **Docker**, orchestration using **Kubernetes (k3s)**, and deployment on **AWS EC2**.

## Project Overview

FinSmart Finances is a web-based financial management application with a React frontend, Spring Boot backend, and MySQL database.

This project demonstrates how to:
- Containerize the frontend and backend using Docker.
- Configure communication between containers using Nginx.
- Run MySQL in a container with persistent storage.
- Deploy application components using Kubernetes Deployments and Services.
- Expose the frontend through a Kubernetes NodePort service.
- Deploy the application on an AWS EC2 Ubuntu server.

## Technology Stack

| Technology | Purpose |
|---|---|
| React.js | Frontend |
| Java 17 | Backend runtime |
| Spring Boot | Backend framework |
| MySQL 8.0 | Database |
| Docker | Application containerization |
| Nginx | Frontend web server and reverse proxy |
| Kubernetes (k3s) | Container orchestration |
| AWS EC2 | Cloud hosting |
| Ubuntu Server 24.04 LTS | Cloud operating system |
| Git & GitHub | Version control |

## Repository Structure

The following structure shows the important project directories and configuration files:

```text
Finsmart_Finances_New/
│
├── finsmartbackend-frontend-backend/
│   │
│   ├── ⭐ Dockerfile
│   ├── pom.xml
│   ├── mvnw
│   ├── .mvn/
│   └── src/
│       └── main/
│           └── java/
│               └── com/finsmart/
│                   └── Finsmart_Finances/
│                       └── controller/
│
├── finsmartbackend-frontend-main/
│   │
│   ├── ⭐ Dockerfile
│   ├── ⭐ nginx.conf
│   ├── package.json
│   ├── package-lock.json
│   ├── public/
│   └── src/
│       ├── api/
│       │   ├── axiosConfig.js
│       │   └── stockApi.js
│       └── components/
│
├── ⭐ k8s/
│   ├── ⭐ mysql-deployment.yaml
│   ├── ⭐ backend-deployment.yaml
│   └── ⭐ frontend-deployment.yaml
│
└── ⭐ README.md
```

## Important Files and Their Locations

The following files are the main implementation files for this assignment.

### 1. Backend Dockerfile

<mark>Location:</mark>

`finsmartbackend-frontend-backend/Dockerfile`

Purpose:
- Uses the Eclipse Temurin Java 17 base image.
- Copies Maven configuration and backend source code.
- Builds the Spring Boot application using Maven.
- Exposes port `8099`.
- Starts the generated Spring Boot JAR.

### 2. Frontend Dockerfile

<mark>Location:</mark>

`finsmartbackend-frontend-main/Dockerfile`

Purpose:
- Uses Node.js 20 Alpine to install dependencies and build the React application.
- Uses a multi-stage Docker build.
- Uses Nginx Alpine to serve the production frontend.
- Exposes port `80`.

### 3. Nginx Configuration

<mark>Location:</mark>

`finsmartbackend-frontend-main/nginx.conf`

Purpose:
- Serves the React frontend.
- Handles frontend routes using `index.html`.
- Forwards API requests to the Spring Boot backend.
- Supports communication between frontend and backend containers through Kubernetes service networking.

### 4. MySQL Kubernetes Configuration

<mark>Location:</mark>

`k8s/mysql-deployment.yaml`

Purpose:
- Creates a MySQL 8.0 Deployment.
- Creates a PersistentVolumeClaim for database storage.
- Configures the database and application user.
- Creates a ClusterIP Service named `finsmart-mysql`.

### 5. Backend Kubernetes Configuration

<mark>Location:</mark>

`k8s/backend-deployment.yaml`

Purpose:
- Deploys the Spring Boot backend.
- Uses the Docker image `finsmart-backend:v1`.
- Exposes container port `8099`.
- Connects to MySQL using the Kubernetes service hostname `finsmart-mysql`.
- Creates a ClusterIP Service named `finsmart-backend`.

### 6. Frontend Kubernetes Configuration

<mark>Location:</mark>

`k8s/frontend-deployment.yaml`

Purpose:
- Deploys the React frontend using Nginx.
- Uses the Docker image `finsmart-frontend:v1`.
- Exposes container port `80`.
- Creates a NodePort Service to provide external access.

## Assignment Implementation

### Part A – Docker Containerization

**Step 1: Identify the application structure**

Identified the React frontend, Spring Boot backend, and MySQL database components.

**Step 2: Verify backend and frontend configuration**

Inspected the Java version, Maven configuration, React dependencies, application ports, and database connection settings.

**Step 3: Create the backend Dockerfile**

Created the backend Dockerfile using Java 17 and Maven to package the Spring Boot application.

**Step 4: Build the backend Docker image**

```bash
docker build -t finsmart-backend:v1 .
```

**Step 5: Create the frontend Dockerfile**

Created a multi-stage Dockerfile using Node.js for the React build and Nginx for serving the production application.

**Step 6: Configure Nginx**

Created `nginx.conf` to serve the frontend and forward API requests to the backend service.

**Step 7: Build the frontend Docker image**

```bash
docker build -t finsmart-frontend:v1 .
```

**Step 8: Configure Docker networking**

Created a Docker network to allow communication between the frontend, backend, and database containers.

**Step 9: Run the MySQL container**

Used the official MySQL 8.0 image and configured persistent database storage.

**Step 10: Run and verify the application containers**

Started the frontend and backend containers and checked application connectivity and database initialization.

### Part B – Kubernetes Deployment

**Step 1: Prepare Kubernetes configuration files**

Created the `k8s/` directory containing three YAML configuration files.

**Step 2: Deploy MySQL**

```bash
kubectl apply -f k8s/mysql-deployment.yaml
```

**Step 3: Deploy the backend**

```bash
kubectl apply -f k8s/backend-deployment.yaml
```

**Step 4: Deploy the frontend**

```bash
kubectl apply -f k8s/frontend-deployment.yaml
```

**Step 5: Verify deployments and pods**

```bash
kubectl get deployments
kubectl get pods
kubectl get services
```

The application uses three main Kubernetes components:

| Component | Kubernetes resource | Service type |
|---|---|---|
| MySQL | Deployment | ClusterIP |
| Backend | Deployment | ClusterIP |
| Frontend | Deployment | NodePort |

### Part C – AWS Cloud Implementation

The application was deployed on an AWS EC2 Ubuntu server.

**AWS environment:**
- Cloud provider: Amazon Web Services
- Service: EC2
- Operating system: Ubuntu Server 24.04 LTS
- Container runtime: Docker
- Kubernetes distribution: k3s

**Implementation steps:**

1. Launched an Ubuntu EC2 instance.
2. Configured SSH access using a key pair.
3. Installed Docker on the EC2 instance.
4. Installed k3s for Kubernetes orchestration.
5. Transferred the project files to EC2 using SCP.
6. Built the backend and frontend Docker images.
7. Imported the custom images into the k3s container runtime.
8. Deployed MySQL, backend, and frontend using Kubernetes YAML files.
9. Exposed the frontend using a NodePort service.
10. Verified the application pods and Kubernetes services.

## Docker Images

The following images were created or used:

| Image | Description |
|---|---|
| `finsmart-backend:v1` | Custom Spring Boot backend image |
| `finsmart-frontend:v1` | Custom React frontend image |
| `mysql:8.0` | Official MySQL database image |

The MySQL image was pulled from Docker Hub rather than built from a custom Dockerfile.

## AWS Deployment Information

The frontend was exposed through a Kubernetes NodePort service.

**Frontend access URL (EC2):**

`http://15.207.71.76:32640`

The NodePort used by the frontend service is `32640`.

The EC2 security group must allow inbound TCP traffic on the configured NodePort for external browser access.

## Useful Kubernetes Commands

Check all pods:

```bash
sudo kubectl get pods
```

Check services:

```bash
sudo kubectl get services
```

Check deployments:

```bash
sudo kubectl get deployments
```

View backend logs:

```bash
sudo kubectl logs deployment/finsmart-backend
```

View frontend logs:

```bash
sudo kubectl logs deployment/finsmart-frontend
```

View MySQL logs:

```bash
sudo kubectl logs deployment/finsmart-mysql
```

Restart the frontend deployment:

```bash
sudo kubectl rollout restart deployment/finsmart-frontend
```

Check rollout status:

```bash
sudo kubectl rollout status deployment/finsmart-frontend
```

## Key Learning Outcomes

- Understanding Dockerfiles and Docker image creation.
- Containerizing frontend and backend applications.
- Using multi-stage Docker builds.
- Configuring Nginx as a reverse proxy.
- Understanding Docker networking and persistent storage.
- Creating Kubernetes Deployments, Services, and PersistentVolumeClaims.
- Deploying a multi-container application using Kubernetes.
- Deploying containerized applications on AWS EC2.
- Managing application containers using kubectl and k3s.

## Security Notes

- Do not commit private SSH keys, AWS credentials, API keys, or production passwords.
- Use Kubernetes Secrets or an appropriate external secrets manager for sensitive configuration.
- Replace demonstration database credentials before production deployment.
- Restrict SSH and application access through appropriate EC2 security group rules.


---

**Project:** FinSmart Finances – Containerization & Kubernetes Deployment Challenge  
**Focus:** Docker, Kubernetes, AWS EC2, and Cloud Deployment
