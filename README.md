# Kubernetes MongoDB + Mongo Express Project
Deploy a complete MongoDB + Mongo Express application on a Kubernetes Minikube cluster using Deployments, Services, Secrets, ConfigMaps, and Namespaces.

A perfect project to demonstrate your DevOps, Cloud, and Kubernetes skills.

📚 Table of Contents

Overview

Architecture

Features

Tech Stack

Project Structure

Prerequisites

Setup Instructions

Accessing Mongo Express UI

Troubleshooting

Cleanup

Screenshots

Credits

📌 Overview

This project demonstrates how to deploy a database + UI setup using Kubernetes components:

MongoDB Deployment + ClusterIP Service

Mongo Express Deployment + NodePort Service

Secrets for DB credentials

ConfigMap for MongoDB service hostname

Namespace isolation

Minikube as the Kubernetes environment

This mirrors real-world microservice deployment patterns used in DevOps & production systems.

🏗️ Architecture
                          +-----------------------------+
                          |       User / Browser        |
                          |   http://<minikube-ip>      |
                          +--------------+--------------+
                                         |
                                         v
                           NodePort Service (30000)
                                         |
                                         v
                          Mongo Express Deployment/Pod
                                         |
             --------------------------------------------------
             |                      |                          |
      ConfigMap (DB Host)     Secret (Credentials)     UI Dashboard
             |
             v
        ClusterIP Service (MongoDB)
             |
             v
      MongoDB Deployment/Pod

✨ Features

✔ Deploy MongoDB using Kubernetes Deployment
✔ Secure DB credentials using Kubernetes Secrets
✔ Provide DB connection info using ConfigMap
✔ Expose Mongo Express UI using NodePort
✔ Isolate entire stack in custom Namespace
✔ Real-world Minikube setup for local testing
✔ Follows GitOps-friendly folder structure

🧰 Tech Stack
Component	Technology
Kubernetes	Minikube
Container Runtime	Docker
Database	MongoDB
UI	Mongo Express
Config Management	ConfigMap + Secrets
Networking	NodePort + ClusterIP
Tools	kubectl, Docker Desktop
📁 Project Structure
k8s-mongo-mongoexpress/
│
├── manifests/
│   ├── namespace.yaml
│   ├── mongo-secret.yaml
│   ├── mongo-configmap.yaml
│   ├── mongo.yaml
│   ├── mongo-express.yaml
│
└── README.md


Each manifest is modular, easy to read, and easy to deploy.

🛠 Prerequisites

Make sure these are installed:

Docker Desktop

Minikube

kubectl

Homebrew (macOS)

🚀 Setup Instructions
Start Minikube
minikube start --driver=docker --memory=1800 --cpus=2


Verify:

kubectl get nodes

Apply Kubernetes Manifests (in order)
kubectl apply -f manifests/namespace.yaml
kubectl apply -f manifests/mongo-secret.yaml
kubectl apply -f manifests/mongo-configmap.yaml
kubectl apply -f manifests/mongo.yaml
kubectl apply -f manifests/mongo-express.yaml

Check status
kubectl get pods -n demo-app
kubectl get svc -n demo-app

🌐 Accessing Mongo Express UI
Get Minikube IP:
minikube ip

Open in browser:
http://<minikube-ip>:30000


Example:

http://192.168.49.2:30000

Default Login
Username: admin
Password: pass

🛠️ Troubleshooting
Mongo Express cannot connect to MongoDB

Check logs:

kubectl logs -n demo-app -l app=mongo-express

Secret not found
kubectl get secrets -n demo-app

NodePort not accessible
minikube service mongo-express-service -n demo-app --url

🧹 Cleanup

Delete everything:

kubectl delete namespace demo-app


Stop Minikube:

minikube stop