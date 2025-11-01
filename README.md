Local Kubernetes Cluster Deployment with Minikube

## Objective
To deploy a containerized application to a local Kubernetes cluster (Minikube), demonstrating core concepts of application lifecycle management: deployment, service exposure, scaling, and logging.

## Tools & Technologies
* **Kubernetes** : v1.34.0 (Managed by Minikube)
* **Cluster Tool** : Minikube v1.37.0 (Using Docker driver)
* **Docker Desktop** : For access
* **Client Tool** : kubectl
* **Application Image** : `k8s.gcr.io/echoserver:1.10`

## Deliverables
The following files confirm the successful completion of the task:

1.  **deployment.yaml** : Defines the desired state for the application (initial state: 2 replicas).
2.  **service.yaml** : Defines a **NodePort** service to expose the application externally.
3.  **images** :  Contains visual evidence of each step (listed below).
4.  **logs** : when scaled.
## Execution Steps & Verification
The following steps were executed and verified via the corresponding screenshots:

**1. Cluster Start**
    `minikube start --driver=docker `
     minikube status ( to know the satus of minikube )
<img width="745" height="449" alt="Image" src="https://github.com/user-attachments/assets/9b510ef0-d240-4df3-9822-c70a32c807c2" />
**2. Deployment** 
    `kubectl apply -f deployment.yaml`
     kubectl apply -f service.yaml
**3. Initial Pods** 
    `kubectl get pods` 
     Confirms the initial **2 Pods** are in a **Running** state.
**4. Service Exposure**
    `kubectl get services`
     Confirms the **NodePort** service is active and correctly configured
<img width="745" height="449" alt="Image" src="https://github.com/user-attachments/assets/bdb90467-80f9-4500-a97e-6c417f5645d8" />
**5. Scaling** 
    `kubectl scale deployment my-web-deployment --replicas=5`
   **Scales** the application replicas from 2 to 5
**6. Verification** 
    `kubectl get pods` 
     Confirms the total of **5 Pods** are now Running.
<img width="745" height="449" alt="Image" src="https://github.com/user-attachments/assets/85518598-8abd-42f0-bd0a-9d43088a5b3d" />
**7. Inspection**
    `kubectl describe deployment my-web-deployment`
     Provides detailed logs, confirming the **Scaling Event** and resource status.
<img width="1920" height="1020" alt="Image" src="https://github.com/user-attachments/assets/48646a63-1594-4692-95e6-2652a5575715" />
**8. Access Test** 
    `minikube service my-web-service --url` 
     Confirms the application is accessible from the host machine.
     type the https://,..... on screen after running the above command
     the below image provides same 
<img width="1920" height="403" alt="Image" src="https://github.com/user-attachments/assets/a4e635d9-7e39-46fc-b88e-35ebd4fefbbf" />

## Cleanup

The following commands were run after successful completion and documentation to safely free up local system resources:
# Remove application resources
kubectl delete -f service.yaml
kubectl delete -f deployment.yaml

# Delete the Minikube cluster environment
minikube delete
