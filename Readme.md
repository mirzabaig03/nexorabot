# Nexora Bot

Nexora Bot is a Multi-Modal RAG (Retrieval-Augmented Generation) application built with:

* **FastAPI** (Backend API)
* **Celery** (Asynchronous ingestion worker)
* **Redis** (Message broker)
* **Supabase Cloud** (Database + Storage)
* **Next.js** (Frontend)
* **Clerk** (Authentication)

This repository contains both the frontend and the fully containerized backend.

---

# 🏗 Project Structure

```
NEXORABOT/
│
├── Nexora_Bot_Client/        # Next.js Frontend
│   ├── src/
│   ├── public/
│   ├── .env.example
│   └── package.json
│
└── Nexora_Bot_Server/        # Dockerized Backend
    ├── src/
    ├── docker-compose.yml
    ├── Dockerfile
    ├── pyproject.toml
    ├── poetry.lock
    ├── .env.docker.example
    └── supabase/
```

---

# 🧱 Architecture Overview

```
Frontend (Next.js)
        ↓
FastAPI Backend (Docker)
        ↓
Redis (Docker)
        ↓
Celery Worker (Docker)
        ↓
Supabase Cloud
```

---

# ⚙️ Prerequisites

Make sure the following are installed:

* **Docker Desktop** (required)
* **Node.js 18+**
* A **Supabase Cloud project**
* A **Clerk project** for authentication

No local PostgreSQL or Supabase installation is required.

---

# 🔐 Environment Configuration

## 1️⃣ Backend Configuration

Navigate to:

```
Nexora_Bot_Server/
```

Create a file named:

```
.env.docker
```

Use `.env.docker.example` as reference.

---

## 2️⃣ Frontend Configuration

Navigate to:

```
Nexora_Bot_Client/
```

Create a file named:

```
.env
```

Use `.env.example` as reference.

``
---

# 🚀 Running the Project

## Step 1 — Start the Backend

Open a terminal and run:

```bash
cd Nexora_Bot_Server
docker compose up --build
```

This will start:

* FastAPI backend on **[http://localhost:8000](http://localhost:8000)**
* Celery worker
* Redis message broker

To verify backend is running, open:

```
http://localhost:8000/docs
```

---

## Step 2 — Start the Frontend

Open a new terminal and run:

```bash
cd Nexora_Bot_Client
npm install
npm run dev
```

Frontend will be available at:

```
http://localhost:3000
```

# 🛑 Stopping the Backend

From inside `Nexora_Bot_Server/`:

```bash
docker compose down
```

---

# 📌 Important Notes

* Backend is fully containerized using Docker.
* Supabase is cloud-hosted.
* Redis runs inside Docker.
* Frontend runs locally using Node.js.
* First Docker build may take significant time due to ML dependencies.
* Ensure Docker has sufficient memory allocated (8GB recommended).

---

# 🔐 Security

* Backend uses Supabase **Service Role Key** for system-level operations.
* Frontend must only use public keys.
* Never commit `.env` or `.env.docker` files.
* Rotate keys immediately if exposed.

---

This setup allows full local development and testing of the complete Nexora Bot system.
