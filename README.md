# SecureFleet

A secure cloud control plane and DeviceOps Console for LinuxEdge gateways and their attached devices. It is independently demonstrable through a simulated-device service.

## Languages

- C# with ASP.NET Core for APIs, ingestion, domain logic, and workers.
- TypeScript with React for the operations console.
- SQL for PostgreSQL migrations and diagnostics.
- HCL for Terraform.
- YAML for CI/CD, containers, and optional Kubernetes/Helm configuration.

## Suggested structure

```text
securefleet/
├── backend/
│   ├── src/
│   │   ├── Api/
│   │   ├── Application/
│   │   ├── Domain/
│   │   ├── Infrastructure/
│   │   ├── Ingestion/
│   │   └── Workers/
│   └── tests/
├── frontend/
│   ├── src/features/
│   ├── src/components/
│   └── tests/
├── simulator/            # Hundreds of deterministic fake devices
├── infrastructure/
│   ├── terraform/
│   ├── docker/
│   └── helm/             # Optional later milestone
├── observability/        # Dashboards, alerts, and collector config
├── .gitignore
├── ARCHITECTURE.md
└── README.md
```

## Potential backend packages

- ASP.NET Core and SignalR
- Entity Framework Core with Npgsql
- MQTTnet
- MassTransit with RabbitMQ only when asynchronous workflows justify a broker
- FluentValidation
- OpenIddict or standards-based integration with an external OIDC provider
- OpenTelemetry packages
- Serilog
- Hangfire or Quartz.NET for scheduled/background work; choose one
- Testcontainers for integration tests
- xUnit, FluentAssertions, and optionally NSubstitute

## Potential frontend packages

- React, TypeScript, and Vite
- React Router
- TanStack Query and TanStack Table
- Zod
- a restrained component system such as MUI or shadcn/ui
- Recharts for operational charts
- Vitest and React Testing Library
- Playwright for end-to-end tests

## Infrastructure packages and services

- PostgreSQL, Redis, and an MQTT broker
- Docker and Docker Compose
- Terraform with AWS provider
- OpenTelemetry Collector, Prometheus, and Grafana
- Kubernetes and Helm only after the Docker deployment is complete

## Independent demonstration

Run the backend, UI, and simulated-device generator locally. Demonstrate registration, health, telemetry, commands, signed release metadata, canary deployment, automatic pause, and rollback decisions.

## Integration

LinuxEdge is the primary managed device. SecureFleet consumes only the cloud contracts and never links LinuxEdge source code. HILForge may call public APIs for end-to-end deployment tests.

