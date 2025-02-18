# CI/CD Pipelines Documentation

This repository contains **CI/CD pipelines** for automating **code validation, infrastructure deployment, and security checks**. The following GitHub Actions workflows have been implemented:

---

## 🚀 CI Pipeline (`ci.yml`)
### **📌 Purpose**
The **CI pipeline** ensures that every change to the `app/` directory follows best practices by:
- Running **ESLint** for TypeScript linting.
- Running **Prettier** for JSON formatting.
- Allowing warnings without failing the pipeline.
- Ensuring consistency before merging code to `develop` or `main`.

### **⚡️ Trigger Conditions**
- Runs on `push` to `develop` and `main` branches.
- Runs on `pull_request` to `develop` and `main`.
- **Only runs if changes are made in `app/**`.**

### **🔧 Workflow Steps**
1. **Checkout Code** – Fetches the latest repository changes.
2. **Set Up Node.js** – Configures the environment for JavaScript/TypeScript.
3. **Install Dependencies** – Installs project dependencies using `npm ci`.
4. **Run ESLint (Linting)** – Scans TypeScript files for errors (`app/**/*.ts`).
5. **Run Prettier (Formatting)** – Checks JSON formatting (`app/**/*.json`).
6. **Allow Warnings Without Failing** – Uses `|| true` to continue despite warnings.

### **📝 YAML Reference**
See [`.github/workflows/ci.yml`](.github/workflows/ci.yml).

---

## 🏗️ Terraform Pipeline (`terraform.yml`)
### **📌 Purpose**
The **Terraform pipeline** automates infrastructure deployment with Terraform:
- **Tests infrastructure locally using LocalStack**.
- **Runs security checks with Checkov**.
- **Deploys to AWS without manual approval**.

### **⚡️ Trigger Conditions**
- Runs on `push` to `main` if `infrastructure/**` changes.
- Runs on `pull_request` to `main`.

### **🔧 Workflow Steps**
#### **1️⃣ Local Validation (`terraform-local`)**
1. **Checkout Code** – Fetches infrastructure changes.
2. **Set Up Terraform** – Installs Terraform CLI.
3. **Start LocalStack** – Runs AWS services locally via Docker.
4. **Terraform Init** – Initializes Terraform providers.
5. **Terraform Validate** – Checks syntax correctness.
6. **Checkov Security Scan** – Analyzes Terraform code for security risks.
7. **Terraform Plan (LocalStack)** – Generates an execution plan for local testing.

#### **2️⃣ AWS Deployment (`terraform-aws`)**
1. **Checkout Code** – Fetches infrastructure changes.
2. **Set Up Terraform** – Installs Terraform CLI.
3. **Terraform Init (AWS)** – Prepares Terraform for AWS deployment.
4. **Terraform Apply (AWS)** – Applies infrastructure changes automatically.

### **📝 YAML Reference**
See [`.github/workflows/terraform.yml`](.github/workflows/terraform.yml).

---



