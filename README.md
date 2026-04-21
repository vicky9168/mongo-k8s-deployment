# 🗄️ MongoDB + Mongo Express Kubernetes Deployment

This project contains Kubernetes manifests to deploy **MongoDB (database)** and **Mongo Express (web UI)** using **Secrets, ConfigMaps, and Services**.

---

## 🖼️ Architecture Diagram

<img width="1536" height="1024" alt="img1" src="https://github.com/user-attachments/assets/b02e6723-c85b-42d0-b279-a064850b733c" />


---

## 🚀 Components

### 🔹 MongoDB Deployment: `mongodb-deployment`

* Runs MongoDB database in a Pod  
* Uses credentials from **Secret**  
* Label: `app=mongodb`  

### 🔹 Mongo Express Deployment: `mongo-express-deployment`

* Runs Mongo Express web UI  
* Connects to MongoDB using:
  * Secret (username/password)  
  * ConfigMap (database URL)  
* Label: `app=mongo-express`  

### 🔹 Services

* **mongodb-service**
  * Type: `ClusterIP`  
  * Used for internal communication  

* **mongo-express-service**
  * Type: `LoadBalancer`  
  * Exposes application externally  

---

## 📂 Files

* `mongodb-secret.yaml` → Stores DB credentials  
* `mongo.yaml` → MongoDB Deployment + Service  
* `mongo-configmap.yaml` → Database configuration  
* `mongo-express.yaml` → Mongo Express Deployment + Service  

---

## ⚙️ Prerequisites

* Kubernetes cluster (EKS / Minikube / Kops)  
* `kubectl` installed and configured  
* Internet access to pull Docker images  

---

## 📦 Deployment Steps

### 1️⃣ Clone the repository

```bash
git clone <your-repo-url>
cd <repo-name>
```

### 2️⃣ Apply Kubernetes manifests

```bash
kubectl apply -f mongodb-secret.yaml
kubectl apply -f mongo.yaml
kubectl apply -f mongo-configmap.yaml
kubectl apply -f mongo-express.yaml
```

### 3️⃣ Verify resources

```bash
kubectl get pods
kubectl get svc
kubectl get all
kubectl get configmap
kubectl get secret
```

---

## 🌐 Access Application

Get external IP:

```bash
kubectl get svc mongo-express-service
```

Then access:

```
http://<EXTERNAL-IP>:8081
```

---

## 🔁 Application Flow

```
Browser → LoadBalancer → Mongo Express → MongoDB Service → MongoDB
```

---

## ⚠️ Important Notes

* MongoDB is **not exposed publicly** (ClusterIP)  
* Mongo Express is exposed using **LoadBalancer**  
* In local setups (**Minikube / Kops**), **EXTERNAL-IP may stay pending**  

Since you are using **Kops**, ensure:

* Cloud provider (AWS ELB) is properly configured  
* IAM permissions are set correctly  

👉 Otherwise, use **NodePort** or `kubectl port-forward` for testing  

---

---
