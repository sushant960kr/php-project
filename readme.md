Project Summary: Automated PHP Deployment Using Jenkins, Docker, and AWS EC2
This project automates the deployment of a PHP application using Jenkins, Docker, and AWS EC2, ensuring seamless CI/CD (Continuous Integration & Continuous Deployment). It sets up an automated pipeline that pulls code from GitHub, builds a Docker image, pushes it to DockerHub, and deploys it on an AWS EC2 instance.

Key Components:
GitHub Repository: Stores the PHP project and Jenkins pipeline configuration.
Jenkins CI/CD Pipeline: Automates the build, test, and deployment process.
Docker: Containerizes the PHP application for easy deployment.
AWS EC2: Hosts the application on a scalable cloud server.
SSH & Credentials Management: Securely connects Jenkins to AWS for deployment.
Workflow:
Fork & Clone the GitHub Repository
Modify the Jenkinsfile to use your GitHub and DockerHub details
Create AWS EC2 Instances: One as a Master (Jenkins + Docker) and another as a Node
Install Jenkins & Docker on the Master instance using an automated script
Configure Jenkins Credentials: Add DockerHub and SSH keys for authentication
Trigger the Jenkins Pipeline:
Pulls the latest code from GitHub
Builds a Docker image and pushes it to DockerHub
Deploys the image on the AWS Node instance
Access the Running Application using the EC2 Public IP

![Screenshot 2025-03-18 134745](https://github.com/user-attachments/assets/2271bccc-fa5c-4abd-99d4-7aac470b0813)
![Screenshot 2025-03-18 134639](https://github.com/user-attachments/assets/952c791f-e589-4bec-a2ff-8030fbb44b07)
![Screenshot 2025-03-18 134619](https://github.com/user-attachments/assets/19b88254-954b-4960-8ad7-97127cf50d56)
