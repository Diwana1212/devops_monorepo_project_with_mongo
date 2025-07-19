# DevOps Monorepo Project

This is a full-stack DevOps monorepo project with the following components:

- ✅ React Frontend (Dockerized)
- ✅ Node.js Backend (Express + Swagger + MongoDB)
- ✅ MongoDB Database
- ✅ Docker support
- ✅ Kubernetes (Kind) deployment setup

---

## 🧱 Project Structure

```
devops_monorepo_project/
├── frontend/               # React app
├── backend/                # Node.js + Swagger + MongoDB connection
├── k8s/                    # Kubernetes manifests (Frontend, Backend, MongoDB)
```

---

## ⚙️ Prerequisites

- Docker
- Node.js and npm
- Kind (Kubernetes IN Docker)
- kubectl
- MongoDB (for local testing or use in-cluster service)

---

## 🚀 Setup Instructions

### 1. Clone the project

```bash
unzip devops_monorepo_project_no_jenkins_with_mongo_k8s.zip
cd devops_monorepo_project
```

---

### 2. Build Docker Images

```bash
docker build -t react-frontend ./frontend
docker build -t node-backend ./backend
```

---

### 3. Create a Kind Cluster

```bash
kind create cluster --name devops-project
```

---

### 4. Load Docker Images into Kind

```bash
kind load docker-image react-frontend --name devops-project
kind load docker-image node-backend --name devops-project
```

---

### 5. Deploy to Kubernetes

```bash
kubectl apply -f k8s/mongo-deployment.yaml
kubectl apply -f k8s/mongo-service.yaml

kubectl apply -f k8s/backend-deployment.yaml
kubectl apply -f k8s/frontend-deployment.yaml
```

---

### 6. Verify Pods and Services

```bash
kubectl get pods
kubectl get svc
```

---

### 7. Accessing the App

You can port-forward the frontend service:

```bash
kubectl port-forward deployment/frontend 3000:3000
```

Then open: [http://localhost:3000](http://localhost:3000)

Backend Swagger can be accessed by port-forwarding as well:

```bash
kubectl port-forward deployment/backend 5000:5000
```

Then open: [http://localhost:5000/api-docs](http://localhost:5000/api-docs)

---

## 🧪 Local MongoDB (optional)

If you want to run MongoDB locally instead of in Kubernetes:

```bash
docker run -d -p 27017:27017 --name mongodb mongo:5.0
```

Update the MongoDB URI in `backend/index.js` if needed.

---

## 🤝 Contribution

Feel free to improve, customize or contribute!

---

## 📜 License

MIT License
