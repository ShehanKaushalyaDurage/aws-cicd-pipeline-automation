# AWS CI/CD Pipeline Automation (React to EC2)

---

## 📖 Project Overview

This repository contains a simple **CI/CD (Continuous Integration / Continuous Delivery) pipeline** that automatically builds and deploys a **React** application (bundled with Vite) to an **AWS EC2 instance**. It uses **GitHub Actions** to automate the deployment process.

---

## 🚀 How This Project Automates Deployment

1. **Source Control** – Code is hosted on GitHub.
2. **GitHub Actions** – The workflow (`deployement.yml`) runs on every `push` or `pull_request` to the `main` branch.
3. **Build Stage**
   - Sets up Node.js v20.
   - Installs dependencies using `npm ci`.
   - Builds the React application for production using `npm run build` (creating the `dist/` directory).
4. **Deploy Stage**
   - Configures SSH access using GitHub Secrets.
   - Uses `rsync` to securely copy the compiled `dist/` folder to the specified path on your AWS EC2 instance.

---

## 🛠️ Tech Stack

- **Frontend:** React 18, Vite
- **CI/CD:** GitHub Actions
- **Hosting:** AWS EC2 (Amazon Elastic Compute Cloud)
- **Deployment Tool:** `rsync` over SSH

---

## 📦 Prerequisites

To use this CI/CD pipeline, you will need:

1. An **AWS EC2 instance** running (e.g., Ubuntu/Amazon Linux) with a web server (like Nginx or Apache) configured to serve your application.
2. The following **GitHub Secrets** configured in your repository settings (`Settings > Secrets and variables > Actions`):

| Secret Name | Description | Example |
|-------------|-------------|---------|
| `EC2_HOST` | The public IP or domain of your EC2 instance | `54.210.xx.xx` |
| `EC2_USER` | The SSH username for your instance | `ubuntu` or `ec2-user` |
| `EC2_SSH_KEY` | The private SSH key (`.pem` or `.rsa`) to access the instance | `-----BEGIN RSA PRIVATE KEY-----...` |
| `EC2_APP_PATH` | The destination path on the EC2 instance where files should be copied | `/var/www/html/my-app` |

---

## ⚙️ Local Development

1. **Clone the repository**
   ```bash
   git clone https://github.com/shehankaushalya/aws-cicd-pipeline-automation.git
   cd aws-cicd-pipeline-automation
   ```
2. **Install dependencies**
   ```bash
   npm install
   ```
3. **Run the local development server**
   ```bash
   npm run dev
   ```
4. **Build for production manually**
   ```bash
   npm run build
   ```

---

## ✉️ Contact & Contributions

- **Author:** Shehan Kaushalya Durage
- **GitHub:** https://github.com/shehankaushalya/aws-cicd-pipeline-automation

Contributions are welcome! Open an issue or submit a PR.
