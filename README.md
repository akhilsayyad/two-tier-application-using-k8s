# Two-Tier Application Deployment Using Kubernetes

## Project Overview
Deployed a two-tier web application using Kubernetes, consisting of a Python Flask backend and a MySQL database. The application uses Kubernetes Deployments, Services, Persistent Volumes, and Persistent Volume Claims for container orchestration and database storage.

## Technologies Used
- Kubernetes
- Docker
- Python Flask
- MySQL
- YAML
- Persistent Volumes (PV) & Persistent Volume Claims (PVC)
- Kubernetes Services

## Project Architecture

          User / Browser
                |
                |
          Flask Service
                |
          Flask Pod(s)
                |
           MySQL Service
                |
            MySQL Pod
                |
             MySQL PVC
                |
             MySQL PV

## Project Structure

two-tier-application-using-k8s/
├── two-tier-app-deployment.yml
├── two-tier-app-svc.yml
├── mysql-deployment.yml
├── mysql-svc.yml
├── mysql-pv.yml
├── mysql-pvc.yml
└── README.md

## Kubernetes Components

- **Deployments:** Manage application and MySQL pods.
- **Services:** Enable communication between Flask and MySQL.
- **Persistent Volume (PV):** Provides persistent database storage.
- **Persistent Volume Claim (PVC):** Requests storage for MySQL.
- **Environment Variables:** Configure database connection details.
- **Labels and Selectors:** Connect Services with the correct Pods.
- **Container Images:** Package and run application dependencies.

## Deployment Steps

**1. Apply MySQL storage configurations**

kubectl apply -f mysql-pv.yml
kubectl apply -f mysql-pvc.yml

**2. Deploy MySQL**

kubectl apply -f mysql-deployment.yml
kubectl apply -f mysql-svc.yml

**3. Deploy Flask application**

kubectl apply -f two-tier-app-deployment.yml
kubectl apply -f two-tier-app-svc.yml


## Verification Commands

kubectl get pods
kubectl get deployments
kubectl get services
kubectl get pv
kubectl get pvc
kubectl describe pod <pod-name>
kubectl logs <pod-name>

## Troubleshooting

kubectl get pods -o wide
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl get events --sort-by=.metadata.creationTimestamp
kubectl get endpoints

## Key Learning Outcomes

- Container orchestration using Kubernetes.
- Deploying multi-tier applications.
- Managing application replicas using Deployments.
- Internal communication using ClusterIP Services.
- Persistent database storage using PV and PVC.
- Managing application configuration using environment variables.
- Troubleshooting Pods, Services, and Deployments.
- Managing Kubernetes resources using YAML manifests.

## Access the Application

**1. Get the Flask Service details**

kubectl get svc

**2. If using NodePort, find the assigned port**

kubectl get svc two-tier-app-svc

**3. Access the application**

Open your browser:

http://<EC2-PUBLIC-IP>:<NODEPORT>

For example:
http://13.x.x.x:30004

**Note:**
- Ensure the EC2 Security Group allows inbound traffic on your NodePort.
- Ensure the Kubernetes worker node is accessible from your browser.
- If using ClusterIP instead of NodePort, use port forwarding:

kubectl port-forward svc/two-tier-app-svc 5000:5000

Then open:

http://localhost:5000
