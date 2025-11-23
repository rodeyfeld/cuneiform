# Cuneiform - Secrets Management

Self-hosted **Cuneiform** (powered by [OpenBao](https://openbao.org/)) instance for secrets management in the Universe ecosystem.

## Local Development

Run the development server (in-memory, with root token "root"):

```bash
docker compose up
```

Access the UI at http://localhost:8200
Token: `root`

## Production

In production, Cuneiform runs on Kubernetes with Raft storage backend for persistence and high availability.

### Unsealing

When deployed to production, Cuneiform starts sealed. You must initialize and unseal it:

```bash
# Forward port
kubectl port-forward svc/cuneiform-service 8200:8200 -n galaxy

# Initialize (save the keys!)
export BAO_ADDR='http://127.0.0.1:8200'
bao operator init

# Unseal (run 3 times with different keys)
bao operator unseal <key>
```
