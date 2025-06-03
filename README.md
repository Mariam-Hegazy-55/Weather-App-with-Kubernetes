#  WeatherApp on Kubernetes (KIND)

A cloud-native microservices application deployed on a local Kubernetes cluster using KIND (Kubernetes in Docker). WeatherApp showcases a modular architecture built for learning and experimenting with Kubernetes and microservices locally.

---

## 🔍 Project Summary

WeatherApp consists of four main components:

- 🎨 **UI Service (`weatherapp-ui`)** – The frontend user interface.
- 🌤️ **Weather Engine (`weatherapp-weather`)** – Fetches weather data from external APIs.
- 🛡️ **User Gateway (`weatherapp-auth`)** – Handles user authentication.
- 🗃️ **Data Core (MySQL)** – Stores user credentials and related data.

---

## 🧩 System Architecture

Kubernetes primitives are used to manage and orchestrate the application:

- ⚙️ **Deployments** for stateless components (UI, Weather, Auth).
- 🏛️ **StatefulSet** for MySQL, ensuring persistent identity and storage.
- 🔌 **ClusterIP Services** for internal service discovery and communication.
- 🌐 **Ingress Controller (Nginx)** to expose the app externally.
- 💽 **StorageClass** and **PersistentVolumes** to ensure data persistence.

![image](https://github.com/user-attachments/assets/863250b2-2684-4667-89d5-f3677ae0fd54)

---

🛠️ Requirements Before You Begin
To run WeatherApp locally, ensure you have:

🐋 Docker (for containerization)

☸️ KIND or Minikube (for local Kubernetes cluster)

🛠️ Kubectl (for cluster interaction)


## 🚀 Deployment Steps

Follow the steps below to deploy WeatherApp on a local Kubernetes cluster using KIND:

```bash
# 1. Clone the repository
git clone https://github.com/YOUR_GITHUB_USERNAME/weatherapp.git
cd weatherapp

# 2. Create a KIND cluster
kind create cluster --name weatherapp

# 3. Apply the storage configuration
kubectl apply -f storageclass.yaml

# 4. Deploy the MySQL database
kubectl apply -f statefulset.yaml
kubectl apply -f headless-service.yaml

# 5. (Optional) Run an initialization job for the database
kubectl apply -f init-job.yaml

# 6. Deploy the application microservices
kubectl apply -f deployment.yaml        # UI
kubectl apply -f deployment\ 2.yaml     # Auth service
kubectl apply -f deployment\ 3.yaml     # Weather service

# 7. Apply the services for each component
kubectl apply -f service.yaml
kubectl apply -f service\ 2.yaml
kubectl apply -f service\ 3.yaml

# 8. Apply ingress configuration
kubectl apply -f ingress.yaml

# 9. Verify that all components are running
kubectl get pods
kubectl get svc
kubectl get ingress

# 10. Access the application
# Make sure to map weatherapp.local in your /etc/hosts file:
# 127.0.0.1 weatherapp.local
# Then open:
http://weatherapp.local


---


