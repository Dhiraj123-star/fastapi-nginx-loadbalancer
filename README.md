
# ⚡ FastAPI + Nginx Load Balancer (Dockerized)

A simple setup to understand and experiment with **different load balancing algorithms** — 🌀 **Round Robin**, ⚖️ **Least Connections**, and 🔒 **IP Hash** — using **FastAPI**, **Nginx**, and **Docker Compose** 🐳.

Now includes **GitHub Actions CI/CD** core functionality for automatic Docker builds and pushes.

---

## 🧠 Overview

This project demonstrates **how Nginx distributes requests** among multiple **FastAPI** application instances using various **load balancing strategies**.
It’s a hands-on example to explore **scalability**, **resilience**, and **traffic distribution** in containerized microservices setups.

---

## 📁 Project Structure

```
fastapi-nginx-loadbalancer/
├── app/
│   ├── main.py
│   ├── requirements.txt
│   ├── Dockerfile
├── nginx/
│   ├── nginx.conf
├── docker-compose.yml
└── README.md
```

---

## ⚙️ Setup & Run Locally

### 🏗️ 1. Build and Start Containers

```bash
docker-compose up --build
```

### 🌍 2. Visit in Browser

Open 👉 **[http://localhost](http://localhost)**

You’ll see alternating responses like:

```json
{"message": "Hello from FastAPI!", "host": "app1"}
{"message": "Hello from FastAPI!", "host": "app2"}
```

---

## 🔁 Load Balancing Algorithms

You can switch between load balancing methods in **`nginx/nginx.conf`** under the `upstream` block:

### 🌀 Round Robin (default)

```nginx
upstream fastapi_app {
    server app1:8000;
    server app2:8000;
}
```

### ⚖️ Least Connections

```nginx
upstream fastapi_app {
    least_conn;
    server app1:8000;
    server app2:8000;
}
```

### 🔒 IP Hash

```nginx
upstream fastapi_app {
    ip_hash;
    server app1:8000;
    server app2:8000;
}
```

To apply changes:

```bash
docker compose restart nginx
```

---

## ⚙️ CI/CD (GitHub Actions) Core Functionality

This project includes a **GitHub Actions workflow** that:

* 🔄 **Triggers automatically** on pushes or pull requests to `main`.
* 🏗️ **Builds the Docker image** for FastAPI + Nginx.
* 🔑 **Logs in to Docker Hub** securely via GitHub Secrets.
* 🚀 **Pushes the latest image** to Docker Hub (`dhiraj918106/fastapi-nginx-loadbalancer:latest`).

This ensures every change is automatically built and ready for deployment without manual intervention.

---

## 🧹 Cleanup

Stop and remove containers:

```bash
docker compose down
```

---


