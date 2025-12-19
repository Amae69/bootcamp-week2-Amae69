# Project Analysis: ShopMicro E-commerce Platform

## 📖 Overview
**ShopMicro** is a microservices-based e-commerce platform designed to demonstrate modern DevOps and Platform Engineering practices. It integrates a full stack of applications (Frontend, Backend, ML) with a production-grade infrastructure stack including Kubernetes orchestration and comprehensive observability.

---

## 📂 Folder Structure Analysis

### 1. `/backend` (Node.js & Express)
**Purpose**: The core API service managing products, users, and business logic.
- **`server.js`**: Entry point. Sets up the Express app, middleware (logging, metrics, security), and route handling.
- **`routes/`**: API endpoints for products, users, and health checks.
- **`middleware/`**: Custom middleware for `telemetry` (OpenTelemetry), `logging` (Winston), and `metrics` (Prometheus).
- **`Dockerfile`**: Multi-stage build for valid Node.js containerization.

### 2. `/frontend` (React.js)
**Purpose**: The user facing interface for the e-commerce store.
- **`src/`**: Source code for React components and pages.
- **`public/`**: Static assets.
- **`nginx.conf`**: Nginx configuration for serving the React build in production/containerized environments.
- **`Dockerfile`**: Builds the React app and serves it via Nginx.

### 3. `/ml-service` (Python & Flask)
**Purpose**: A dedicated microservice for product recommendations using Machine Learning.
- **`app.py`**: Flask application server containing the recommendation logic and API routes.
- **`telemetry.py`**: OpenTelemetry configuration for distributed tracing.
- **`metrics.py`**: Custom Prometheus metrics collectors.
- **`logging_config.py`**: Structured logging setup.
- **`requirements.txt`**: Python dependencies (pandas, scikit-learn, flask, etc.).

### 4. `/infrastructure` (Observability & Data)
**Purpose**: Configuration for the supporting infrastructure services, primarily the "LGTM" observability stack.
- **`alloy/`**: Configuration for Grafana Alloy (telemetry collector).
- **`grafana/`**: Dashboards and datasource provisioning.
    - **`dashboards/`**: JSON definitions for pre-built Grafana dashboards.
- **`loki/`**: Configuration for Loki (log aggregation).
- **`mimir/`**: Configuration for Mimir (long-term metric storage).
- **`tempo/`**: Configuration for Tempo (distributed tracing).
- **`prometheus/`**: Prometheus (metrics scraping) configuration.
- **`postgres/`**: Initialization scripts (`init.sql`) for the database.

### 5. `/k8s` (Kubernetes Manifests)
**Purpose**: Declarative yaml files for deploying the application to a Kubernetes cluster.
- **`deployments/`**: Defines the desired state for pods (replicas, images, resources) for all services (`backend`, `frontend`, `ml-service`, `postgres`, `redis`).
- **`services/`**: Internal networking abstraction to expose deployments.
- **`ingress/`**: Rules for routing external traffic to internal services.
- **`configmaps/`**: decoupled configuration data injected into pods.
- **`namespace.yaml`**: Defines the logical isolation (likely `shopmicro`) for the project.

### 6. `/scripts` (Automation)
**Purpose**: Shell scripts to automate common developer and ops tasks.
- **`deploy-k8s-lab.sh`**: One-click script to deploy the entire stack to a Kubernetes cluster.
- **`start-full-observability.sh`**: Helper to spin up the observability stack.
- **`status-check.sh`**: Verification script to check health of deployed services.
- **`quick-start.sh`**: Likely a "get started" script for local development.

---

## 🛠 Tech Stack Summary

| Layer | Technology |
|-------|------------|
| **Frontend** | React, Nginx |
| **Backend** | Node.js, Express, OpenTelemetry |
| **ML Service** | Python, Flask, Pandas, Scikit-learn |
| **Database** | PostgreSQL, Redis |
| **Orchestration** | Kubernetes (K8s), Docker Compose |
| **Observability** | Grafana, Prometheus, Loki, Tempo, Mimir, Alloy |

## 🚀 Key Features
- **Microservices Architecture**: Decoupled services communicating via REST APIs.
- **Full Observability**: Logs, Metrics, and Traces are correlated and visualized.
- **Resiliency**: Readiness/Liveness probes and separate infrastructure components.
- **Automation**: Scripts and Manifests for reproducible deployments.
