# dotnetcore-kubernetes

Deploy .NET Core Application on Kubernetes with Helm, Prometheus, and RabbitMQ  
Tested on Ubuntu VM running in Oracle VirtualBox

---

## 📚 Project Overview

This project demonstrates deploying a .NET Core application to a Kubernetes cluster, with monitoring (Prometheus + Grafana) and RabbitMQ (Bitnami Helm Chart) on Ubuntu.  
All Kubernetes resources are managed with YAML and Helm.

---

## 🖥️ Prerequisites

- Oracle VirtualBox
- Ubuntu (LTS recommended, e.g., 22.04)
- Kubernetes Cluster (Minikube or kubeadm)
- kubectl
- Helm 3.x

---

## ⚡ Setup Instructions

### 1. Install Kubernetes (Minikube Example)

```bash
sudo apt update
sudo apt install -y curl wget apt-transport-https
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube start --driver=none
```
### 2. Install Helm & Repositories

```bash
mkdir helm
cd helm
wget https://get.helm.sh/helm-v3.4.1-linux-amd64.tar.gz
tar -xvf helm-v3.4.1-linux-amd64.tar.gz
sudo mv linux-amd64/helm /usr/local/bin

helm version
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
```
### 3. Install Prometheus & Grafana Stack

```bash
helm install prometheus prometheus-community/kube-prometheus-stack
```

### 4. Install RabbitMQ (Bitnami Helm Chart)

```bash
helm install my-rabbitmq bitnami/rabbitmq
```
## Deploy .NET Core Application
- dotnetcore-configmap.yaml
- dotnetapp-deployment.yaml
- dotnetcore-service.yaml
- dotnetcore-ingress.yaml
- 
```bash
kubectl apply -f dotnetcore-configmap.yaml
kubectl apply -f dotnetapp-deployment.yaml
kubectl apply -f dotnetcore-service.yaml
kubectl apply -f dotnetcore-ingress.yaml
```
### 🚀 Quick Start
1. Create Ubuntu VM in Oracle VirtualBox
2. Install Kubernetes, kubectl, Helm
3. Add Helm repos & install Prometheus, RabbitMQ
4. Apply .yaml files for your .NET Core app
5. Access the app via Service/Ingress
6. Monitor using Grafana dashboard
