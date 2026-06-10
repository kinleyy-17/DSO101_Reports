# DSO101 Assignment 1 – Dockerized Full-Stack Todo App

**Student:** Kinley Tshering  
**Student ID:** 02250355  
**Module:** DSO101 – Continuous Integration and Continuous Deployment  
**Submission Date:** 12th March  

---

## 📌 Overview

This assignment involves building a full-stack Todo List web application and deploying it using Docker and Render.com. The application consists of:

- **Frontend (FE):** React.js – UI for adding, editing, and deleting tasks
- **Backend (BE):** Node.js + Express – RESTful CRUD API
- **Database (DB):** PostgreSQL – Data persistence

---

## 🛠️ Tech Stack

| Layer     | Technology          |
|-----------|---------------------|
| Frontend  | React.js            |
| Backend   | Node.js + Express   |
| Database  | PostgreSQL          |
| Container | Docker              |
| Registry  | Docker Hub          |
| Hosting   | Render.com          |

---

## 📁 Repository Structure

```
KinleyTshering_02250355_DSO101_A1/
├── frontend/
│   ├── Dockerfile
│   ├── .env.production
│   └── src/
├── backend/
│   ├── Dockerfile
│   ├── .env.production
│   └── server.js
└── render.yaml
```

---

## 🐳 Docker Setup

### Backend Dockerfile

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 5000
CMD ["node", "server.js"]
```

### Build & Push Commands

```bash
# Backend
docker build -t kyserl11/be-todo:02250355 ./backend
docker push kyserl11/be-todo:02250355

# Frontend
docker build -t kyserl11/todo-app:02250355 ./frontend
docker push kyserl11/todo-app:02250355
```

---

## 🚀 Deployment

### Part A – Pre-built Image Deployment on Render

1. Go to [Render.com](https://render.com) → **New Web Service**
2. Select **Existing Image from Docker Hub**
3. Enter image: `kyserl11/be-todo:02250355`
4. Add environment variables:
   - `DB_HOST`, `DB_USER`, `DB_PASSWORD`, `PORT=5000`
5. Repeat for frontend with `REACT_APP_API_URL=https://be-todo.onrender.com`

### Part B – Automated Build via render.yaml

The `render.yaml` blueprint enables automatic builds on every Git push.

```yaml
services:
  - type: web
    name: be-todo
    env: docker
    dockerfilePath: ./backend/Dockerfile
    envVars:
      - key: DB_HOST
        value: your-render-db-host
      - key: PORT
        value: 5000

  - type: web
    name: fe-todo
    env: docker
    dockerfilePath: ./frontend/Dockerfile
    envVars:
      - key: REACT_APP_API_URL
        value: https://be-todo.onrender.com
```

---

## 🌐 Live URLs

| Service  | URL |
|----------|-----|
| Frontend | https://fe-todo-674p.onrender.com |
| Backend  | https://be-todo.onrender.com |

---

## 📸 Screenshots

> Screenshots of the following are included below:
> - Docker Hub image pushed with student ID tag
> - Render.com Part A deployment (pre-built image)
> - Render.com Part B deployment (automated build)
> - Live app running in browser

---

## ⚙️ Environment Variables

> ⚠️ `.env` files are **not** committed to Git. They are added to `.gitignore`.

**Backend `.env`:**
```
DB_HOST=your-render-db-host
DB_USER=render_db_user
DB_PASSWORD=your_db_password
PORT=5000
```

**Frontend `.env`:**
```
REACT_APP_API_URL=https://be-todo.onrender.com
```

---

## 🧩 Challenges Faced

- Configuring `render.yaml` correctly (file placement, unsupported `buildArgs`, correct `dockerContext` paths)
- Setting up environment variables for both services on Render
- Ensuring the frontend correctly points to the live backend URL

---

## 📚 Learning Outcomes

- Learned how to containerize a multi-service application using Docker
- Gained experience pushing images to Docker Hub with versioned tags
- Understood how to deploy pre-built and auto-built images on Render.com
- Practiced using environment variables securely in both development and production

---

## 🔗 References

- [Docker Documentation](https://docs.docker.com/)
- [Render Documentation](https://render.com/docs)
- [Render Blueprint Spec](https://render.com/docs/blueprint-spec)