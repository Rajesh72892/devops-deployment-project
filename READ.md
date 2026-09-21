*** DevOps Deployment Report ***
1. Project Overview
This project demonstrates the deployment of a simple web application using DevOps practices.
The application was developed using HTML and managed with Git and GitHub. Docker was used to containerize the application, GitHub Actions was used for CI automation, and the application was deployed on an AWS EC2 Linux server. Nginx was configured as a reverse proxy, and basic monitoring and logging were implemented.

2. Technology Stack

HTML  - Web application
Git  - Version control
GitHub -  Source code repository
GitHub Actions	CI automation
Docker	- Application containerization
Docker Compose	- Container configuration
AWS EC2	- Cloud server
Linux	- Server environment
Nginx	- Reverse proxy

3. Git Repository Structure

devops-deployment-project/
│
├── .github/
│   └── workflows/
│       └── ci.yml
│
├── index.html
├── Dockerfile
├── docker-compose.yml
└── README.md

4. Docker Architecture

The web application is packaged into a Docker image using Nginx Alpine as the base image. The Docker container runs the application on port 80.

Web Application
   │
   ▼
index.html
   │
   ▼
Dockerfile
   │
   ▼
Docker Image
   │
   ▼
Docker Container
   │
   ▼
Container Port 80
   │
   ▼
EC2 Host Port 8080

5. CI/CD Workflow

The CI/CD pipeline automates the process of building and testing the Dockerized web application whenever code is pushed to GitHub.

Developer
    ↓
main branch
    ↓
GitHub Repository
    ↓
Pull Request / Merge
    ↓
GitHub Actions
    ↓
Checkout Source Code
    ↓
Build Docker Image
    ↓
Run Docker Container
    ↓
Test Application
    ↓
Successful CI Build

git hub workflow stores in : .github/workflows/ci.yml


6. Cloud Deployment Architecture

Application code is stored in GitHub.
GitHub Actions builds and tests the Docker image.
The Docker application is deployed on an AWS EC2 Linux server.
Docker runs the application on port 8080 locally.
Nginx listens on public port 80.
Nginx forwards incoming requests to the Docker container.
Users access the application through the EC2 public IP.

7. Nginx Reverse Proxy Configuration

Nginx is configured as a reverse proxy to receive HTTP requests from users and forward them to the Docker container running the web application.

server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://127.0.0.1:8080;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}



8. Monitoring & Logging Approach

Basic monitoring and logging were implemented to check the health and availability of the application and server.

Docker status: docker ps
Application logs: docker logs devops-web
Application health: curl http://localhost:8080
HTTP response: curl -I http://localhost:8080
Server resources: top, free -h, df -h
Nginx status: sudo systemctl status nginx

9. Problems Encountered

During the project, some common DevOps issues were encountered:

Git push was rejected because the remote branch had different commits.
Docker container and application port configuration required correction.
Public access required correct AWS Security Group and Nginx configuration.

10. Solutions Implemented

The issues were resolved by:

Managing Git branches and remote changes correctly.
Mapping Docker port 80 to the required local port.
Configuring Nginx to forward requests to the Docker container.
Allowing HTTP port 80 in the AWS Security Group.


11. Final Application URL

The deployed application can be accessed using the EC2 public IP:

http://54.167.117.28



