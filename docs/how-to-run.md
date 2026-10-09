# How to Run the Kubernetes Web Application

## 1. Project Overview
This project deploys an Nginx web application on Kubernetes. It uses a Deployment to manage two replicas, a Service to provide stable access, and a ConfigMap to supply the webpage content.

## 2. Prerequisites
Before running the project, ensure the following are available:
* Docker Desktop with Kubernetes enabled, or Minikube with a running Kubernetes cluster.
* kubectl installed.
* Access to the correct Kubernetes context.
* Internet connectivity to download the Nginx image.

## 3. Verify Kubernetes
Check the kubectl installation: kubectl version --client
Check the active Kubernetes context: kubectl config current-context
Verify that the cluster is reachable: kubectl cluster-info
Check the available nodes: kubectl get nodes
The cluster should be running and its nodes should be ready before continuing.

## 4. Navigate to the Project Directory
Open a terminal in the project root directory: cd kubernetes-web-app
Use the actual path where you cloned or extracted the repository.

## 5. Deploy the Application
Apply the configuration files: kubectl apply -f k8s/
This creates the ConfigMap, Deployment, and Service.

## 6. Verify the Deployment
Check the Deployment: kubectl get deployments
Check the Pods: kubectl get pods
Wait until both Pods are in the Running state and ready.
Check the Service: kubectl get service kubernetes-web-app-service

## 7. Access the Application
Run: kubectl port-forward service/kubernetes-web-app-service 8080:80
Keep this terminal open and visit: http://localhost:8080
The browser should display the custom webpage.
Port forwarding provides a convenient local access method without requiring direct access to the Kubernetes NodePort.

## 8. Scale the Application
Increase the replica count to three: kubectl scale deployment kubernetes-web-app --replicas=3
Verify the new replica count: kubectl get deployment kubernetes-web-app
Check the Pods: kubectl get pods
Kubernetes should create an additional Pod to match the desired replica count.

## 9. Inspect Application Logs
Run: kubectl logs deployment/kubernetes-web-app
This command displays logs from a selected Pod belonging to the Deployment. If you need to inspect a specific replica, obtain its name using `kubectl get pods` and run `kubectl logs POD_NAME`.

## 10. Clean Up Resources
Remove the resources created by the project: kubectl delete -f k8s/
Stop port forwarding by pressing Ctrl+C in the terminal where it is running.

## 11. Expected Outcome
After completing the steps:
* Kubernetes runs the Nginx application in two Pods.
* The ConfigMap provides the custom HTML content.
* The Service provides stable access to the application.
* The application is accessible at `http://localhost:8080` through port forwarding.
* The Deployment can be scaled to three replicas.
* The resources can be inspected and deleted using kubectl.

## 12. Troubleshooting
### Pods Are Not Running
Run: kubectl describe pods
Review the Events section for image-pull, scheduling, or configuration errors.

### Application Is Not Accessible
Check the Pods and Service: 
kubectl get pods
kubectl get service kubernetes-web-app-service
Ensure port forwarding is still running and use `http://localhost:8080`.

### ConfigMap Is Missing
Check: kubectl get configmap web-app-config 
If the ConfigMap is missing, apply the project files again: kubectl apply -f k8s/

### Cluster Is Not Reachable
Check the active context and node status:
kubectl config current-context
kubectl get nodes
Start your local cluster if it is stopped, and verify that kubectl is configured for the correct cluster.

