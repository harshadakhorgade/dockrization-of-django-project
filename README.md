  
# Deploying a Django Project on AWS EC2 with Docker
```markdown


This guide will walk you through setting up an AWS EC2 instance, installing Docker, Dockerizing your Django project, and deploying it on a public IP.

## Step-by-Step Guide

### 1. **Set up an EC2 Instance**
1. Log in to the **AWS Management Console**.
2. Launch a new EC2 instance:
   - Choose **t2.micro** (free-tier eligible) as the instance type.
   - Select an **Amazon Machine Image (AMI)**, such as **Ubuntu** or **Amazon Linux 2**.
3. Configure the instance:
   - Add **SSH access** by opening port `22` in the security group.
   - Add an **inbound rule** for TCP port `8000` (open it for `0.0.0.0/0`).
4. Launch the instance and download the **SSH key file**.

---

### 2. **SSH into the EC2 Instance**
- Use the SSH key to connect to your instance. Replace `<your-key.pem>` and `<your-ec2-public-ip>` with your key file and public IP:

```bash
ssh -i /path/to/your-key.pem ubuntu@<your-ec2-public-ip>
```

Example:

```bash
ssh -i "C:\Users\Harsahada Khorgade\Downloads\dockerkey.pem" ubuntu@13.233.36.42
```

---

### 3. **Install Docker on the EC2 Instance**
Run the following commands:

```bash
sudo apt-get update
sudo apt-get install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER
```

Log out and log back in to apply the group changes:

```bash
exit
ssh ubuntu@<your-ec2-public-ip>
```

Check the Docker installation:

```bash
docker --version
```

---

### 4. **Install Docker Compose (Optional)**
Install Docker Compose to manage multi-container setups:

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

---

### 5. **Upload Your Django Project to EC2**
Use **SCP** or **Git** to upload your project to the instance. For Git, run:

```bash
git clone https://github.com/harshadakhorgade/dockrization-of-django-project.git
cd dockrization-of-django-project
```

Update your Django project settings in `settings.py`:

```python
ALLOWED_HOSTS = ['*']
```

---

### 6. **Create a Dockerfile**
Add a `Dockerfile` to the root of your Django project:

```dockerfile
# Use an official Python runtime as a parent image
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container
COPY . /app/

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Expose the port the app runs on
EXPOSE 8000

# Run the Django development server
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
```

---

### 7. **Create a `docker-compose.yml` (Optional)**
If using Docker Compose, create the following file:

```yaml
version: '3'

services:
  wHere's a README file written in Markdown format:  

```markdown
# Deploying a Django Project on AWS EC2 with Docker

This guide will walk you through setting up an AWS EC2 instance, installing Docker, Dockerizing your Django project, and deploying it on a public IP.

## Step-by-Step Guide

### 1. **Set up an EC2 Instance**
1. Log in to the **AWS Management Console**.
2. Launch a new EC2 instance:
   - Choose **t2.micro** (free-tier eligible) as the instance type.
   - Select an **Amazon Machine Image (AMI)**, such as **Ubuntu** or **Amazon Linux 2**.
3. Configure the instance:
   - Add **SSH access** by opening port `22` in the security group.
   - Add an **inbound rule** for TCP port `8000` (open it for `0.0.0.0/0`).
4. Launch the instance and download the **SSH key file**.

---

### 2. **SSH into the EC2 Instance**
- Use the SSH key to connect to your instance. Replace `<your-key.pem>` and `<your-ec2-public-ip>` with your key file and public IP:

```bash
ssh -i /path/to/your-key.pem ubuntu@<your-ec2-public-ip>
```

Example:

```bash
ssh -i "C:\Users\Harsahada Khorgade\Downloads\dockerkey.pem" ubuntu@13.233.36.42
```


### 8. **Build and Run the Docker Container**
Build and run the container:

```bash
docker-compose up --build
docker-compose up -d
```

Verify the running container:

```bash
docker ps
```

To rebuild and restart:

```bash
docker-compose down
docker-compose up --build -d
```

---

### 9. **Access Your Django Project**
Visit your EC2 public IP at port `8000`:

```plaintext
http://<your-ec2-public-ip>:8000
```

---

### 10. **Clean Up Docker Containers and Images**
To stop and remove containers:

```bash
docker ps
docker stop <container_id>
docker rm <container_id>
```

To remove images and unused resources:

```bash
docker images
docker rmi <image_id>
docker image prune
docker system prune -a
```

---

## Troubleshooting
- Ensure port `8000` is open in the EC2 security group.
- Check logs for errors:

```bash
docker logs <container_id>
```

Enjoy deploying your Django project with Docker on AWS EC2!
```
   
```

---

### 8. **Build and Run the Docker Container**
Build and run the container:

```bash
docker-compose up --build
docker-compose up -d
```

Verify the running container:

```bash
docker ps
```

To rebuild and restart:

```bash
docker-compose down
docker-compose up --build -d
```

---

### 9. **Access Your Django Project**
Visit your EC2 public IP at port `8000`:

```plaintext
http://<your-ec2-public-ip>:8000
```

---

### 10. **Clean Up Docker Containers and Images**
To stop and remove containers:

```bash
docker ps
docker stop <container_id>
docker rm <container_id>
```

To remove images and unused resources:

```bash
docker images
docker rmi <image_id>
docker image prune
docker system prune -a
```

---

## Troubleshooting
- Ensure port `8000` is open in the EC2 security group.
- Check logs for errors:

```bash
docker logs <container_id>
```

Enjoy deploying your Django project with Docker on AWS EC2!
```
