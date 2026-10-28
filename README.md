# CI/CD Pipeline — Flask, Docker, GHCR & AWS EC2

## Project Overview

This project demonstrates an automated CI pipeline for a Python Flask application using GitHub Actions and Docker, with image publishing to GitHub Container Registry (GHCR) and manual deployment to AWS EC2.

## Technologies Used

- **Python & Flask** — Web application
- **Pytest** — Automated testing
- **Docker** — Application containerization
- **GitHub Actions** — Automated CI pipeline
- **GHCR** — Docker image registry
- **AWS EC2 & Ubuntu** — Cloud deployment

## Project Implementation

### Step 1 — Create the Flask Application
Developed a simple Flask web application that displays **Hello from DevOps!** on port 5000.

### Step 2 — Add Automated Tests
Created `test_app.py` using Pytest to verify the application's HTTP response and status code.

### Step 3 — Dockerize the Application
Created a `Dockerfile` and `requirements.txt`, then built and tested the Docker image locally.

```bash
docker build -t flask-cicd:v1 .
docker run -d -p 5000:5000 flask-cicd:v1
```

### Step 4 — Configure GitHub Actions CI
Created `.github/workflows/ci.yml` to automatically:

1. Checkout the repository.
2. Set up Python and install dependencies.
3. Run Pytest.
4. Build the Docker image.
5. Authenticate with GHCR.
6. Publish the Docker image to GHCR.

The pipeline runs on every push to the `main` branch.

### Step 5 — Publish the Image to GHCR
The Docker image is automatically published to:

```text
ghcr.io/jyothisjose9a/automated-cicd-pipeline:latest
```

### Step 6 — Deploy to AWS EC2
Launched an Ubuntu EC2 instance, configured a security group, connected using SSH, and installed Docker.

Downloaded the published image:

```bash
sudo docker pull ghcr.io/jyothisjose9a/automated-cicd-pipeline:latest
```

Started the application:

```bash
sudo docker run -d \
  --name flask-cicd \
  -p 5000:5000 \
  ghcr.io/jyothisjose9a/automated-cicd-pipeline:latest
```

### Step 7 — Verify Deployment
Tested the running application using:

```bash
curl http://localhost:5000
```

The application can also be accessed through the EC2 public IP on port 5000 when the security group permits access.

## CI/CD Workflow

```text
Git Push
   ↓
GitHub Actions
   ↓
Pytest → Docker Build
   ↓
Publish Image to GHCR
   ↓
Manual Docker Pull on AWS EC2
   ↓
Run Flask Container
```

## Key Learnings

- Automated application testing and Docker image building using GitHub Actions.
- Published container images to GHCR.
- Deployed a prebuilt Docker image to AWS EC2.
- Configured Linux, SSH, Docker, and AWS networking.

**Note:** CI and GHCR publishing are automated. Deployment to EC2 is manual.


