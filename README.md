Here’s a **clean, complete guide** you can copy-paste or turn into a README for deploying your Streamlit app using Docker from **local to server**.

---

# 🚀 Streamlit App: Docker Deployment from Local to Server

This guide covers:

1. ✅ Tagging the Docker image
2. ⬆️ Pushing to Docker Hub
3. 📥 Pulling from Docker Hub on the server
4. 🔁 Restarting the container with the latest image

---

## 🔧 1. Build and Tag Docker Image (Local Machine)

### A. Build the image

```bash
docker build -t streamlit-app .
```

### B. Tag the image for Docker Hub

Replace `yourusername` and `yourtag` (e.g., `latest` or `v1`):

```bash
docker tag streamlit-app yourusername/streamlit-app:yourtag
```

Example:

```bash
docker tag streamlit-app johnsmith/streamlit-app:v1
```

---

## 🔐 2. Login to Docker Hub

```bash
docker login
```

Enter your Docker Hub username and password.

---

## 📤 3. Push the Image to Docker Hub

```bash
docker push yourusername/streamlit-app:yourtag
```

Example:

```bash
docker push johnsmith/streamlit-app:v1
```

---

## 💻 4. SSH into Your Server

```bash
ssh user@your-server-ip
```

---

## 📥 5. Pull the Image on the Server

```bash
docker pull yourusername/streamlit-app:yourtag
```

Example:

```bash
docker pull johnsmith/streamlit-app:v1
```

---

## 🔁 6. Stop and Remove Old Container (Optional, but recommended)

```bash
docker stop streamlit-app
docker rm streamlit-app
```

> This avoids naming conflicts if the container already exists.

---

## 🚀 7. Run the New Container

```bash
docker run -d \
  --name streamlit-app \
  -p 8501:8501 \
  yourusername/streamlit-app:yourtag
```

Example:

```bash
docker run -d --name streamlit-app -p 8501:8501 johnsmith/streamlit-app:v1
```

---

## ✅ 8. Check It’s Running

```bash
docker ps
```

Open in browser:

```
http://your-server-ip:8501
```

---

## 📄 Optional: `docker-compose.yml` for Server

If you want to use `docker-compose`, create this file on your **server**:

```yaml
version: '3.8'

services:
  streamlit:
    image: johnsmith/streamlit-app:v1
    ports:
      - "8501:8501"
    restart: always
    container_name: streamlit-app
```

Then run:

```bash
docker-compose pull
docker-compose up -d
```
