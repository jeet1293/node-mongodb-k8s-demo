# Node & MongoDB on K8s with Minikube

This guide explains how to deploy and test a demo Kubernetes application using Minikube. This application consists of:

- A **MongoDB** deployment and service (defined in `mongo.yaml`)
- A **Web Application** (Node.js) deployment and NodePort service (defined in `webapp.yaml`)

---

## Prerequisites

- **Docker:** [Installation Instructions](https://docs.docker.com/get-docker/)
- **Minikube:** [Installation Instructions](https://minikube.sigs.k8s.io/docs/start/)
- **kubectl:** [Installation Instructions](https://kubernetes.io/docs/tasks/tools/install-kubectl/)


---

## Step 1: Start Minikube

Launch your local Kubernetes cluster with Minikube. You can specify a driver (e.g., Docker, VirtualBox) if needed:

```bash
minikube start --driver=docker
```

## Step 2: Deploy the Application

Apply your YAML files in the correct order (config and secret first, since the deployments depend on them):

```bash
kubectl apply -f manifests/
```
## Step 3: Verify the Deployments

Check that the pods and services are running correctly.

```bash
kubectl get all
```

## Step 4: Access the Web Application
Since the web application is exposed using a NodePort service, you can retrieve its URL with:
```bash
minikube service webapp-service --url
```
Open the returned URL in your browser

## Step 5: Inspect Logs and Debug
If you run into issues, check the logs of your pods.

### View Web Application Logs

```bash
kubectl logs -l app=webapp
```

### View Web MongoDB Logs

```bash
kubectl logs -l app=mongo
```

### For detailed pod information, use:

```bash
kubectl describe pod <pod-name>
```

## Step 6: Clean Up
When you’re done testing, delete the deployed resources and stop Minikube.

### Delete the Resources

```bash
kubectl delete -f manifests/
```

### Stop Minikube

```bash
minikube stop
```

By following these steps, you have successfully deployed and tested your Kubernetes demo application using Minikube. This local setup helps simulate a production-like environment for development and debugging.

## License
This project is licensed under the MIT License.
