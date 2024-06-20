
# DevOps project using CircleCI, ArgoCD, Sonarqube, K8s, Prometheus, Grafana

This repository showcases a comprehensive CI/CD pipeline for deploying a Node.js web application. It leverages a robust set of tools and services to ensure efficient, scalable, and reliable deployments.

Tools and Technologies Used:

- GitHub: Source code management and collaboration.
- CircleCI: Continuous Integration for automated testing and building.
- ArgoCD: Continuous Delivery for managing Kubernetes deployments.
- SonarQube: Code quality analysis and continuous inspection.
- Kubernetes: Orchestrating containerized applications.
- Grafana & Prometheus: Monitoring and observability of the application.
- Slack: Notifications and team communication.

## We will run the SonarQube on Docker
```bash
docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
