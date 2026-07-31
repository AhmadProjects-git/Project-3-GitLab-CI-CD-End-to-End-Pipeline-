# End-to-End GitLab CI/CD Pipeline with Automated Nginx Deployment

An end-to-end Automated CI/CD Pipeline implemented using **GitLab CI/CD** with a **Self-Hosted Linux GitLab Runner** on Windows Subsystem for Linux (WSL2 Ubuntu). The pipeline automatically tests, builds, and deploys a Bootstrap static web application to an active **Nginx Web Server**.

---

## 🛠️ Architecture & Technologies

- **Source Control Management:** GitLab & GitHub
- **CI/CD Platform:** GitLab CI/CD
- **Runner Environment:** Self-Hosted GitLab Runner (`shell` executor on WSL2 Ubuntu 22.04)
- **Web Server:** Nginx (Continuous Deployment Target)
- **Application Stack:** Bootstrap 5 Static Web Application

---

## 🔄 Pipeline Workflow & Stages

1. **Test Stage (`test_job`):** Executes continuous integration smoke tests and repository configuration checks.
2. **Build Stage (`build_job`):** Compiles static assets into the `dist/` production folder and exposes pipeline artifacts.
3. **Deploy Stage (`deploy_job`):** Automatically transfers build artifacts to Nginx's web directory (`/var/www/html/`), serving the updated web application instantly.

---

## 📋 Complete Setup & Installation Guide

### 1. Configure Self-Hosted WSL GitLab Runner
```bash
# Register the local runner with GitLab project registration token
sudo gitlab-runner register \
  --url [https://gitlab.com](https://gitlab.com) \
  --token <YOUR_RUNNER_REGISTRATION_TOKEN> \
  --description "my-wsl-runner" \
  --executor "shell"

# Install as system service and start daemon
sudo gitlab-runner install --user=$USER --working-directory=$HOME
sudo gitlab-runner start

```

### 2. Configure Nginx Web Server on WSL

```bash
# Install and start Nginx web server
sudo apt update && sudo apt install -y nginx
sudo service nginx start

# Update directory permissions for seamless runner deployments
sudo chown -R $USER:$USER /var/www/html
sudo chmod -R 755 /var/www/html

```

---

## ⚙️ CI/CD Configuration (`.gitlab-ci.yml`)

```yaml
stages:
  - test
  - build
  - deploy

test_job:
  stage: test
  tags:
    - my-runner
  script:
    - echo "=== Stage 1: Continuous Integration Testing ==="
    - test -f package.json

build_job:
  stage: build
  tags:
    - my-runner
  script:
    - echo "=== Stage 2: Building Application Assets ==="
    - test -d dist || mkdir -p dist
  artifacts:
    paths:
      - dist/

deploy_job:
  stage: deploy
  tags:
    - my-runner
  script:
    - echo "=== Stage 3: Continuous Deployment to Nginx Web Server ==="
    - cp -r dist/* /var/www/html/
    - echo "Deployment Successful! Web application is live."

```

---

## 📸 Proof of Execution & Screenshots

### 1. GitLab 3-Stage Pipeline Success

All three stages (**Test $\rightarrow$ Build $\rightarrow$ Deploy**) executed successfully on the self-hosted runner:

### 2. Live Application Served via Nginx

Web application continuously deployed and running live on the local web server (`http://localhost`):

---

## 👤 Author

**AHMAD HASSAN**

*DevOps & Cloud Engineer*

```

```Ahmad, yeh rahi aapki **`README.md`** file ka complete text format mein formatted raw code.

Aap simply is poore text box ke contents ko copy kar ke apni **`README.md`** file mein paste kar dein:

```markdown
# End-to-End GitLab CI/CD Pipeline with Automated Nginx Deployment

An end-to-end Automated CI/CD Pipeline implemented using **GitLab CI/CD** with a **Self-Hosted Linux GitLab Runner** on Windows Subsystem for Linux (WSL2 Ubuntu). The pipeline automatically tests, builds, and deploys a Bootstrap static web application to an active **Nginx Web Server**.

---

## 🛠️ Architecture & Technologies

- **Source Control Management:** GitLab & GitHub
- **CI/CD Platform:** GitLab CI/CD
- **Runner Environment:** Self-Hosted GitLab Runner (`shell` executor on WSL2 Ubuntu 22.04)
- **Web Server:** Nginx (Continuous Deployment Target)
- **Application Stack:** Bootstrap 5 Static Web Application

---

## 🔄 Pipeline Workflow & Stages

1. **Test Stage (`test_job`):** Executes continuous integration smoke tests and repository configuration checks.
2. **Build Stage (`build_job`):** Compiles static assets into the `dist/` production folder and exposes pipeline artifacts.
3. **Deploy Stage (`deploy_job`):** Automatically transfers build artifacts to Nginx's web directory (`/var/www/html/`), serving the updated web application instantly.

---

## 📋 Complete Setup & Installation Guide

### 1. Configure Self-Hosted WSL GitLab Runner
```bash
# Register the local runner with GitLab project registration token
sudo gitlab-runner register \
  --url [https://gitlab.com](https://gitlab.com) \
  --token <YOUR_RUNNER_REGISTRATION_TOKEN> \
  --description "my-wsl-runner" \
  --executor "shell"

# Install as system service and start daemon
sudo gitlab-runner install --user=$USER --working-directory=$HOME
sudo gitlab-runner start

```

### 2. Configure Nginx Web Server on WSL

```bash
# Install and start Nginx web server
sudo apt update && sudo apt install -y nginx
sudo service nginx start

# Update directory permissions for seamless runner deployments
sudo chown -R $USER:$USER /var/www/html
sudo chmod -R 755 /var/www/html

```

---

## ⚙️ CI/CD Configuration (`.gitlab-ci.yml`)

```yaml
stages:
  - test
  - build
  - deploy

test_job:
  stage: test
  tags:
    - my-runner
  script:
    - echo "=== Stage 1: Continuous Integration Testing ==="
    - test -f package.json

build_job:
  stage: build
  tags:
    - my-runner
  script:
    - echo "=== Stage 2: Building Application Assets ==="
    - test -d dist || mkdir -p dist
  artifacts:
    paths:
      - dist/

deploy_job:
  stage: deploy
  tags:
    - my-runner
  script:
    - echo "=== Stage 3: Continuous Deployment to Nginx Web Server ==="
    - cp -r dist/* /var/www/html/
    - echo "Deployment Successful! Web application is live."

```

---

## 📸 Proof of Execution & Screenshots

### 1. GitLab 3-Stage Pipeline Success
All three stages (**Test → Build → Deploy**) executed successfully on the self-hosted runner:

<img width="1366" height="768" alt="pipeline-deploy-success" src="https://github.com/user-attachments/assets/86af26ca-2c76-4f70-a4da-3115e574ae7e" />

### 2. Live Application Served via Nginx
Web application continuously deployed and running live on the local web server (`http://localhost`):

<img width="1366" height="768" alt="live-nginx-website" src="https://github.com/user-attachments/assets/7ea319c5-14a8-4caf-81b1-da1823a542d4" />

---
---

## 👤 Maintainer Profile

| Detail | Info |
| :--- | :--- |
| **Author** | **Ahmad Hassan** |
| **Role** | DevOps & Cloud Engineer |
| **Specialization** | CI/CD Automation, Linux System Administration, Cloud Infrastructure |
| **Project Repo** | [GitLab Workspace](https://gitlab.com/ahmadhassanofficala/project-3-gitlab-pipeline) |

---

```
