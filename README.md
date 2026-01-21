# 🚀 My Portfolio Website

This is my **personal portfolio website**, deployed using a **DevOps workflow** with Docker, GitHub Actions, and AWS EC2.

## 📖 About
This project demonstrates:
- 🌐 A static portfolio website (HTML, CSS, JS)
- 🐳 Dockerized deployment using **Nginx**
- ⚙️ Automated CI/CD pipeline with **GitHub Actions**
- ☁️ Hosting on **AWS EC2**

---

## 🛠 Tech Stack
- **Frontend**: HTML, CSS, Bootstrap, JavaScript
- **Web Server**: Nginx (via Docker)
- **DevOps Tools**:
  - Docker
  - GitHub Actions
  - AWS EC2 (Ubuntu Server)


---

## 🐳 Docker Setup

### Build Image Locally
```bash
docker build -t myportfolio .
```

### Run Locally
```bash
docker run -d -p 8080:80 myportfolio
```
Visit: http://localhost:8080

---
## 📦 Push to Docker Hub
```bash
docker tag myportfolio YOUR_DOCKER_USERNAME/portfolio:latest
docker push YOUR_DOCKER_USERNAME/portfolio:latest
```
Public Repository: [Docker Hub](https://hub.docker.com/r/YOUR_DOCKER_USERNAME/portfolio)

---

## ⚙️ CI/CD with GitHub Actions

Every push to main automatically builds and pushes the Docker image to Docker Hub.
```bash
#.github/workflows/docker-build.yml

name: Build and Push Portfolio to Docker Hub

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - run: docker build -t ${{ secrets.DOCKER_USERNAME }}/portfolio:latest .
      - run: docker push ${{ secrets.DOCKER_USERNAME }}/portfolio:latest


```

## ☁️ Deployment on AWS EC2

1. Launch an Ubuntu EC2 instance (t2.micro, free tier).

2. SSH into the server:
```bash
ssh -i your-key.pem ubuntu@<EC2-PUBLIC-IP>
```

3. Install Docker:
```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
```

4. Run the container:
```bash
sudo docker run -d -p 80:80 YOUR_DOCKER_USERNAME/portfolio:latest
```

5. Your portfolio will be live at:

http://EC2-PUBLIC-IP

## 📌 Live Links

 🌍 [Live Portfolio](http://54.160.187.85/)

 🐳 [Docker Hub](https://hub.docker.com/r/mwkalindusuraj/portfolio)

 💻 [GitHub Repo](https://github.com/KalinduSuraj/Portfolio-Website)
