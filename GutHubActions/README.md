# DSO101 Assignment 3 – GitHub Actions CI/CD Pipeline

**Student ID:** 02250355  
**Repository:** `KinleyTshering_02250355_DSO101_A1`  
**Docker Hub:** [`kyserl11/todo-app`](https://hub.docker.com/r/kyserl11/todo-app)

---

## Overview

This repository includes a GitHub Actions CI/CD pipeline that automatically builds and pushes a Docker image to Docker Hub, then triggers a redeployment of the application on Render — whenever code is pushed to the `main` branch.

---

## Application Stack

| Layer     | Technology              |
|-----------|-------------------------|
| Frontend  | React 18.2.0            |
| Backend   | Node.js / Express       |
| Database  | PostgreSQL (Render)     |
| Container | Docker                  |

---

## Live Deployments

| Service  | URL |
|----------|-----|
| Frontend | https://fe-todo-674p.onrender.com |
| Backend  | https://be-todo.onrender.com |

---

## CI/CD Workflow

**File:** `.github/workflows/deploy.yml`

### Trigger

The pipeline runs automatically on every push to the `main` branch.

```yaml
on:
  push:
    branches:
      - main
```

### Pipeline Stages

```
Push to main
     │
     ▼
┌─────────────────────┐
│  1. Checkout Code   │  Clones the repository
└─────────────────────┘
     │
     ▼
┌─────────────────────┐
│  2. Docker Login    │  Authenticates with Docker Hub using secrets
└─────────────────────┘
     │
     ▼
┌─────────────────────┐
│  3. Build Image     │  Builds Docker image tagged as latest
└─────────────────────┘
     │
     ▼
┌─────────────────────┐
│  4. Push to Hub     │  Pushes kyserl11/todo-app:latest to Docker Hub
└─────────────────────┘
     │
     ▼
┌─────────────────────┐
│  5. Render Deploy   │  Triggers redeployment via Render Deploy Hook
└─────────────────────┘
```

---

## Repository Secrets Required

The following secrets must be configured in **GitHub → Settings → Secrets and variables → Actions**:

| Secret Name           | Description                          |
|-----------------------|--------------------------------------|
| `DOCKER_USERNAME`     | Docker Hub username (`kyserl11`)     |
| `DOCKER_PASSWORD`     | Docker Hub password or access token  |
| `RENDER_DEPLOY_HOOK`  | Render deploy hook URL               |

---

## How to Use

### 1. Clone the Repository

```bash
git clone https://github.com/kinleyy-17/KinleyTshering_02250355_DSO101_A1.git
cd KinleyTshering_02250355_DSO101_A1
```

### 2. Set Up Secrets

Go to your GitHub repository → **Settings** → **Secrets and variables** → **Actions**, and add the secrets listed above.

### 3. Push to Trigger the Pipeline

```bash
git add .
git commit -m "your commit message"
git push origin main
```

The GitHub Actions workflow will automatically run and deploy your changes.

### 4. Monitor the Workflow

Go to your repository on GitHub → **Actions** tab to see the workflow run in real time.

---

## Docker Image

The Docker image is publicly available on Docker Hub:

```bash
# Pull the latest image
docker pull kyserl11/todo-app:latest

# Run the container locally
docker run -p 3000:3000 kyserl11/todo-app:latest
```

---

## Project Structure

```
KinleyTshering_02250355_DSO101_A1/
├── .github/
│   └── workflows/
│       └── deploy.yml        # GitHub Actions workflow
├── frontend/                 # React application
│   ├── src/
│   ├── public/
│   └── package.json
├── backend/                  # Node.js / Express API
│   ├── src/
│   └── package.json
├── Dockerfile                # Docker build configuration
└── README.md
```

---

## Related Assignments

| Assignment | Description                              |
|------------|------------------------------------------|
| A1         | Full-stack Todo app with Docker & Render |
| A2         | Jenkins CI/CD pipeline (5-stage)         |
| **A3**     | **GitHub Actions workflow** ← This repo |

---

## Author

**Kinley** | Student ID: `02250355` | DSO101 