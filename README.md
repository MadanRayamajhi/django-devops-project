# Django DevOps Project

A production-ready Django application delivered with a complete DevOps workflow: containerization, CI/CD, Kubernetes deployment, and infrastructure automation.

## Project Summary

This repository contains a Django backend with:
- Docker Compose for local development and PostgreSQL service orchestration
- A Dockerfile for containerized production builds
- Kubernetes manifests for deployment, service, and ingress
- Jenkins pipeline automation for build, test, and deployment
- Terraform infrastructure code targeting AWS
- Nginx proxy configuration for reverse proxy routing

## Repository Layout

- `backend/` — Django project source, `requirements.txt`, and `Dockerfile`
- `docker-compose.yml` — local service composition for backend and Postgres
- `k8s/` — Kubernetes manifests (`deployment.yaml`, `service.yaml`, `ingress.yaml`)
- `jenkins/` + `Jenkinsfile` — CI/CD pipeline configuration
- `terraform/` — infrastructure-as-code definitions
- `nginx/nginx.conf` — reverse proxy configuration

## Tech Stack

- Python 3.12
- Django 5.0
- Django REST Framework
- PostgreSQL 15
- Gunicorn
- Docker / Docker Compose
- Kubernetes
- Jenkins
- Terraform
- Nginx

## Prerequisites

- Git
- Docker and Docker Compose
- Kubernetes CLI (`kubectl`) and access to a cluster
- Jenkins for CI/CD
- Terraform
- Python 3.12

## Quick Start

Clone the repository:

```bash
git clone https://github.com/MadanRayamajhi/django-devops-project.git
cd django-devops-project
```

### Run locally with Docker Compose

```bash
docker-compose up --build
```

The backend will be available on `http://localhost:8000`.

### Run the Django app locally

```bash
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install -r backend/requirements.txt
cd backend
python manage.py migrate
python manage.py runserver
```

## Testing

Execute the Django test suite:

```bash
cd backend
python manage.py test
```

## Kubernetes Deployment

Deploy Kubernetes resources:

```bash
kubectl apply -f k8s/
```

Verify status:

```bash
kubectl get pods
kubectl get svc
kubectl get ingress
```

## Jenkins CI/CD

The pipeline in `Jenkinsfile` includes:
- source checkout from GitHub
- Docker image build
- container run and health check
- automated success/failure reporting

Update Jenkins credentials and pipeline configuration as needed for your environment.

## Terraform Infrastructure

Provision infrastructure with Terraform:

```bash
cd terraform
terraform init
terraform plan
terraform apply
```

The current Terraform configuration includes an AWS EC2 instance resource for Jenkins.

## Notes

- The Django backend is served by Gunicorn in the container image: `CMD ["gunicorn", "config.wsgi:application", "--bind", "0.0.0.0:8000"]`
- Kubernetes manifests include a load-balanced service and ingress rule for `django.example.com`.
- `docker-compose.yml` creates a Postgres service with `devopsdb`, `admin`, and password `password`.

## Contributing

1. Fork the repository
2. Create a branch: `git checkout -b feature/name`
3. Commit your changes
4. Push and open a pull request

## License

MIT License.
