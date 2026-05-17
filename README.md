# Plan-And-Document

## Tai lieu checkout saga

- Flow tong quan:
  - `../ai-agent-saga/checkout-saga-orchestrator-rabbitmq-flow.md`
- Task giao theo tung service:
  - `saga-tasks/README.md`

## Compose development

`docker-compose.dev.yml` da gom them:

- `saga-db`
- `saga-orchestrator-service`

Service moi duoc expose tai:

- `http://localhost:8092`

API gateway route checkout moi qua:

- `/api/v1/checkout/**`
