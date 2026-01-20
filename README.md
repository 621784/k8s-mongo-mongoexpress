# Kubernetes MongoDB + Mongo Express Project

A complete deployment of MongoDB and Mongo Express on a Kubernetes
Minikube cluster using Deployments, Services, Secrets, ConfigMaps, and
Namespaces.

## Overview

This project demonstrates how to deploy: - MongoDB (Deployment +
ClusterIP Service) - Mongo Express UI (Deployment + NodePort Service) -
Secrets for database credentials - ConfigMap for MongoDB hostname -
Namespace isolation - Minikube as the local Kubernetes environment

## Architecture

    User/Browser
        |
        v
    NodePort Service (30000)
        |
        v
    Mongo Express Pod
        |
        |-- ConfigMap (DB Host)
        |-- Secret (Credentials)
        |
        v
    MongoDB Service (ClusterIP)
        |
        v
    MongoDB Pod

## Features

-   Kubernetes Deployments for MongoDB & Mongo Express
-   Secure credentials using Secrets
-   DB configuration using ConfigMap
-   NodePort exposure for Mongo Express UI
-   Namespace-based isolation
-   Minikube-based local Kubernetes setup

## Tech Stack

  Component           Technology
  ------------------- -------------------------
  Container Runtime   Docker
  Kubernetes          Minikube
  Database            MongoDB
  UI                  Mongo Express
  Config              Secrets, ConfigMap
  Tools               kubectl, Docker Desktop

## Project Structure

    k8s-mongo-mongoexpress/
     ├── manifests/
     │   ├── namespace.yaml
     │   ├── mongo-secret.yaml
     │   ├── mongo-configmap.yaml
     │   ├── mongo.yaml
     │   └── mongo-express.yaml
     └── README.md

## Prerequisites

Install: - Docker Desktop - Minikube - kubectl - Homebrew (macOS)

## Setup Instructions

### 1. Start Minikube

    minikube start --driver=docker --memory=1800 --cpus=2
    kubectl get nodes

### 2. Apply Kubernetes Manifests

    kubectl apply -f manifests/namespace.yaml
    kubectl apply -f manifests/mongo-secret.yaml
    kubectl apply -f manifests/mongo-configmap.yaml
    kubectl apply -f manifests/mongo.yaml
    kubectl apply -f manifests/mongo-express.yaml

### 3. Check Resources

    kubectl get pods -n demo-app
    kubectl get svc -n demo-app

## Access Mongo Express UI

1.  Get Minikube IP\

```{=html}
<!-- -->
```
    minikube ip

2.  Open in browser:\

```{=html}
<!-- -->
```
    http://<minikube-ip>:30000

### Default Login

    Username: admin
    Password: pass

## Troubleshooting

### Mongo Express cannot connect to MongoDB

    kubectl logs -n demo-app -l app=mongo-express

### Secrets missing

    kubectl get secrets -n demo-app

### NodePort not accessible

    minikube service mongo-express-service -n demo-app --url

## Cleanup

    kubectl delete namespace demo-app
    minikube stop

## Credits

Created for hands-on Kubernetes & DevOps learning.
