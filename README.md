# SpeechPartner Security Pipeline

A DevSecOps pipeline (SAST, dependency scanning, secret scanning, container
image scanning) built around the SpeechPartner backend and frontend code.

Source app: SpeechPartner (backend: FastAPI/Python, frontend: React/Vite).
This repo is a standalone copy of that codebase used specifically to build
and demonstrate the security pipeline, kept separate from the original
team repository.

## Pipeline

`.github/workflows/security.yml` runs on every push/PR to `main`:

- **Gitleaks** — scans git history for committed secrets
- **Semgrep** — static analysis (SAST) across backend and frontend code
- **Trivy (filesystem)** — dependency vulnerability scanning
- **Trivy (container)** — image scanning for both the backend and frontend
  Docker images

Each job fails the build on CRITICAL/HIGH severity findings, gating merges
on `main`.
