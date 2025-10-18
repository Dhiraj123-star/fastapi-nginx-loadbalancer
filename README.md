

# ⚡ FastAPI + Nginx Load Balancer (Dockerized)

A simple setup to understand and experiment with **different load balancing algorithms** — 🌀 **Round Robin**, ⚖️ **Least Connections**, and 🔒 **IP Hash** — using **FastAPI**, **Nginx**, and **Docker Compose** 🐳.

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

## ⚙️ Setup & Run

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

You can easily switch between load balancing methods in **`nginx/nginx.conf`** under the `upstream` block:

### 🌀 Round Robin (default)

Distributes requests evenly across all servers.

```nginx
upstream fastapi_app {
    server app1:8000;
    server app2:8000;
}
```

---

### ⚖️ Least Connections

Routes new requests to the server with the **fewest active connections** — ideal for uneven workloads.

```nginx
upstream fastapi_app {
    least_conn;
    server app1:8000;
    server app2:8000;
}
```

---

### 🔒 IP Hash

Ensures each client (based on IP) connects to the **same backend server**, maintaining session consistency.

```nginx
upstream fastapi_app {
    ip_hash;
    server app1:8000;
    server app2:8000;
}
```

---

### ♻️ Apply Changes

After modifying the algorithm, restart Nginx:

```bash
docker compose restart nginx
```

---

## 🧹 Cleanup

Stop and remove containers:

```bash
docker compose down
```

---
