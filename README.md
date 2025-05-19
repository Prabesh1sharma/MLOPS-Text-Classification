# 🚀 End-to-End MLOps Pipeline with Kubernetes Deployment

[![Python](https://img.shields.io/badge/Python-3.10-blue.svg)](https://www.python.org/)
[![Docker](https://img.shields.io/badge/Docker-Container-blue.svg)](https://www.docker.com/)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-EKS-orange.svg)](https://kubernetes.io/)
[![AWS](https://img.shields.io/badge/AWS-Cloud-yellow.svg)](https://aws.amazon.com/)
[![MLflow](https://img.shields.io/badge/MLflow-Tracking-green.svg)](https://mlflow.org/)
[![DVC](https://img.shields.io/badge/DVC-Pipeline-purple.svg)](https://dvc.org/)

> **A production-ready MLOps pipeline featuring automated CI/CD, containerized deployment, Kubernetes orchestration, and comprehensive monitoring.**

## 🎯 Project Overview

This project demonstrates a complete MLOps lifecycle implementation, from data ingestion to production deployment. It showcases industry best practices for machine learning operations, including automated testing, containerization, orchestration, and monitoring.

### 🏗️ Architecture

```
Data Source → DVC Pipeline → Model Training → MLflow Tracking → 
Docker Container → ECR Repository → EKS Cluster → Prometheus Monitoring → 
Grafana Visualization
```

## ✨ Key Features

- **🔄 Automated ML Pipeline**: DVC-powered reproducible data science workflows
- **📊 Experiment Tracking**: MLflow integration with DagHub for experiment management
- **🐳 Containerization**: Docker-based application packaging for consistency
- **☸️ Kubernetes Deployment**: AWS EKS for scalable, production-ready hosting
- **🔧 CI/CD Pipeline**: GitHub Actions for automated testing and deployment
- **📈 Monitoring**: Prometheus & Grafana integration for real-time insights
- **☁️ Cloud Storage**: S3 for data versioning and artifact storage

## 🛠️ Technology Stack

### Core Technologies
- **Python 3.10** - Programming language
- **Flask** - Web framework for model serving
- **Docker** - Containerization platform
- **Kubernetes (EKS)** - Container orchestration

### MLOps Tools
- **DVC** - Data version control and pipeline management
- **MLflow** - Experiment tracking and model registry
- **DagHub** - Collaborative MLflow hosting

### Cloud & Infrastructure
- **AWS EKS** - Managed Kubernetes service
- **AWS ECR** - Container registry
- **AWS S3** - Object storage for data and artifacts
- **AWS EC2** - Virtual machines for monitoring

### Monitoring & Observability
- **Prometheus** - Metrics collection and monitoring
- **Grafana** - Visualization and dashboards

### CI/CD
- **GitHub Actions** - Automated workflows and deployment

## 🚀 Quick Start

### Prerequisites

```bash
# Clone the repository
git clone <your-repo-url>
cd <repo-name>

# Create and activate virtual environment
conda create -n atlas python=3.10
conda activate atlas

# Install dependencies
pip install -r requirements.txt
```

### Local Development

```bash
# Initialize DVC
dvc init

# Run the ML pipeline
dvc repro

# Start the Flask application
cd flask_app
python app.py
```

### Docker Deployment

```bash
# Build Docker image
docker build -t capstone-app:latest .

# Run container
docker run -p 8888:3000 -e CAPSTONE_TEST=Secret_key capstone-app:latest
```

## 📊 ML Pipeline Stages

The project implements a complete ML pipeline using DVC:

1. **Data Ingestion** - Automated data collection and validation
2. **Data Preprocessing** - Cleaning, normalization, and transformation
3. **Feature Engineering** - Feature extraction and selection
4. **Model Building** - Training with hyperparameter optimization
5. **Model Evaluation** - Performance metrics and validation
6. **Model Registration** - Versioning and deployment preparation

```bash
# Run specific pipeline stage
dvc repro <stage-name>

# Check pipeline status
dvc status

# View pipeline DAG
dvc dag
```

## 🔧 CI/CD Pipeline

The GitHub Actions workflow automates:

- **Code Quality Checks** - Linting and formatting
- **Unit Testing** - Automated test execution
- **Docker Build** - Container image creation
- **ECR Push** - Image registry upload
- **EKS Deployment** - Production deployment
- **Health Checks** - Post-deployment validation

## ☸️ Kubernetes Deployment

### EKS Cluster Setup

```bash
# Create EKS cluster
eksctl create cluster --name flask-app-cluster \
  --region us-east-1 \
  --nodegroup-name flask-app-nodes \
  --node-type t3.small \
  --nodes 1 \
  --managed

# Update kubeconfig
aws eks --region us-east-1 update-kubeconfig --name flask-app-cluster

# Verify cluster
kubectl get nodes
```

### Application Deployment

```bash
# Deploy application
kubectl apply -f k8s/deployment.yaml

# Check deployment status
kubectl get pods
kubectl get svc

# Access application
kubectl get svc flask-app-service
```

## 📈 Monitoring Setup

### Prometheus Configuration

The monitoring stack includes Prometheus for metrics collection and Grafana for visualization.

#### Prometheus Setup (EC2)
```bash
# Download and configure Prometheus
wget https://github.com/prometheus/prometheus/releases/download/v2.46.0/prometheus-2.46.0.linux-amd64.tar.gz
tar -xvzf prometheus-2.46.0.linux-amd64.tar.gz

# Configure targets
sudo nano /etc/prometheus/prometheus.yml

# Start Prometheus
/usr/local/bin/prometheus --config.file=/etc/prometheus/prometheus.yml
```

#### Grafana Setup (EC2)
```bash
# Install Grafana
wget https://dl.grafana.com/oss/release/grafana_10.1.5_amd64.deb
sudo apt install ./grafana_10.1.5_amd64.deb -y

# Start service
sudo systemctl start grafana-server
sudo systemctl enable grafana-server

# Access at http://<ec2-ip>:3000 (admin/admin)
```

## 🔐 Security & Configuration

### Environment Variables

```bash
# Required environment variables
CAPSTONE_TEST=<your-secret-key>
AWS_ACCESS_KEY_ID=<your-access-key>
AWS_SECRET_ACCESS_KEY=<your-secret-key>
AWS_REGION=us-east-1
ECR_REPOSITORY=capstone-proj
AWS_ACCOUNT_ID=<your-account-id>
```

### IAM Permissions

Ensure your AWS user has the following permissions:
- `AmazonEC2ContainerRegistryFullAccess`
- `AmazonEKSClusterPolicy`
- `AmazonEKSWorkerNodePolicy`
- `AmazonS3FullAccess`

## 🧪 Testing

```bash
# Run unit tests
python -m pytest tests/

# Run integration tests
python scripts/integration_tests.py

# Performance testing
python scripts/load_test.py
```

## 📝 Key Learnings & Best Practices

### MLOps Implementation
- ✅ Automated pipeline orchestration with DVC
- ✅ Experiment tracking and model versioning
- ✅ Infrastructure as Code with CloudFormation
- ✅ Containerized microservices architecture

### Cloud Architecture
- ✅ Scalable Kubernetes deployment on EKS
- ✅ Automated CI/CD with GitHub Actions
- ✅ Comprehensive monitoring and alerting
- ✅ Security best practices and secret management

### Performance Optimization
- ✅ Efficient resource utilization with t3.small instances
- ✅ Auto-scaling capabilities
- ✅ Load balancing for high availability

## 🔧 Troubleshooting

### Common Issues

**1. EKS Node Creation Failure**
```bash
# Check fleet request quota
aws service-quotas get-service-quota --service-code ec2 --quota-code L-34B43A08

# Solution: Request quota increase or use different instance types
```

**2. Docker Build Issues**
```bash
# Clear Docker cache
docker system prune -a

# Rebuild with no cache
docker build --no-cache -t capstone-app:latest .
```

**3. Kubectl Context Issues**
```bash
# Reset kubectl context
aws eks --region us-east-1 update-kubeconfig --name flask-app-cluster
```

## 🧹 Resource Cleanup

```bash
# Delete Kubernetes resources
kubectl delete deployment flask-app
kubectl delete service flask-app-service
kubectl delete secret capstone-secret

# Delete EKS cluster
eksctl delete cluster --name flask-app-cluster --region us-east-1

# Verify cleanup
eksctl get cluster --region us-east-1
```

## 📚 Documentation

- [DVC Documentation](https://dvc.org/doc)
- [MLflow Documentation](https://mlflow.org/docs/latest/index.html)
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [AWS EKS User Guide](https://docs.aws.amazon.com/eks/latest/userguide/)


<div align="center">

**If you found this project helpful, I very very thankful to myself**


</div>