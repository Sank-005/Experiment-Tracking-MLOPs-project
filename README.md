# End-to-End Sentiment Analysis MLOps Pipeline

> An end-to-end machine learning project that demonstrates the complete lifecycle of a sentiment analysis system—from experimentation and reproducible pipelines to automated deployment and production monitoring.

![Python](https://img.shields.io/badge/Python-3.10-blue)
![MLflow](https://img.shields.io/badge/MLflow-Experiment%20Tracking-orange)
![DVC](https://img.shields.io/badge/DVC-Pipeline%20Management-purple)
![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED)
![AWS](https://img.shields.io/badge/AWS-Cloud%20Deployment-FF9900)
![Kubernetes](https://img.shields.io/badge/Kubernetes-EKS-326CE5)
![CI/CD](https://img.shields.io/badge/CI%2FCD-Automated-success)
![Prometheus](https://img.shields.io/badge/Prometheus-Monitoring-E6522C)

---

## 📌 Overview

This project implements an **end-to-end sentiment analysis machine learning workflow** with a strong focus on **MLOps practices and production deployment**.

While building an accurate model is an important part of any machine learning system, a real-world ML application also requires reproducibility, experiment tracking, versioning, automated testing, reliable deployment, and monitoring. This project explores those aspects by taking a sentiment analysis application through a complete ML lifecycle.

The workflow covers:

**Data → Processing → Feature Engineering → Model Training → Evaluation → Model Registration → Deployment → Monitoring**

---

## 🎯 Project Objectives

The objective of this project is to build a sentiment analysis system while applying practical MLOps principles throughout its lifecycle.

Key goals include:

* Building a modular machine learning pipeline for sentiment analysis
* Tracking experiments and model performance using MLflow
* Creating reproducible pipelines using DVC
* Managing pipeline artifacts with remote storage
* Automating validation and deployment workflows using CI/CD
* Containerizing the application using Docker
* Deploying the application on AWS using Kubernetes
* Monitoring the deployed application using Prometheus and Grafana

---

# 🏗️ Project Architecture

```text
                         ┌─────────────────────┐
                         │   Sentiment Data    │
                         └──────────┬──────────┘
                                    │
                         ┌──────────▼──────────┐
                         │   Data Ingestion    │
                         └──────────┬──────────┘
                                    │
                         ┌──────────▼──────────┐
                         │ Data Preprocessing  │
                         └──────────┬──────────┘
                                    │
                         ┌──────────▼──────────┐
                         │ Feature Engineering │
                         └──────────┬──────────┘
                                    │
                         ┌──────────▼──────────┐
                         │   Model Building    │
                         └──────────┬──────────┘
                                    │
                         ┌──────────▼──────────┐
                         │  Model Evaluation   │
                         └──────────┬──────────┘
                                    │
                         ┌──────────▼──────────┐
                         │  Model Registration │
                         └──────────┬──────────┘
                                    │
                  ┌─────────────────▼─────────────────┐
                  │        Flask Application          │
                  └─────────────────┬─────────────────┘
                                    │
                         ┌──────────▼──────────┐
                         │ Docker + CI/CD      │
                         └──────────┬──────────┘
                                    │
                         ┌──────────▼──────────┐
                         │ AWS ECR / AWS EKS   │
                         └──────────┬──────────┘
                                    │
                         ┌──────────▼──────────┐
                         │  Production Service │
                         └──────────┬──────────┘
                                    │
                    ┌───────────────▼───────────────┐
                    │ Prometheus → Grafana          │
                    │ Monitoring & Visualization    │
                    └───────────────────────────────┘
```

---

# 🔄 End-to-End MLOps Workflow

```text
┌────────────────┐
│ Experimentation │
└───────┬────────┘
        ▼
┌────────────────┐
│ MLflow / DagsHub│
│ Experiment Track│
└───────┬────────┘
        ▼
┌────────────────┐
│  DVC Pipeline   │
│ Reproducibility │
└───────┬────────┘
        ▼
┌────────────────┐
│ Testing & CI/CD │
└───────┬────────┘
        ▼
┌────────────────┐
│ Docker Image    │
└───────┬────────┘
        ▼
┌────────────────┐
│ AWS ECR         │
└───────┬────────┘
        ▼
┌────────────────┐
│ Kubernetes (EKS)│
└───────┬────────┘
        ▼
┌────────────────┐
│ Prometheus &    │
│ Grafana         │
└────────────────┘
```

---

# 🧠 Machine Learning Pipeline

The sentiment analysis workflow is organized into modular stages to keep the codebase maintainable and the pipeline reproducible.

```text
src/
│
├── logger/
├── data_ingestion.py
├── data_preprocessing.py
├── feature_engineering.py
├── model_building.py
├── model_evaluation.py
└── register_model.py
```

### Pipeline Stages

| Stage                   | Description                                              |
| ----------------------- | -------------------------------------------------------- |
| **Data Ingestion**      | Loads data required for the sentiment analysis workflow  |
| **Data Preprocessing**  | Cleans and prepares raw text data                        |
| **Feature Engineering** | Transforms processed data into useful model features     |
| **Model Building**      | Trains candidate machine learning models                 |
| **Model Evaluation**    | Evaluates model performance using defined metrics        |
| **Model Registration**  | Registers selected models for further use and deployment |

---

# 🧪 Experiment Tracking

The project uses **MLflow with DagsHub** to manage machine learning experimentation.

Experiment tracking helps organize and compare different training runs by recording relevant information such as:

* Model parameters
* Experiment metrics
* Model artifacts
* Training runs

This provides better visibility into the model development process and makes experimentation easier to reproduce.

---

# 🔁 Reproducible Pipelines with DVC

The machine learning workflow is structured as a **DVC pipeline**, allowing different stages of the project to be executed and reproduced systematically.

```bash
dvc repro
```

The pipeline configuration separates the workflow into clearly defined stages and uses parameter configuration to support reproducible experimentation.

DVC remote storage can also be configured using **Amazon S3** for managing pipeline artifacts.

```text
Source Code ─────────► Git
ML Pipeline ─────────► DVC
Data / Artifacts ────► DVC Remote Storage
Experiments ─────────► MLflow / DagsHub
```

---

# ⚙️ Continuous Integration & Deployment

The project includes automated workflows using **GitHub Actions**.

The CI/CD pipeline helps automate parts of the software and deployment lifecycle, including validation, testing, container image creation, and cloud deployment.

```text
Code Push
    │
    ▼
Run Tests
    │
    ▼
Build Docker Image
    │
    ▼
Push Image to AWS ECR
    │
    ▼
Deploy to AWS EKS
```

This helps bring software engineering practices into the machine learning development workflow.

---

# 🐳 Containerization

The sentiment analysis application is containerized using **Docker**, packaging the application and its dependencies into a portable deployment unit.

### Build the image

```bash
docker build -t sentiment-analysis-app:latest .
```

### Run the container

```bash
docker run -p 8888:5000 sentiment-analysis-app:latest
```

---

# ☁️ Cloud Deployment with AWS

The application is designed to use AWS services across different stages of the deployment workflow.

| AWS Service    | Role in the Project                         |
| -------------- | ------------------------------------------- |
| **Amazon S3**  | Remote storage for DVC-managed artifacts    |
| **Amazon ECR** | Container image registry                    |
| **Amazon EKS** | Managed Kubernetes environment              |
| **EC2**        | Infrastructure used for monitoring services |

The containerized application can be deployed to an EKS cluster and exposed through a Kubernetes service.

---

# ☸️ Kubernetes Deployment

The application is deployed using **Amazon Elastic Kubernetes Service (EKS)**.

The deployment workflow follows:

```text
Application Code
       │
       ▼
Docker Image
       │
       ▼
Amazon ECR
       │
       ▼
EKS Cluster
       │
       ▼
Kubernetes Pods
       │
       ▼
LoadBalancer Service
       │
       ▼
Sentiment Analysis API
```

Using Kubernetes introduces concepts commonly used in production environments, including container orchestration, deployments, services, and scalable infrastructure.

---

# 📊 Monitoring & Observability

A deployed ML system should be observable after deployment.

This project integrates a monitoring stack consisting of:

### Prometheus

Prometheus is used to collect metrics from the deployed application at configured intervals.

### Grafana

Grafana is used to visualize monitored metrics through dashboards.

```text
Deployed Application
        │
        │ Metrics
        ▼
   Prometheus
        │
        ▼
     Grafana
        │
        ▼
 Monitoring Dashboard
```

---

# 🛠️ Tech Stack

### Machine Learning & Experiment Tracking

* Python
* MLflow
* DagsHub

### Pipeline & Data Versioning

* DVC
* Amazon S3

### Application & Deployment

* Flask
* Docker
* Kubernetes
* Amazon EKS
* Amazon ECR

### Automation

* GitHub Actions

### Monitoring

* Prometheus
* Grafana

---

# 📂 Project Structure

```text
.
├── src/
│   ├── logger/
│   ├── data_ingestion.py
│   ├── data_preprocessing.py
│   ├── feature_engineering.py
│   ├── model_building.py
│   ├── model_evaluation.py
│   └── register_model.py
│
├── flask_app/
├── tests/
├── scripts/
│
├── .github/
│   └── workflows/
│       └── ci.yaml
│
├── dvc.yaml
├── params.yaml
├── requirements.txt
├── Dockerfile
└── README.md
```

---

# 🚀 Getting Started

## 1. Clone the Repository

```bash
git clone <your-repository-url>
cd <repository-name>
```

## 2. Create and Activate the Environment

```bash
conda create -n atlas python=3.10
conda activate atlas
```

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

## 4. Run the Pipeline

```bash
dvc repro
```

---

# 🔐 Security

Sensitive information such as authentication tokens and cloud credentials should never be committed to the repository.

The project uses environment variables and repository secrets for managing sensitive configuration during automated workflows.

---

# 🌱 Future Improvements

Possible future extensions include:

* [ ] Automated model retraining
* [ ] Data and model drift detection
* [ ] Automated monitoring alerts
* [ ] Model performance tracking in production
* [ ] Kubernetes autoscaling
* [ ] Infrastructure as Code
* [ ] Advanced deployment strategies such as blue-green or canary deployments

---

# 🎓 Key Learnings

This project helped me understand that deploying a machine learning model involves much more than training and evaluating it.

Through this project, I explored how different components of the MLOps ecosystem work together to support a complete ML lifecycle—from experimentation and reproducibility to deployment and monitoring.

The project represents my hands-on effort to build a **sentiment analysis system using production-oriented MLOps practices**.

---

## 👨‍💻 Author

**S Singh**

Aspiring Machine Learning / Applied Science Engineer with an interest in building reliable, scalable, and production-oriented machine learning systems.
