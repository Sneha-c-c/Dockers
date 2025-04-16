# 🐳 Docker Mastery with Sneha

A complete learning journey from **Docker beginner to advanced**, explained using real-life analogies, practical examples, and powerful tricks.

---

## 📚 Topics Covered

### ✅ 1. What is Docker?
> Docker is like a **container truck** 🚛 – it packages software, dependencies, and config together to run anywhere.

- Lightweight, fast, and portable
- Solves the "It works on my machine" problem
- Container ≠ Virtual Machine (no OS overhead)

---

### ✅ 2. Images vs Containers
- **Image** = Recipe 📖  
- **Container** = Dish prepared using that recipe 🍝  
- You create containers **from** images

---

### ✅ 3. Dockerfile
> Instructions to bake your custom app image 🍪

```Dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["node", "index.js"]
```

- `FROM`: base image
- `COPY`: copy files into container
- `RUN`: run shell commands (install dependencies)
- `CMD`: start the app

---

### ✅ 4. Build & Run Commands

```bash
docker build -t sneha-app .
docker run -p 3000:3000 sneha-app
docker ps
docker stop <container_id>
```

---

### ✅ 5. Volumes & Bind Mounts

- **Volume**: Persistent storage managed by Docker
- **Bind Mount**: Link a specific local folder to container path (live syncing)

```bash
docker run -v myvol:/data myimage        # Volume
docker run -v $(pwd):/app myimage        # Bind mount
```

---

### ✅ 6. Networking in Docker

- Containers communicate via internal DNS (`app`, `mongo`, etc.)
- Use Docker’s default bridge network
- `--link` or custom networks are optional for more control

---

### ✅ 7. Docker Compose 🧩

> Define & run multi-container apps (like a personal assistant 💼)

```yaml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      - mongo
  mongo:
    image: mongo
    volumes:
      - mongo_data:/data/db

volumes:
  mongo_data:
```

```bash
docker-compose up
docker-compose down
```

---

### ✅ 8. Dockerignore

Like `.gitignore` for Docker to skip unnecessary files:

```plaintext
node_modules
.env
*.log
tests/
```

---

### ✅ 9. Multi-Stage Builds ⚡️

> Build in one stage, deploy clean in another (smaller, faster, secure)

```Dockerfile
FROM node:18 as builder
WORKDIR /app
COPY . .
RUN npm install

FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app .
CMD ["node", "index.js"]
```

---

## 🚀 Bonus Tips

- Use **`alpine`** images for smaller size
- Always define `.dockerignore`
- Use named volumes for persistent data
- Use `docker-compose` for local dev with multiple services
- Multi-stage builds = deploy like a PRO 💼

---
