# Day 7 – CI/CD Pipeline Design

## 1️⃣ CI/CD Best Practices
- Use small, frequent commits.
- Automate builds, tests, and deployments.
- Keep pipelines fast and efficient.
- Use environment variables for secrets.
- Implement rollback mechanisms.

## 2️⃣ Company Deployment Environments
| Environment | Purpose | Example Branch |
|--------------|----------|----------------|
| Development | For internal testing | dev |
| Staging | For pre-production validation | staging |
| Production | Live user environment | main |

## 3️⃣ Testing Strategies in Pipelines
- **Unit Tests:** Run automatically on every push.  
- **Integration Tests:** Run before staging deploy.  
- **End-to-End Tests:** Run before production release.  
- **Security Scans:** Run in all environments.

## 4️⃣ Security Scanning Integration
- Use tools like **Trivy** or **Snyk** for vulnerability scanning.  
- Check for:
  - Outdated dependencies
  - Secrets in code
  - Base image vulnerabilities

## 5️⃣ Standard Pipeline Template (Example)
```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 18
      - name: Install dependencies
        run: npm ci
      - name: Run tests
        run: npm test
      - name: Build Docker Image
        run: docker build -t my-html-app .
      - name: Push to Docker Hub
        run: docker push amalap/my-html-app:latest
