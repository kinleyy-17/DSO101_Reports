# DSO101 Assignment 2 – Jenkins CI/CD Pipeline

**Student:** Kinley Tshering  
**Student ID:** 02250355  
**Module:** DSO101 – Continuous Integration and Continuous Deployment  
**Submission Date:** 25th March  

---

## 📌 Overview

This assignment configures a **Jenkins CI/CD pipeline** to automate the build, test, and deployment of the Todo List application from Assignment 1. The pipeline runs on a local Jenkins server and integrates with GitHub and Docker Hub.

---

## 🛠️ Tools & Technologies

| Tool         | Purpose                          |
|--------------|----------------------------------|
| Jenkins      | CI/CD automation (localhost:8080)|
| GitHub       | Source code hosting              |
| Node.js/npm  | JavaScript runtime & packages    |
| Jest         | Unit testing framework           |
| jest-junit   | JUnit report generation          |
| Docker       | Containerization & deployment    |

---

## ⚙️ Jenkins Setup

### 1. Install Jenkins
- Downloaded from [jenkins.io/download](https://www.jenkins.io/download/)
- Running on: `http://localhost:8080`

### 2. Plugins Installed
- NodeJS Plugin
- Pipeline
- GitHub Integration
- Docker Pipeline

### 3. Node.js Configuration
- Manage Jenkins → Tools → NodeJS
- Added Node.js LTS v20.x

### 4. GitHub Credentials
- Manage Jenkins → Credentials → Add
- Type: Username & Password
- Username: GitHub username
- Password: GitHub Personal Access Token (PAT)

---

## 📁 Repository Structure

```
KinleyTshering_02250355_DSO101_A1/
├── backend/
│   ├── package.json
│   ├── server.js
│   └── ...
├── frontend/
│   └── ...
└── Jenkinsfile
```

---

## 🔧 Pipeline Stages

The pipeline consists of **5 stages**:

| Stage | Description |
|-------|-------------|
| 1. Checkout | Clone repository from GitHub |
| 2. Install Dependencies | Run `npm install` |
| 3. Build | Run `npm run build` |
| 4. Test | Run Jest tests + generate JUnit report |
| 5. Deploy | Build & push Docker image to Docker Hub |

---

## 📄 Jenkinsfile

```groovy
pipeline {
    agent any
    tools {
        nodejs 'NodeJS'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/kinleyy-17/KinleyTshering_02250355_DSO101_A1.git'
            }
        }
        stage('Install') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
            post {
                always {
                    junit 'junit.xml'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    docker.build('kyserl11/todo-app:latest')
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-creds') {
                        docker.image('kyserl11/todo-app:latest').push()
                    }
                }
            }
        }
    }
}
```

---

## 🧪 Testing Setup

### Install Jest and jest-junit

```bash
npm install --save-dev jest jest-junit
```

### package.json scripts

```json
{
  "scripts": {
    "test": "jest --ci --reporters=default --reporters=jest-junit",
    "build": "react-scripts build"
  }
}
```

## 🧩 Challenges Faced

- Plugin installation failures due to campus network restrictions
- Git history bloat from committed `node_modules` — resolved by creating a clean repo
- Jenkinsfile corruption and file casing issues on Windows
- React 19 / react-scripts incompatibility — resolved by downgrading to React 18.2.0 and react-scripts 5.0.1
- Setting up jest-junit for proper JUnit XML report generation

---

## 📚 Learning Outcomes

- Gained hands-on experience setting up a local Jenkins CI/CD server
- Learned to configure multi-stage pipelines using Jenkinsfile (declarative syntax)
- Understood how to integrate GitHub credentials and Docker Hub in Jenkins
- Practiced unit testing with Jest and publishing test reports in Jenkins

---

## 🔗 References

- [Jenkins Documentation](https://www.jenkins.io/doc/)
- [Jest Documentation](https://jestjs.io/docs/getting-started)
- [jest-junit](https://github.com/jest-community/jest-junit)
- [Docker Pipeline Plugin](https://plugins.jenkins.io/docker-workflow/)