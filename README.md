# Web App on Kubernetes Cluster

## Overview
This project is a multi-tier web application designed for cloud-native deployment using Kubernetes. It demonstrates containerization, orchestration, and modern DevOps practices.

## Scenario
- Built a multi-tier web application stack
- Containerized all components
- Thoroughly tested the stack
- Ready to host for production

## Features
- User authentication and registration
- Dashboard and user management
- File uploads and downloads
- Real-time messaging with RabbitMQ
- Fast data access with Memcached

## Requirements
- High availability
- Fault tolerance
- Easily scalable
- Platform independent
- Portable & flexible

## Industry Statistics
- 77% of containers run on Kubernetes
- 89% (including Redshift & Rancher)
- 56% of organizations plan to increase usage in 12 months
- 28% growth in production containers

## Technologies Used
- Kubernetes for orchestration
- Helm for deployment automation
- Docker for containerization
- NGINX as web server/load balancer
- Java (Spring) for backend
- MySQL for database
- RabbitMQ for messaging
- Memcached for caching

## Container Images
- Docker images are published to Docker Hub under the `vprofile` organization
  - `vprofile/vprofiledb`: Database service
  - `vprofile/vprofileapp`: Main application service

## Project Structure
- **compose/**: Docker Compose files for local development
- **helm/**: Helm charts for Kubernetes deployments
- **kubernetes/**: Raw Kubernetes manifests for all services
- **src/**: Java source code and web resources
- **pom.xml**: Maven build and dependency file

## Local Development
To run the app locally:
```sh
cd compose
docker-compose up
```
This will start all services for local testing and development.

## Key Deployment Steps
1. Provision a Kubernetes cluster (cloud or local)
2. Build and push Docker images for the app and database
3. Create an EBS volume for the database pod (if using AWS):
   ```sh
   aws ec2 create-volume --availability-zone=<zone> --size=<size> --volume-type=gp2
   ```
4. Label nodes with zone names for high availability:
   ```sh
   kubectl get nodes
   kubectl describe node <node-name> | grep <zone>
   ```
5. Configure secrets and environment variables using Kubernetes Secrets
6. Deploy dependencies (MySQL, RabbitMQ, Memcached) using Helm or manifests
7. Deploy the main application using Helm or manifests
8. Expose the app using a LoadBalancer or Ingress

## Provisioning the Stack on Kubernetes
- I provisioned the entire application stack on my Kubernetes cluster using the following command:
  ```sh
  kubectl create -f .
  ```
- This command applied all the Kubernetes manifests in the directory, creating the necessary Deployments, Services, and Secrets for my application.
- If a resource already existed (like a Secret or Service), Kubernetes reported it as "AlreadyExists" and continued with the rest of the resources.
- After running this, all components of my multi-tier web application were up and running on the cluster.

## Configuration & Secrets
- All critical configuration (database, cache, messaging, etc.) is managed in `application.properties` (not included here for security)
- Sensitive data is managed with Kubernetes Secrets (base64-encoded) and never hardcoded
- Example secret manifest:
  ```yaml
  apiVersion: v1
  kind: Secret
  metadata:
    name: app-secret
  type: Opaque
  data:
    db-pass: <base64-encoded-password>
    rmq-pass: <base64-encoded-password>
  ```

## Additional Configuration
- **logback.xml:** Centralized logging configuration for monitoring and debugging
- **validation.properties:** Custom validation messages for user input
- **db_backup.sql:** Example database backup for easy restoration

## Testing
Automated unit and integration tests are included. To run tests:
```sh
mvn test
```

## Security
- No sensitive data is exposed in code or documentation
- Follows best practices for secret management and configuration

## About
This project highlights my experience with cloud-native application development, Kubernetes, and DevOps best practices. For more details or to discuss, feel free to reach out!

## Domain Setup & Project Completion
- I configured a custom domain for my web application using AWS Route 53 and GoDaddy.
- This allowed me to point a memorable URL to my Kubernetes cluster’s external IP, making the application easily accessible to users.
- With the domain setup complete, the project is fully deployed and production-ready.


