dotnetcore-kubernetes

Deploy .NET Core Application on Kubernetes with Helm, Prometheus, and RabbitMQFor use on Ubuntu VM running in Oracle VirtualBox

Project Overview

This project demonstrates deploying a .NET Core application to a Kubernetes cluster, alongside a monitoring stack (Prometheus + Grafana) and RabbitMQ (Bitnami Helm Chart), on Ubuntu in Oracle VirtualBox. All resources are managed with YAML manifests and Helm.

Prerequisites

Oracle VirtualBox

Ubuntu (recommend LTS version, e.g., 22.04)

Kubernetes Cluster (Minikube or kubeadm)

kubectl

Helm 3.x

Setup Instructions

1. Install Kubernetes (Minikube Example)

sudo apt update
sudo apt install -y curl wget apt-transport-https
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube start --driver=none

2. Install Helm

mkdir helm
cd helm
wget https://get.helm.sh/helm-v3.4.1-linux-amd64.tar.gz
tar -xvf helm-v3.4.1-linux-amd64.tar.gz
sudo mv linux-amd64/helm /usr/local/bin
helm version

3. Add Helm Repositories

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update

4. Install Prometheus & Grafana Stack

helm install prometheus prometheus-community/kube-prometheus-stack

5. Install RabbitMQ (Bitnami Helm Chart)

helm install my-rabbitmq bitnami/rabbitmq

You can adjust configuration using the RabbitMQ values.yaml

6. Deploy .NET Core Application (Kubernetes YAML)

Files to use:

dotnetcore-configmap.yaml: ConfigMap for the app

dotnetapp-deployment.yaml: Deployment for .NET Core app

dotnetcore-service.yaml: Service to expose the app

dotnetcore-ingress.yaml: Ingress config (optional)

Deploy with kubectl:

kubectl apply -f dotnetcore-configmap.yaml
kubectl apply -f dotnetapp-deployment.yaml
kubectl apply -f dotnetcore-service.yaml
kubectl apply -f dotnetcore-ingress.yaml

7. Check Installation Status

kubectl get pod,svc,ingress
helm list

8. Access Grafana Dashboard

Find the Grafana Service port (usually 3000):

kubectl get svc

Open your browser to http://<NodeIP>:<Port>

Default User: admin

Default Password: prom-operator

Directory Structure

dotnetcore-kubernetes/
├── dotnetapp-deployment.yaml
├── dotnetcore-configmap.yaml
├── dotnetcore-ingress.yaml
├── dotnetcore-service.yaml
└── README.md

References

Helm Official

Prometheus Helm Chart

Bitnami RabbitMQ Chart

Kubernetes Docs

Quick Start

Spin up Ubuntu VM on Oracle VirtualBox

Install Kubernetes, kubectl, Helm

Add Helm repos and deploy Prometheus, RabbitMQ

Apply all provided .yaml files for your .NET Core app

Access your app via Service/Ingress

Monitor with Grafana dashboard

Fork, clone, or use as a template for your own Kubernetes lab.
Contributions are welcome!
