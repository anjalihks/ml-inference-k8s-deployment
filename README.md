# 🩺 Diabetes Prediction – End-to-End MLOps Deployment  

![Python](https://img.shields.io/badge/Python-3.10-blue)
![FastAPI](https://img.shields.io/badge/FastAPI-Framework-green)
![Docker](https://img.shields.io/badge/Docker-Containerized-blue)
![Kubernetes](https://img.shields.io/badge/Kubernetes-Orchestrated-326CE5)
![MLOps](https://img.shields.io/badge/MLOps-Production--Ready-orange)

---

## 🚀 Project Overview

This project demonstrates an end-to-end MLOps pipeline for deploying a Machine Learning model into a scalable, production-ready cloud-native environment.

A Random Forest classifier is trained to predict whether a person is diabetic based on key health metrics.  
The trained model is exposed via a REST API using FastAPI, containerized using Docker, and deployed to Kubernetes with multiple replicas for high availability and scalability.

This project simulates how ML models are productionized in real-world DevOps and Cloud environments.

---

## 🎯 Problem Statement

Predict whether a person is diabetic based on:

- Pregnancies  
- Glucose  
- Blood Pressure  
- BMI  
- Age  

Dataset used: Pima Indians Diabetes Dataset.

---

## 🏗 Architecture

### 🔹 High-Level System Architecture

```
                        +-------------------+
                        |      Client       |
                        +---------+---------+
                                  |
                                  v
                        +-------------------+
                        |   Load Balancer   |
                        +---------+---------+
                                  |
                                  v
                        +-------------------+
                        | Kubernetes Service|
                        +---------+---------+
                                  |
                 +----------------+----------------+
                 |                                 |
        +--------v--------+               +--------v--------+
        |      Pod 1      |               |      Pod 2      |
        |  (Replica 1)    |               |  (Replica 2)    |
        +--------+--------+               +--------+--------+
                 |                                 |
                 v                                 v
        +----------------+               +----------------+
        |  FastAPI App   |               |  FastAPI App   |
        | + Loaded Model |               | + Loaded Model |
        +----------------+               +----------------+
```

---

## 🧠 MLOps Workflow

This project implements the following lifecycle:

1. Data Collection  
2. Offline Model Training  
3. Model Serialization (.pkl artifact)  
4. REST API for Inference  
5. Containerization using Docker  
6. Kubernetes Deployment  
7. Horizontal Scaling & High Availability  

---

## 📂 Project Structure

```
ml-inference-k8s-deployment/
│
├── app/
│   ├── train.py              # Model training script
│   └── main.py               # FastAPI inference service
│
├── k8s/
│   └── deployment.yaml       # Kubernetes Deployment & Service
│
├── requirements.txt          # Python dependencies
├── Dockerfile                # Container definition
├── .gitignore
└── README.md
```

---

## 🧪 Model Training

The training script:

- Loads dataset  
- Selects relevant features  
- Splits data into train/test  
- Trains RandomForestClassifier  
- Saves model as `diabetes_model.pkl`  

### Run Training

```bash
python train.py
```

This generates:

```
diabetes_model.pkl
```

This file is the serialized model artifact used for inference.

---

## 🌐 FastAPI Inference Service

The API:

- Loads model at startup
- Exposes REST endpoints
- Validates inputs
- Returns JSON predictions

### Endpoints

**Health Check**
```
GET /
```

**Prediction**
```
POST /predict
```

### Sample Request

```json
{
  "Pregnancies": 2,
  "Glucose": 130,
  "BloodPressure": 70,
  "BMI": 28.5,
  "Age": 45
}
```

### Sample Response

```json
{
  "diabetic": true
}
```

---

## 🐳 Dockerization

The application is containerized to ensure:

- Environment consistency  
- Dependency management  
- Portability across systems  

### Build Docker Image

```bash
docker build -t your-dockerhub-username/diabetes-api .
```

### Run Locally

```bash
docker run -p 8000:8000 your-dockerhub-username/diabetes-api
```

---

## ☸️ Kubernetes Deployment

Deployment includes:

- Deployment resource (replicas: 2)
- Service resource
- LoadBalancer for external access

### Deploy

```bash
kubectl apply -f k8s/deployment.yaml
```

### Production Characteristics

- High availability (multiple replicas)
- Self-healing pods
- Stateless architecture
- Load-balanced traffic

---

## 📈 Scalability & Reliability

- Horizontal scaling via replica count
- Kubernetes automatically recreates failed pods
- Stateless design enables easy scaling
- Ready for HPA (Horizontal Pod Autoscaler)

---

## 🔄 Model Update Workflow

1. Retrain model
2. Generate new `.pkl`
3. Rebuild Docker image
4. Push new image
5. Rolling update in Kubernetes

Follows immutable infrastructure best practices.

---

## ☁ Cloud Mapping (AWS Example)

| Component       | AWS Equivalent |
|-----------------|----------------|
| Docker Image    | Amazon ECR     |
| Kubernetes      | Amazon EKS     |
| LoadBalancer    | AWS ELB        |
| Model Artifact  | Amazon S3      |

---

## 🔐 Future Enhancements

- CI/CD pipeline (GitHub Actions / Jenkins)
- Image version tagging
- Liveness & readiness probes
- Prometheus monitoring
- Centralized logging
- Model version registry
- Infrastructure as Code (Terraform)
- Horizontal Pod Autoscaler

---

## 🎯 Key Concepts Demonstrated

- Supervised learning deployment
- Model serialization
- REST-based inference
- Stateless microservice architecture
- Docker containerization
- Kubernetes orchestration
- Horizontal scalability
- Self-healing infrastructure
- Immutable deployments

---

## 👨‍💻 Anjali Yadav

End-to-End ML deployment project demonstrating practical MLOps and cloud-native deployment concepts.
