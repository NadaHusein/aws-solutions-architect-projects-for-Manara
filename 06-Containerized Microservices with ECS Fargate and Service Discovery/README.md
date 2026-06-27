\##Project 6 – Containerized Microservices with ECS Fargate and Service Discovery



**Overview**



This project demonstrates how to migrate a monolithic Node.js application into containerized microservices running on Amazon ECS Fargate.



The application consists of three independent services:



* Auth Service
* Orders Service
* Notifications Service



Each service is deployed independently, communicates through AWS Cloud Map service discovery, and is fronted by an Application Load Balancer using path-based routing.



**Solution Architecture**



The application is deployed inside a VPC.



External users access the Application Load Balancer.



The ALB routes requests:



/api/auth

&#x20;     ↓

Auth Service



/api/orders

&#x20;     ↓

Orders Service



/api/notifications

&#x20;     ↓

Notifications Service



Each service runs as an ECS Fargate Service.



Services communicate internally using AWS Cloud Map DNS names.



Sensitive configuration is injected from AWS Secrets Manager.



Redis is used as a centralized session cache.



CodePipeline automatically deploys new Docker images using Blue/Green deployment with CodeDeploy.



**Networking**



* VPC
* Public Subnets
* Private Subnets
* NAT Gateway
* Internet Gateway
* Security Groups
* Application Load Balancer



Containers run inside private subnets.



Only the ALB is internet-facing



**ECS Cluster**



One ECS Cluster hosts three Fargate services.



**Cluster**



├── Auth Service



├── Orders Service



└── Notifications Service



**Each service has:**



* Task Definition
* Task Role
* Execution Role
* Auto Scaling
* Health Checks



**Service Discovery**



AWS Cloud Map provides DNS-based discovery.



Example:



auth.internal



orders.internal



notifications.internal



**Orders service can call**



http://auth.internal



without knowing IP addresses.



**Container Images**



Each microservice has its own Docker image.



Auth



↓



Docker



↓



Amazon ECR



↓



Amazon ECS



Image scanning is enabled on push.



**Load Balancer Routing**



Example routing:



**Path	            Target Service**

/api/auth	        Auth

/api/orders	        Orders

/api/notifications	Notifications



**Secrets Management**



Secrets Manager stores:



Database password

JWT Secret

API Keys



Secrets are injected into ECS containers during startup.



No credentials are hardcoded



**Redis**



Amazon ElastiCache Redis stores:



User sessions

Authentication cache

Shared application cache



This keeps containers stateless



**CI/CD Pipeline**



Deployment flow:



GitHub



↓



CodePipeline



↓



Build Docker Images



↓



Push to Amazon ECR



↓



CodeDeploy



↓



Blue Environment



↓



Validation



↓



Traffic Shift



↓



Green Environment



Automatic rollback occurs if health checks fail.



**Monitoring**



Monitoring includes:



CloudWatch Logs

ECS Metrics

ALB Metrics

X-Ray Service Map

Security

IAM Task Roles

Private Subnets



**Security Groups**

Secrets Manager

HTTPS

Image Vulnerability Scanning

Least Privilege Access

