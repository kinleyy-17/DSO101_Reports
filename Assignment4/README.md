# DSO101 Assignment 4 – Deploy Your First Web App using GitHub & Render

**Student:** Kinley Tshering  
**Student ID:** 02250355  
**Module:** DSO101 – Continuous Integration and Continuous Deployment  
**Submission Date:** 13th May  

---

## 📌 Overview

This assignment demonstrates the basics of deploying a web application using:

- **Git & GitHub** – Version control and source hosting
- **GitHub Actions** – CI/CD automation
- **Render** – Cloud deployment

The project uses **Option A** – a static HTML/CSS website deployed as a Render Static Site.

---

## 🛠️ Tools & Technologies

| Tool            | Purpose              |
|-----------------|----------------------|
| GitHub          | Source code hosting  |
| GitHub Actions  | CI/CD automation     |
| Render          | Web app deployment   |

---

## 📁 Repository Structure

```
KinleyTshering_02250355_DSO101_A4/
├── index.html
├── style.css
├── README.md
└── .github/
    └── workflows/
        └── deploy.yml
```

---

## 🖥️ Application

A simple static website built with HTML and CSS.

**index.html**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>My First DevOps App</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <h1>Hello DevOps!</h1>
  <p>Deployed using GitHub Actions and Render.</p>
</body>
</html>
```

---

## 🔄 CI/CD Workflow

**File:** `.github/workflows/deploy.yml`

```yaml
name: Deploy to Render

on:
  push:
    branches: [ "main" ]

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Dummy step
        run: echo "Code pushed successfully!"
```

This workflow triggers automatically on every push to the `main` branch. Render picks up the new commit and redeploys the site automatically.

---

## 🚀 Deployment Steps

### Step 1 – Set Up GitHub Repository

```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin <repo-url>
git push -u origin main
```

### Step 2 – Enable GitHub Actions

- Go to the **Actions** tab in your GitHub repository
- The workflow at `.github/workflows/deploy.yml` will run automatically on push

### Step 3 – Deploy on Render

1. Go to [render.com](https://render.com) and sign in with GitHub
2. Click **New → Static Site**
3. Connect your GitHub repository
4. Configure:
   - **Build Command:** *(leave empty for plain HTML)*
   - **Publish Directory:** `.`
5. Click **Create Static Site**

---

## 🌐 Live Deployment

| Service | URL |
|---------|-----|
| Live App | *(add your Render URL here)* |

---

## 🧩 Challenges Faced

- Understanding how Render automatically detects and deploys static sites from a connected GitHub repo
- Configuring the correct publish directory for a plain HTML project

---

## 📚 Learning Outcomes

- Understood the fundamentals of Git version control and GitHub repository setup
- Learned to write a basic GitHub Actions workflow
- Gained experience deploying a static site on Render.com
- Understood the end-to-end CI/CD flow: code push → Actions run → Render redeploy

---

## 🔗 References

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Render Static Sites](https://render.com/docs/static-sites)
- [Git Documentation](https://git-scm.com/doc)