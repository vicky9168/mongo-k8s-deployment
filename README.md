🗄️ MongoDB + Mongo Express on Kubernetes

A Kubernetes project that deploys MongoDB (database) and Mongo Express (web UI) using Secrets, ConfigMaps, and Services.

🖼️ Architecture Diagram

![Uploading img1.png…]()

🚀 What This Project Does
Deploys MongoDB as backend database
Deploys Mongo Express as frontend UI
Uses Secret for secure credentials
Uses ConfigMap for database configuration
Exposes application using LoadBalancer Service
🧩 Components
🔹 MongoDB
Internal database
Uses Secret for authentication
Exposed via ClusterIP Service (internal only)
🔹 Mongo Express
Web-based MongoDB UI
Connects using:
Secret (username/password)
ConfigMap (MongoDB service name)
Exposed externally via LoadBalancer Service
📂 Project Files
mongodb-secret.yaml → Stores credentials
mongo.yaml → MongoDB Deployment + Service
mongo-configmap.yaml → DB configuration
mongo-express.yaml → Mongo Express setup
⚙️ Setup
kubectl apply -f mongodb-secret.yaml
kubectl apply -f mongo.yaml
kubectl apply -f mongo-configmap.yaml
kubectl apply -f mongo-express.yaml
🔍 Verify
kubectl get pods
kubectl get svc
kubectl get all
kubectl get configmap
kubectl get secret
🌐 Access Application
kubectl get svc mongo-express-service

👉 Open in browser:

http://<EXTERNAL-IP>:8081
🔁 Application Flow
Browser → LoadBalancer → Mongo Express → MongoDB Service → MongoDB
⚠️ Notes
MongoDB is not exposed publicly (ClusterIP)
Mongo Express is exposed using LoadBalancer
In local setups (Minikube / Kops), EXTERNAL-IP may stay pending
Since you are using Kops, ensure:
Proper cloud provider setup (AWS ELB)
IAM permissions are configured
Otherwise, consider using NodePort for testing
