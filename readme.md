# PHP Project – Automated Deployment Using Jenkins, Docker, DockerHub & AWS

This project shows how a PHP application can be automatically deployed using a CI/CD pipeline.  
The pipeline uses **Jenkins** for automation, **Docker** for containerization, **DockerHub** for image storage, and **AWS EC2 + ASG + Route 53** for hosting and scaling.

---

## 📌 Project Overview

This repository contains a simple PHP web application.  
The main goal of the project is to automate the entire deployment process so that:

- Whenever code is updated on GitHub  
- Jenkins automatically builds and deploys it  
- The application becomes live on AWS EC2  
- The website is accessible using a Route 53 domain  
- The infrastructure auto-scales using ASG  

This creates a production-ready CI/CD setup.

---

## 🔄 CI/CD Pipeline Workflow

### **1. Fork the GitHub Repository**
The original project was forked and uploaded to your GitHub account.

### **2. Connect GitHub to Jenkins Using Poll SCM**
- Jenkins monitors the GitHub repo  
- Whenever a change is pushed, Jenkins automatically starts the pipeline  

Example Poll SCM schedule:  

### **✔ Route 53 (DNS)**
- Route 53 Hosted Zone was created  
- An **A-Record (Alias)** was mapped to the Application Load Balancer (ALB)  
- This allows accessing the app using your domain name  

### **✔ Auto Scaling Group (ASG)**
- EC2 instances run inside an ASG  
- ASG automatically increases or decreases the number of servers  
- Each new EC2 instance pulls the Docker image and runs the PHP container  
- ALB performs health checks and routes traffic

This gives:
- High availability  
- Automatic failover  
- Automatic scaling  


  ---

![Screenshot 2025-03-18 134745](https://github.com/user-attachments/assets/2271bccc-fa5c-4abd-99d4-7aac470b0813)
![Screenshot 2025-03-18 134639](https://github.com/user-attachments/assets/952c791f-e589-4bec-a2ff-8030fbb44b07)
![Screenshot 2025-03-18 134619](https://github.com/user-attachments/assets/19b88254-954b-4960-8ad7-97127cf50d56)
