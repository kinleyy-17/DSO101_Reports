# DSO101 Assignment 3 – GitHub Actions CI/CD Pipeline

**Student:** Kinley Tshering  
**Student ID:** 02250355  
**Module:** DSO101 – Continuous Integration and Continuous Deployment  
**Submission Date:** 29th April  

---

## 📌 Overview

This assignment configures a **GitHub Actions** workflow to automate:

1. Building a Docker image for the Todo application
2. Pushing the image to **Docker Hub**
3. Triggering an automatic redeployment on **Render.com** via a deploy webhook

---

## 🛠️ Tools & Technologies

| Tool           | Purpose                        |
|----------------|--------------------------------|
| GitHub         | Source code hosting            |
| GitHub Actions | CI/CD automation               |
| Docker         | Containerization               |
| Docker Hub     | Container image registry       |
| Render.com     | Cloud deployment               |
| Node.js / npm  | Backend runtime                |
| Jest           | Testing framework              |

---

## 📁 Repository Structure

```
KinleyTshering_02250355_DSO101_A1/
├── frontend/
│   ├── Dockerfile
│   └── src/
├── backend/
│   ├── Dockerfile
│   └── server.js
└── .github/
    └── workflows/
        └── deploy.yml
```

---

## 🔐 GitHub Secrets Configuration

The following secrets must be added under **Settings → Secrets and Variables → Actions**:

| Secret Name          | Description                          |
|----------------------|--------------------------------------|
| `DOCKERHUB_USERNAME` | Your Docker Hub username             |
| `DOCKERHUB_TOKEN`    | Docker Hub Personal Access Token     |
| `RENDER_DEPLOY_HOOK` | Render.com deploy webhook URL        |

> ⚠️ **Never hardcode credentials in your code or workflow files.**

---

## 📄 GitHub Actions Workflow

**File:** `.github/workflows/deploy.yml`

```yaml
on:
  push:
    branches: ["main"]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      # 1. Checkout code
      - name: Checkout Repository
        uses: actions/checkout@v4

      # 2. Login to DockerHub
      - name: Login to DockerHub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}

      # 3. Build & Push Docker Image
      - name: Build and Push Docker Image
        run: |
          docker build -t ${{ secrets.DOCKERHUB_USERNAME }}/todo-app:latest .
          docker push ${{ secrets.DOCKERHUB_USERNAME }}/todo-app:latest

      # 4. Trigger Render Redeployment
      - name: Trigger Render Deployment
        run: curl -X POST ${{ secrets.RENDER_DEPLOY_HOOK }}
```

---

## 🐳 Dockerfile (Backend Example)

```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

---

## 🚀 How It Works

1. A `git push` to the `main` branch triggers the GitHub Actions workflow
2. The workflow checks out the code on an `ubuntu-latest` runner
3. It logs into Docker Hub using stored secrets
4. Builds the Docker image and pushes it tagged as `latest`
5. Sends a POST request to the Render deploy webhook, triggering a redeployment

---

## 🌐 Live Deployment

| Service  | URL |
|----------|-----|
| Frontend | https://fe-todo-674p.onrender.com |
| Backend  | https://be-todo.onrender.com |

---

## 🧩 Challenges Faced

- Render does not automatically redeploy when a new Docker image is pushed to Docker Hub — solved by adding a `curl` call to the Render deploy webhook in the workflow
- A Docker Personal Access Token was accidentally committed to the repository, triggering a GitHub push protection block — resolved by creating an orphan branch and force pushing; the leaked token was subsequently revoked on Docker Hub

---

## 📚 Learning Outcomes

- Learned to write GitHub Actions workflows using YAML syntax
- Understood how to securely manage credentials using GitHub Secrets
- Gained experience integrating Docker Hub and Render.com into an automated CI/CD pipeline
- Understood the importance of secret hygiene and how to recover from credential leaks

---

## 🔗 References

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [docker/login-action](https://github.com/docker/login-action)
- [Render Deploy Hooks](https://render.com/docs/deploy-hooks)
- [Docker Hub](https://hub.docker.com/)