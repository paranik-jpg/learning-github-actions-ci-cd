# Docker Compose & GitHub Actions CI/CD

[![CI](https://github.com/paranik-jpg/learning-github-actions-ci-cd/actions/workflows/ci.yml/badge.svg)](https://github.com/paranik-jpg/learning-github-actions-ci-cd/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

A hands-on implementation exploring container orchestration with Docker Compose, Flask, Redis, and continuous integration with GitHub Actions.

---

## Architecture Overview

```
                      ┌──────────────────────────────────────┐
                      │            Docker Compose            │
                      │                                      │
[Client :8000] ──────►│  [web] Flask (Python 3.10)           │
                      │    │                                 │
                      │    ▼                                 │
                      │  [redis] Alpine in-memory store      │
                      │    ▲                                 │
                      │    └── Persistent Volume (redis-data)│
                      └──────────────────────────────────────┘
```

---

## Features
- **Containerized Web Service**: Lightweight Alpine-based Flask application tracking request hits.
- **In-Memory Caching**: Redis alpine image with persistent volume data mounting.
- **Service Dependency & Healthchecks**: Configured healthcheck probes preventing race conditions during container spin-up.
- **Automated CI Pipeline**: Validates Python syntax/linting with `flake8` and verifies Compose configuration on every commit and PR.

---

## Running Locally

1. **Clone the repository**:
   ```bash
   git clone https://github.com/paranik-jpg/learning-github-actions-ci-cd.git
   cd learning-github-actions-ci-cd
   ```

2. **Configure environment variables**:
   ```bash
   cp .env.example .env
   ```

3. **Start services with Docker Compose**:
   ```bash
   docker compose up --build
   ```

4. **Verify endpoint**:
   ```bash
   curl http://localhost:8000
   # Hello from Docker! I have been seen 1 time(s).
   ```

---

## License
Distributed under the [MIT License](LICENSE).
