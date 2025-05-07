# 🚀 DevOps Infrastructure for Full-Stack Web Application

[![Build Status](https://img.shields.io/badge/build-passing-brightgreen)]()
[![Uptime Status](https://img.shields.io/badge/frontend-100%25-green)]()
[![Vault Status](https://img.shields.io/badge/vault-online-blue)]()
[![License](https://img.shields.io/badge/license-MIT-blue.svg)]()

---

This repository documents the end-to-end DevOps pipeline and infrastructure configuration for a full-stack web application, deployed and maintained on an Azure Virtual Machine. The setup supports continuous integration, deployment, monitoring, reverse proxying, secure secret management, and access via custom domain and HTTPS.

---

## 🧰 Features & Implementations

### ☁️ Azure Virtual Machine Configuration

* Provisioned a VM on Microsoft Azure with resources tailored to the project’s scope.
* Enabled **Azure Monitor** and configured custom **firewall alerts** for basic internal visibility.

---

### ⚙️ CI/CD with Jenkins

* Integrated **Jenkins** with a multibranch pipeline triggered via GitHub webhooks.
* Separated CI/CD logic into individual `Jenkinsfile`s for **frontend** and **backend** repositories:

#### 🖼️ Frontend Pipeline:

* Sets up the environment.
* Linting and unit testing.
* Builds the React application.
* Deploys the static files.

#### ⚙️ Backend Pipeline:

* Environment setup and Docker image build.
* **Development Branch**:

  * Runs the image in a temporary container.
  * Performs health checks to validate container behavior.
  * Removes the container after testing.
* **Main Branch**:

  * Pushes the image to DockerHub as `latest`.
  * Pulls and deploys the container on the VM.
  * Runs production-level health checks.

---

### 🌐 Nginx Reverse Proxy

* Configured **Nginx** to:

  * Serve frontend static files.
  * Route API traffic to the backend container.
  * Proxy requests to the HashiCorp Vault service.
  * Enforce **HTTP to HTTPS** redirection for secure access.

---

### 🌍 Custom Domain & SSL

* Purchased a domain and configured DNS records for:

  * Frontend
  * Backend API
  * Vault service
* Generated and installed **SSL certificates** for encrypted HTTPS access on all services.

---

### 📊 Monitoring & Alerting

#### 🔎 Internal Monitoring

* Deployed **Prometheus** and **Node Exporter** to track system metrics (CPU, memory, disk).
* Visualized metrics through a **Grafana** dashboard.
* Implemented **Alertmanager** to email alerts to the DevOps leader and team lead when thresholds are exceeded.

#### 🌐 External Monitoring

* Set up **UptimeRobot** to monitor availability of:

  * Frontend
  * Backend API
  * Vault service
* Configured email alerts for downtime or unreachability.

---

### 🔐 Secret Management with HashiCorp Vault

* Installed and configured the **open-source version of HashiCorp Vault** on the Azure VM.
* Vault is accessible via a secure subdomain with HTTPS enabled via Nginx reverse proxy.
* Configured **custom policies** to enforce principle of least privilege:

  * Example: A Jenkins-specific policy that allows access to only required secret paths for pipeline operations.
  * Restricted access to more sensitive secrets for non-privileged applications or services.
* Enabled **AppRole authentication** to allow services like Jenkins to authenticate securely and programmatically.

---

## 📄 Repository Structure

```
/infrastructure
  ├── nginx/
  ├── jenkins/
  ├── monitoring/
  └── vault/
```

---

## 👥 Contributors

* **DevOps Lead:** \[Your Name]
* **Team Lead:** \[Team Leader Name]

---

## 📌 License

This project is licensed for academic and personal use.

---

## 🛠️ Tools & Technologies

* Azure Virtual Machine
* Jenkins
* Docker & DockerHub
* Prometheus & Grafana
* Node Exporter
* Alertmanager
* Nginx
* UptimeRobot
* HashiCorp Vault
* GitHub Webhooks
