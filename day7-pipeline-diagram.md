# CI/CD Pipeline Architecture Diagram

```mermaid
flowchart LR
    A[Developer Pushes Code] --> B[GitHub Repository]
    B --> C[GitHub Actions CI/CD Pipeline]
    C --> D[Build Docker Image]
    D --> E[Push Image to Docker Hub]
    E --> F[Deploy to Dev/Staging/Production Environments]
