# Changelog — Sovereign AWS DataEng

All notable changes follow [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) format.
Versioning follows [Semantic Versioning](https://semver.org/).

## [Unreleased]

### Added
- Full ecosystem documentation suite (ARCHITECTURE, DEVELOPER_GUIDE, SME_PLAYBOOK, SOP)
- GitHub Actions CI matrix (Python 3.10 / 3.11 / 3.12)
- Multistage Dockerfile with non-root user, health check, OCI labels
- docker-compose.yml with SBB platform network
- n8n custom node integration via `SovereignTools`
- `.env.example` environment template
- CONTRIBUTING, CODE_OF_CONDUCT, SECURITY governance files
- OpenAPI 3.1 compatible REST API spec
- Bandit security scan in CI

## [1.0.0] — 2024-01-01

### Added
- Initial production release of Sovereign AWS DataEng (PKG-021)
- Core microservice on port `8801`
- n8n webhook adapter (`n8n/webhook_adapter.py`)
- REST API (`POST /api/v1/execute`, `GET /health`)
- Components: GlueJobRunner, S3DataLake, AthenaQueryEngine, RedshiftLoader, CostOptimizer
- pyproject.toml packaging with `[dev]` extras
- CLI: `sovereign-aws-dataeng --help`
- Unit test suite (pure `unittest.TestCase`, no external test framework required)

### Domain: Cloud Data Engineering & ETL
Serverless ETL orchestrator for AWS Glue, S3, Athena, and Redshift. Manages data pipelines, schema evolution, and cost-optimized query execution.

[Unreleased]: https://github.com/BlackFoxgamingstudio/aws-dataeng/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/BlackFoxgamingstudio/aws-dataeng/releases/tag/v1.0.0
