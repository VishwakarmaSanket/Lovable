# Loveable

> An evolving AI-powered developer environment for generating, editing, and running applications inside isolated sandboxes.

## Overview

Loveable explores how an AI-assisted development environment can safely create and modify applications inside isolated execution environments.

The project is being built incrementally. The current implementation focuses on the **sandbox and infrastructure foundation**, while AI orchestration, authentication, routing, and related services evolve alongside it.

```text
User
  │
  ▼
Application / AI Layer
  │
  ▼
Sandbox Management
  │
  ▼
Kubernetes
  │
  ▼
Isolated Vite Environment
  │
  ▼
Preview / Execution
```

## Current Architecture

| Component | Responsibility |
|---|---|
| `sandbox/server` | Creates and manages isolated sandbox environments through the Kubernetes API |
| `sandbox/template` | React + Vite application template used inside sandbox environments |
| `sandbox/agent` | Agent-side execution capabilities within a sandbox |
| `sandbox/router` | Routes preview and agent traffic to the appropriate sandbox |
| `ai-orchestration` | Runs AI workflows and agent logic using LangGraph |
| `auth` | Handles authentication and Google OAuth flow |
| `k8s` | Kubernetes manifests, services, ingress, and RBAC configuration |
| `skaffold.yml` | Coordinates image builds, file sync, and Kubernetes deployment |

## Key Ideas

### Isolated execution

Generated application code should run in an isolated environment rather than inside the main application process. Sandboxes separate application execution from the control plane.

### Dynamic environments

The sandbox service communicates with Kubernetes to provision and manage application environments dynamically instead of treating a single local process as the runtime.

### AI orchestration

The AI layer is separated from sandbox management so agent workflows can reason about code and tools without coupling orchestration logic directly to the execution environment.

### Preview routing

Preview and agent traffic are routed through dedicated paths so individual sandbox environments can be reached without exposing their internal runtime directly.

## Tech Stack

| Area | Technologies |
|---|---|
| **Frontend** | React, Vite |
| **Backend** | Node.js, Express |
| **AI** | LangChain, LangGraph, Mistral |
| **Persistence** | MongoDB, Mongoose |
| **Infrastructure** | Docker, Kubernetes, NGINX Ingress, Skaffold |
| **Authentication** | JWT, Google OAuth 2.0 |

## Repository Structure

```text
Loveable/
├── ai-orchestration/
├── auth/
├── k8s/
├── sandbox/
│   ├── agent/
│   ├── router/
│   ├── server/
│   └── template/
├── docs/
├── skaffold.yml
└── README.md
```

## Development

### Prerequisites

- Node.js 18+
- npm 9+
- Docker
- Kubernetes
- `kubectl`
- Skaffold

### Sandbox server

```bash
cd sandbox/server
npm install
npm run dev
```

### Sandbox template

```bash
cd sandbox/template
npm install
npm run dev
```

### Kubernetes

```bash
kubectl apply -f k8s/rbac.yml
kubectl apply -f k8s/sandbox-deployment.yml
kubectl apply -f k8s/sandbox-service.yml
kubectl apply -f k8s/ingress.yml
```

## Documentation

Development notes and sandbox setup material live under [`docs/`](./docs).

## Engineering Decisions

The repository is documented as the system evolves. Major architectural decisions are recorded alongside implementation so the project captures not only **what** was built, but **why** it was built that way.

Current areas of exploration include:

- sandbox isolation
- Kubernetes-based provisioning
- service boundaries
- AI tool orchestration
- preview routing
- authentication
- real-time communication
- persistence and synchronization

## Project Status

**Active development**

Features are being introduced incrementally, tested, documented, and integrated as the system evolves.

## License

ISC