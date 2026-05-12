# dotnet-on-k8s

> ASP.NET Core workloads on Kubernetes — a portfolio project documenting 
> the journey from .NET developer to Platform Engineer.

## What this is

A hands-on portfolio project documenting the transition from Senior .NET Developer 
to Platform Engineer. Each milestone introduces a new layer of the platform stack:

- **M1** — ASP.NET Core app deployed on local Kubernetes (kind)
- **M2** — Helm chart + Argo CD (GitOps)
- **M3** — Observability: OpenTelemetry, Prometheus, Grafana
- **M4** — PostgreSQL on Kubernetes with persistent storage
- **M5** — Terraform module published to registry.terraform.io

## Architecture

```
┌─────────────────────────────────────────┐
│           kind cluster (local)          │
│                                         │
│  ┌─────────────┐     ┌───────────────┐  │
│  │  Deployment │────▶│      Pod      │  │
│  │ hello-world │     │  ASP.NET Core │  │
│  └─────────────┘     └───────────────┘  │
│                              │          │
│                    ┌─────────▼───────┐  │
│                    │    Service      │  │
│                    │   ClusterIP     │  │
│                    └─────────────────┘  │
└─────────────────────────────────────────┘
```

**Current stack:**
- Runtime: .NET 9 / ASP.NET Core
- Container: Docker (multi-stage build)
- Orchestration: Kubernetes (kind)
- Local tooling: kubectl, helm, k9s

## Prerequisites

- [Docker](https://docs.docker.com/engine/install/) 
- [kind](https://kind.sigs.k8s.io/docs/user/quick-start/) 
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [.NET 9 SDK](https://dotnet.microsoft.com/download)

## Quick Start

Clone the repository:
```bash
git clone https://github.com/mikolaj-k/dotnet-on-k8s.git
cd dotnet-on-k8s
```

Create the cluster:
```bash
kind create cluster --name dotnet-on-k8s
```

Build and load the image:
```bash
docker build -t hello-world:v1 src/HelloWorld/
kind load docker-image hello-world:v1 --name dotnet-on-k8s
```

Deploy with Helm:
```bash
helm install hello-world ./charts/hello-world
```

Verify:
```bash
kubectl port-forward service/hello-world 8080:80
curl http://localhost:8080/weatherforecast
```

## Project Structure

```
dotnet-on-k8s/
├── src/
│   └── HelloWorld/           # ASP.NET Core application
│       ├── Dockerfile         # Multi-stage build
│       └── HelloWorld.csproj
├── charts/
│   └── hello-world/           # Helm chart
│       ├── Chart.yaml          # Chart metadata
│       ├── values.yaml         # Default values
│       └── templates/
│           ├── deployment.yaml
│           └── service.yaml
└── docs/
    └── adr/                   # Architecture Decision Records
        └── ADR-001-local-kubernetes-kind.md
```

## Architecture Decision Records

| ADR | Decision | Status |
|-----|----------|--------|
| [ADR-001](docs/adr/ADR-001-local-kubernetes-kind.md) | Local Kubernetes: kind over minikube/k3d | Accepted |

## Roadmap

- [x] M1 — ASP.NET Core on local Kubernetes (kind)
- [x] M2 — Helm chart + Argo CD (GitOps)
- [ ] M3 — Observability: OpenTelemetry, Prometheus, Grafana
- [ ] M4 — PostgreSQL on Kubernetes with persistent storage
- [ ] M5 — Terraform module published to registry.terraform.io

## Author

Mikołaj Klimas
