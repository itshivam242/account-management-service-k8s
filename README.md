# Account Management Service - Kubernetes Deployement
This project demonstrates the setup and deployment of the account-management-service application with MySQL database integration in a Kubernetes cluster.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

What things you need to install the software and how to install them.

- Docker
- Minikube
- kubectl
- Maven
- Java 17

### Installing

A step-by-step series of examples that tell you how to get a development environment running.

#### 1. Create a project folder and clone the Account Management service
```bash
mkdir k8s-assignment && cd k8s-assignment
git clone https://github.com/itshivam242/account-management-service-k8s.git ./
```
#### 2. Build the Spring Boot application using Maven
```bash
mvn clean install
```
#### 3. Build the Docker image
```bash
docker build -t shivammittal242/account-management-service:latest .
```
#### 4. Set Up Kubernetes Deployment and Services
Set Up MySQL Persistent Volume and Deployment of MySQL & Application
```bash
kubectl apply -f k8s/mysql-pv.yml --namespace devops
kubectl apply -f k8s/mysql-pvc.yml --namespace devops
kubectl apply -f k8s/mysql-deployment.yml --namespace devops
kubectl apply -f k8s/account-deployment.yml --namespace devops
```
#### 5. Expose the Application Using a Kubernetes Service

```bash
kubectl apply -f k8s/account-service.yml --namespace devops
```
#### 6. Check the service URL with Minikube
```bash
minikube service account-management-service --namespace devops
```
#### 7. Scaling the Application
To scale the application to multiple instances (replicas), use the following command:
```bash
kubectl scale deployment account-management-service --replicas=3 --namespace devops
```
#### 8. Check the status of the pods to ensure scaling:
```bash
kubectl get pods --namespace devops
````
#### 9. Stop the Application
To stop the application by scaling down to 0 replicas:
```bash
kubectl scale deployment account-management-service --replicas=0 --namespace devops
````
## Usage

The following API endpoints are available for managing accounts:

1. **Create a new account**
    - **HTTP Method:** POST
    - **Endpoint:** `/accounts`

2. **Add money to an account**
    - **HTTP Method:** PUT
    - **Endpoint:** `/accounts/add-money/{accountId}`

3. **Withdraw money from an account**
    - **HTTP Method:** PUT
    - **Endpoint:** `/accounts/withdraw-money/{accountId}`

4. **Get account details by account ID**
    - **HTTP Method:** GET
    - **Endpoint:** `/accounts/{accountId}`

5. **Delete an account**
    - **HTTP Method:** DELETE
    - **Endpoint:** `/accounts/{accountId}`

6. **Delete account by customer ID**
    - **HTTP Method:** DELETE
    - **Endpoint:** `/accounts/customers/{customerId}`



