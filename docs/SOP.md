# Standard Operating Procedure: Sovereign Aws Dataeng

## 1. Service Health Verification
Run `sovereign-aws-dataeng --health` to confirm the engine responds with status `HEALTHY`.

## 2. Webhook Adapter Operation
The webhook adapter listens on port `8801`:
```bash
python3 n8n/webhook_adapter.py
```
If port 8801 is occupied, check active processes:
```bash
lsof -i :8801
```

## 3. n8n Integration Testing
Send a probe POST request:
```bash
curl -X POST http://localhost:8801/api/v1/execute \
  -H "Content-Type: application/json" \
  -d '{"action": "health_ping", "payload": {"test": true}}'
```
