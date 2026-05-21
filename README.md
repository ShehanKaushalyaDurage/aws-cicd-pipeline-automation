# AWS CI/CD Pipeline Automation

---

## 📖 Project Overview

This repository contains a **complete CI/CD (Continuous Integration / Continuous Delivery) pipeline** that automatically builds, tests, and deploys a Laravel application to **AWS**.  It is designed to be a learning resource—think of it as a hands‑on classroom where you can see exactly how modern DevOps practices are wired together.

---

## 🛠️ What is CI/CD?

- **Continuous Integration (CI)** – Every time a developer pushes code, the pipeline **instantly builds** the application, runs **unit & integration tests**, and checks code quality.
- **Continuous Delivery (CD)** – After the CI stage succeeds, the same pipeline can **automatically deploy** the verified build to a test or production environment on AWS.
- The goal is to **detect problems early**, keep the codebase **always releasable**, and **remove manual steps** that are error‑prone.

---

## 🚀 How This Project Automates CI/CD to AWS

1. **Source Control** – Code lives in a Git repository (GitHub, GitLab, Bitbucket…).
2. **GitHub Actions / AWS CodePipeline** – The workflow runs on every `push` or `pull‑request`.
3. **Build Stage**
   - Installs PHP, Composer, Node.js, and required extensions.
   - Executes `composer install` and `npm install`.
   - Runs `php artisan test` and `npm run test`.
4. **Package Stage**
   - Archives the Laravel application into a Docker image.
   - Tags the image with the Git SHA.
5. **Push Stage**
   - Pushes the Docker image to **Amazon ECR** (Elastic Container Registry).
6. **Deploy Stage**
   - Updates an **Amazon ECS** service (or **Elastic Beanstalk**) to use the new image.
   - Runs database migrations via `php artisan migrate`.
   - Performs a health‑check to verify the new version is serving traffic.

---

## 📦 Prerequisites

| Tool | Version |
|------|---------|
| Docker | 24.x |
| AWS CLI | 2.x |
| Composer | 2.x |
| Node.js | 20.x |
| Terraform (optional) | 1.6.x |
| Git | any recent version |

You also need an AWS account with the following permissions:
- `ecr:*`
- `ecs:*` (or `elasticbeanstalk:*` if you choose EB)
- `iam:PassRole`
- `cloudformation:*`

---

## 🏗️ Project Structure

```
aws-cicd-pipeline-automation/
├─ .github/                # GitHub Actions workflow files
│   └─ workflows/ci-cd.yml
├─ ecs/                    # ECS task definition & service config
├─ docker/                 # Dockerfile & compose files
├─ scripts/                # Helper scripts (build, deploy, migrate)
├─ src/                    # Your Laravel application code
├─ terraform/              # (optional) Infra‑as‑code for ECR/ECS
└─ README.md               # <-- This file
```

---

## ⚙️ Setup & Local Development

1. **Clone the repository**
   ```bash
   git clone https://github.com/your‑org/aws-cicd-pipeline-automation.git
   cd aws-cicd-pipeline-automation
   ```
2. **Configure AWS credentials**
   ```bash
   aws configure   # enter your Access Key, Secret, region
   ```
3. **Build the Docker image locally**
   ```bash
   docker build -t laravel-app:local .
   ```
4. **Run the app**
   ```bash
   docker compose up -d
   ```
5. **Run tests**
   ```bash
   ./scripts/run-tests.sh
   ```

---

## 📈 Running the CI/CD Pipeline Manually

If you want to trigger the pipeline without a push:

```bash
# Push a temporary tag – GitHub Actions will pick it up
git tag ci-demo-$(date +%s)
git push origin ci-demo-$(date +%s)
```

Or invoke the scripts directly:

```bash
# Build & push Docker image to ECR
./scripts/build-and-push.sh
# Deploy the new image to ECS
./scripts/deploy.sh
```

---

## 🎓 Teaching Points

| Concept | What you’ll learn |
|---------|-------------------|
| **Infrastructure as Code** | Define ECR repo, ECS cluster, and IAM roles in Terraform.
| **GitHub Actions syntax** | Write YAML jobs, matrix builds, and step caching.
| **Docker multi‑stage builds** | Keep images slim by separating build & runtime layers.
| **Zero‑downtime deployments** | Use ECS rolling updates and health‑checks.
| **Secrets management** | Store AWS keys in GitHub secrets, reference them securely.
| **Automated testing** | Integrate PHPUnit and Jest into the pipeline.

---

## 📄 License

This project is licensed under the **MIT License** – feel free to fork, modify, and use it in your own learning labs.

---

## ✉️ Contact & Contributions

- **Author:** Shehan Kaushalya Durage
- **Email:** <shehan@example.com>
- **GitHub:** https://github.com/shehankaushalya/aws-cicd-pipeline-automation

Contributions are welcome! Open an issue or submit a PR.

---

*Happy coding – may your pipelines always be green!*
