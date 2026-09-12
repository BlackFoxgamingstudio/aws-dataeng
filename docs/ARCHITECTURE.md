# Architecture: Sovereign AWS DataEng

## Overview

**Package ID:** `PKG-021`  
**Domain:** Cloud Data Engineering & ETL  
**Microservice Port:** `8801`  
**n8n Webhook Path:** `aws-dataeng-trigger`  
**GitHub:** [BlackFoxgamingstudio/aws-dataeng](https://github.com/BlackFoxgamingstudio/aws-dataeng)

Serverless ETL orchestrator for AWS Glue, S3, Athena, and Redshift. Manages data pipelines, schema evolution, and cost-optimized query execution.

---

## System Architecture

```
                     ┌──────────────────────────────────┐
                     │       Sovereign AWS DataEng         │
                     │       Port: 8801            │
                     ├──────────────┬───────────────────┤
   n8n Webhook ────▶ │  REST API    │   Core Engine     │
   HTTP POST         │  /api/v1/*   │   Dispatcher      │
                     └──────┬───────┴────────┬──────────┘
                            │                │
              ┌─────────────▼────────────────▼─────────┐
              │          Component Layer                 │
              │  GlueJobRunner   | S3DataLake      | AthenaQueryE  │
              └────────────────────────┬────────────────┘
                                       │
              ┌────────────────────────▼────────────────┐
              │      n8n Central Event Bus (:5678)       │
              └─────────────────────────────────────────┘
```

## Core Components

### `GlueJobRunner`
Handles all gluejobrunner operations. Exposes async methods callable from the core dispatcher.

### `S3DataLake`
Handles all s3datalake operations. Exposes async methods callable from the core dispatcher.

### `AthenaQueryEngine`
Handles all athenaquery operations. Exposes async methods callable from the core dispatcher.

### `RedshiftLoader`
Handles all redshiftloader operations. Exposes async methods callable from the core dispatcher.

### `CostOptimizer`
Handles all costoptimizer operations. Exposes async methods callable from the core dispatcher.

---

## API Contract

All interactions follow the SBB standard envelope:

```http
POST /api/v1/execute
Content-Type: application/json
X-SBB-API-Key: <api-key>

{
  "action": "<operation>",
  "payload": {},
  "trace_id": "optional-uuid"
}
```

**Success Response (HTTP 200):**
```json
{
  "status": "success",
  "data": {},
  "trace_id": "...",
  "timestamp": "2025-01-01T00:00:00Z"
}
```

**Health Check:**
```http
GET /health
→ {"status": "healthy", "service": "sovereign-aws-dataeng", "port": 8801}
```

## Integration Matrix

| System | Protocol | Direction | Purpose |
|--------|----------|-----------|---------|
| n8n Event Bus (:5678) | HTTP POST | Outbound | Event forwarding |
| n8n Webhook | HTTP POST | Inbound | Trigger execution |
| SBB Codebase Vault (:8766) | HTTP | Outbound | Code analysis |
| SBB Patterns Bible (:8794) | HTTP | Outbound | Standards validation |
| External APIs | HTTPS | Outbound | Domain-specific data |

## Deployment Architecture

```yaml
# docker-compose excerpt
sovereign-aws-dataeng:
  image: sovereign-aws-dataeng:latest
  ports: ["8801:8801"]
  healthcheck:
    test: curl -f http://localhost:8801/health
    interval: 30s
```

## Security Model

| Control | Implementation |
|---------|---------------|
| Authentication | `X-SBB-API-Key` header (env: `SBB_API_KEY`) |
| Rate Limiting | 100 req/min per client IP |
| Input Validation | Pydantic models (strict mode) |
| Container Security | Non-root user (`appuser:1001`) |
| Secrets | Environment variables only (never hardcoded) |
| TLS | Terminate at reverse proxy (nginx/caddy) |

## Tags
`aws`, `etl`, `glue`, `s3`, `athena`
