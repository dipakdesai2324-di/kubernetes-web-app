# kubernetes-web-app
Deploy a containerized web application on Kubernetes and expose it through a Service.
# Kubernetes Web Application

## Project Overview
This project demonstrates how to deploy and manage a containerized Nginx web application using Kubernetes.
The application runs in Kubernetes Pods managed by a Deployment and is exposed through a NodePort Service. A ConfigMap stores the custom HTML webpage served by Nginx.

## Objectives
* Deploy a containerized web application on Kubernetes.
* Manage multiple application replicas using a Deployment.
* Expose the application using a Service.
* Store application content in a ConfigMap.
* Inspect and scale Pods using kubectl.
* Understand application updates and rollout behavior.

## Technologies Used
* Kubernetes
* Docker
* Nginx
* YAML
* kubectl
* Git and GitHub

## Project Structure
```text
kubernetes-web-app/
├── README.md
├── .gitignore
├── k8s/
│   ├── configmap.yaml
│   ├── deployment.yaml
│   └── service.yaml
└── docs/
    └── how-to-run.md
```

## Prerequisites
* A working Kubernetes cluster.
* kubectl installed and configured to access the cluster.
* Internet access to pull the Nginx container image.
* A Kubernetes context pointing to the intended cluster.
For a local environment, you can use Kubernetes in Docker Desktop or a Minikube cluster.

## Deploy the Application
Apply the Kubernetes configuration files: kubectl apply -f k8s/

## Verify the Resources
Check the Pods: kubectl get pods
Check the Deployment: kubectl get deployments
Check the Service: kubectl get services
Check the ConfigMap: kubectl get configmap web-app-config

## Access the Application
Use port forwarding: kubectl port-forward service/kubernetes-web-app-service 8080:80
Open the following URL in a browser while port forwarding is running: http://localhost:8080
The custom webpage should display the message "Hello from Kubernetes!"

## Scale the Application
Scale the Deployment to three replicas: kubectl scale deployment kubernetes-web-app --replicas=3
Verify the Pods: kubectl get pods

## Update and Monitor the Application
Inspect the Deployment rollout: kubectl rollout status deployment/kubernetes-web-app
Inspect the application logs: kubectl logs deployment/kubernetes-web-app

## Clean Up
Remove the resources created by this project: kubectl delete -f k8s/
If you started port forwarding, stop it by pressing Ctrl+C in its terminal.

## Learning Outcomes

This project provides practical experience with Kubernetes Deployments, Pods, Services, ConfigMaps, replicas, scaling, application access, logs, and resource cleanup.
