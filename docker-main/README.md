

```markdown
# 🐳 Dockerized Flask App

A simple Python Flask web app running inside a Docker container. This project demonstrates how to build, run, and manage containers using Docker and Docker Desktop.

---

## 📁 Project Structure

```
my-python-app/
├── app.py             # Main Flask application
├── requirements.txt   # Python dependencies
├── Dockerfile         # Docker build instructions
└── README.md          # Project documentation
```

---

## 🚀 Getting Started

### 1. Prerequisites

✅ [Docker Desktop](https://www.docker.com/products/docker-desktop/) installed and running  
✅ Visual Studio Code (optional, but recommended)  
✅ Python **not required** on host — everything runs in the container

---

### 2. Clone the Repository

```bash
git clone https://github.com/your-username/my-python-app.git
cd my-python-app
```

---

### 3. Build the Docker Image

```bash
docker build -t my-python-app .
```

---

### 4. Run the Docker Container

```bash
docker run -d -p 5000:5000 --name flask-container my-python-app
```

![Running Container](https://github.com/user-attachments/assets/788d86e3-f021-4c47-bdfe-83efc2985a5d)  
Image URL: `https://github.com/user-attachments/assets/788d86e3-f021-4c47-bdfe-83efc2985a5d`

---

### 5. Check the App in Docker Desktop

Open **Docker Desktop** and go to the **Containers & Apps** tab:

- ✅ See `flask-container` running  
- 📜 Click to view logs  
- 💻 Use the built-in CLI to access the container shell  
- 🔁 Start / Stop / Restart / Delete the container as needed  

---

### 6. View the Web App in Browser (Optional)

Open your browser and visit:

```
http://localhost:5000
```

You should see:  
**`Hello from Docker!`**

![Web App Screenshot](https://github.com/user-attachments/assets/4def6299-36e8-4a07-a91f-b5a570352b70)  
Image URL: `https://github.com/user-attachments/assets/4def6299-36e8-4a07-a91f-b5a570352b70`

---

## 🧰 Useful Docker Commands

```bash
# List running containers
docker ps

# List all containers (including stopped)
docker ps -a

# View logs
docker logs flask-container

# Open a shell inside the container
docker exec -it flask-container bash

# Stop the container
docker stop flask-container

# Remove the container
docker rm flask-container
```

![Docker Logs](https://github.com/user-attachments/assets/e74c8031-77e8-43f9-ae2a-58110d71bed8)  
Image URL: `https://github.com/user-attachments/assets/e74c8031-77e8-43f9-ae2a-58110d71bed8`

---

## 📦 Docker Desktop Overview

| Feature              | Location                                |
|----------------------|-----------------------------------------|
| View containers      | Containers & Apps tab                   |
| Access logs / CLI    | Click container → Logs / CLI            |
| Manage images        | Images tab                              |
| Manage volumes       | Volumes tab                             |
| Start / Stop / Delete| Buttons in container row                |

![Docker UI](https://github.com/user-attachments/assets/a8c06c57-a286-4c2c-a632-f3291a1172c3)  
Image URL: `https://github.com/user-attachments/assets/a8c06c57-a286-4c2c-a632-f3291a1172c3`

---

## 🧼 Clean Up

```bash
# Stop and remove the container
docker stop flask-container
docker rm flask-container

# Remove the Docker image
docker rmi my-python-app
```

---
```
