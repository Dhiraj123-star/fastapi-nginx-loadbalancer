
# ⚡ FastAPI + Nginx Load Balancer (Dockerized)

A simple setup to understand **different load balancing types** (Round Robin, Least Connections, IP Hash) using **FastAPI**, **Nginx**, and **Docker Compose** 🐳.

---

## 🧠 Overview

This project runs **multiple FastAPI app instances** behind **Nginx** to simulate load balancing behavior.

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

## 🔁 Change Load Balancing Type

Edit `nginx/nginx.conf` → update the upstream section:

### ⚙️ Round Robin (default)

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

Then restart Nginx:

```bash
docker compose restart nginx
```

---

## 🧹 Cleanup

To stop and remove containers:

```bash
docker compose down
```

---

## ✅ Next Steps

In the next stage, we’ll:

* Add **more FastAPI instances dynamically**
* Try **auto-scaling**
* Add **metrics and health checks**

