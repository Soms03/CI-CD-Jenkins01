This repo contains the source code of the multi-container 3-tier web application.

The directory structure is

project/
│
├── docker-compose.yml
├── db/
│   └── init.sql
├── backend/
│   ├── Dockerfile
│   ├── app.py
│   └── requirements.txt
└── frontend/
    ├── Dockerfile
    ├── index.html
    ├── backend.html
    └── student.html

It is for the purpose of practicing the CI/CD pipeline using Jenkins. 

1. The Jenkins pipeline gets triggered on a GitHub commit on the master (here) branch
2. Then pulls code from GitHub
3. Build as a Docker image with a tag.
4. Push the image to Docker hub.
5. Then it connects (SSH) to the deployment server (Ubuntu).
6. Pulls the latest image from Docker hub and the latest docker-compose.yml from GitHub.
7. Stops the previous version containers and starts containers with the latest images.
8. The credentials are managed on the Jenkins server.

Future Add-ons: (may be in another repo)

Putting all this together is not the aim, and it is not like that; using all the below-mentioned tools makes the best CI/CD pipeline.
These are the considerations, and it depends on the tech stack, infra, and pipeline design based on the requirements (SLA, SLO, etc.) and decisions like cost optimization, security/compliance, integrity, and so on.

In terms of deployment/infra tech stack.

1. Kubernetes—for orchestration.
2. Helm—managing K8s packages.
3. Terraform + Ansible—Infra provisioning and server configuration.
4. ArgoCD—Continuous deployment (It's more than that, UI, ahmm).
5. Nexus repo—build artifact repo.
6. Build tools—Maven, Pybuilder, and Cmake.

In terms of Security.

1. AWS Secrets Manager and Vaults (Terraform and others)—manage credentials (rotate them periodically).
2. Static code test—SonarQube.
3. After-build test for .py, js, Java applications.
4. Docker image scan—Trivy.
5. Dynamic code test—OSWASP.

In terms of Notification.

1. SNS—for server launch/start/stop/... during auto-scaling.
2. Slack—team notification.

In terms of Monitoring.

1. Prometheus—data collection
2. Grafana—data visualization
3. Splunk, Datadog, ELK stack—data logging
