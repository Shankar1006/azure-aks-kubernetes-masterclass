# Create AKS Cluster

## Step-01: Introduction
- Understand about AKS Cluster
- Discuss about Kubernetes Architecture from AKS Cluster perspective

## Step-02: Create AKS Cluster
- Create Kubernetes Cluster
- **Basics**
  - **Subscription:** Free Trial
  - **Resource Group:** Creat New: aks-rg1
  - **Kubernetes Cluster Name:** aksdemo1
  - **Region:** (US) Central US
  - **Kubernetes Version:** Select what ever is latest stable version
  - **Node Size:** Standard DS2 v2 (Default one)
  - **Node Count:** 1
- **Node Pools**
  - leave to defaults
- **Authentication**
  - Authentication method: 	System-assigned managed identity
  - Rest all leave to defaults
- **Networking**
  - **Network Configuration:** Advanced
  - **Network Policy:** Azure
  - Rest all leave to defaults
- **Integrations**
  - Azure Container Registry: None
  - leave to defaults
- **Tags**
  - leave to defaults
- **Review + Create**
  - Click on **Create**


## Step-03: Cloud Shell - Configure kubectl to connect to AKS Cluster
- Go to https://shell.azure.com  //opens command line interface in azure portal
```
# Template
az aks get-credentials --resource-group <Resource-Group-Name> --name <Cluster-Name>

# Replace Resource Group & Cluster Name
az aks get-credentials --resource-group aks-rg1 --name aksdemo1

# List Kubernetes Worker Nodes
kubectl get nodes 
kubectl get nodes -o wide // To get detailed information
```

## Step-04: Explore Cluster Control Plane and Workload inside that
```
# List Namespaces
kubectl get namespaces  //shows namespaces
(or)
kubectl get ns

# List Pods from all namespaces // Pod represents a single instance of a running process in your cluster
kubectl get pods --all-namespaces    //to see all workloads in namespace, those are system default workloads which runs by default

# List all k8s objects from Cluster Control plane
kubectl get all --all-namespaces
```

## Step-05: Explore the AKS cluster on Azure Management Console
- Explore the following features on high-level
- **Overview**
  - Activity Log
  - Access Control (IAM)
  - Security
  - Diagnose and solver problems
- **Settings**
  - Node Pools
  - Upgrade
  - Scale
  - Networking
  - DevSpaces
  - Deployment Center
  - Policies
- **Monitoring**
  - Insights
  - Alerts
  - Metrics
  - and many more 
- **VM Scale Sets**
  - Verify Azure VM Instances               //Virtual machines scale set-->Settings/Networking-->Accelerating Network should be enabled
  - Verify if **Enhanced Networking is enabled or not**  



## Step-06: Local Desktop - Install Azure CLI and Azure AKS CLI
```
# Install Azure CLI (MAC)
brew update && brew install azure-cli

# Login to Azure
az login

# Install Azure AKS CLI
az aks install-cli

# Configure Cluster Creds (kube config)
az aks get-credentials --resource-group aks-rg1 --name aksdemo1

# List AKS Nodes
kubectl get nodes 
kubectl get nodes -o wide
```
- **Reference Documentation Links**
- https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest
- https://docs.microsoft.com/en-us/cli/azure/aks?view=azure-cli-latest

## Step-07: Deploy Sample Application and Test
- Don't worry about what is present in these two files for now. 
- By the time we complete **Kubernetes Fundamentals** sections, you will be an expert in writing Kubernetes manifest in YAML.
- For now just focus on result. 
```
# Deploy Application
kubectl apply -f kube-manifests/

# Verify Pods
kubectl get pods

# Verify Deployment
kubectl get deployment

# Verify Service (Make a note of external ip)
kubectl get service

# Access Application
http://<External-IP-from-get-service-output>
```

## Step-07: Clean-Up
```
# Delete Applications
kubectl delete -f kube-manifests/   //after deleting verify pods,deployment, services whether present or not...
```

## References
- https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-macos?view=azure-cli-latest

## Why Managed Identity when creating Cluster?
- https://docs.microsoft.com/en-us/azure/aks/use-managed-identity
