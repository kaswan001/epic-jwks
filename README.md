# Epic FHIR JWKS (public)

Public JSON Web Key Set for Epic on FHIR **Backend Services** JWT verification.

**Do not put private keys in this repo.** Only `jwks.json` is public.

## GitHub Pages

1. Create a new **public** GitHub repo (e.g. `epic-jwks`).
2. Push this folder as the repo root.
3. **Settings → Pages → Deploy from branch** `main` / root (or `/docs` if you move files).
4. After deploy, open one of:
   - `https://<user>.github.io/epic-jwks/jwks.json`
   - `https://<user>.github.io/epic-jwks/.well-known/jwks.json`

## Epic app form

| Field | Value |
|-------|--------|
| Non-Production JWK Set URL | `https://<user>.github.io/epic-jwks/jwks.json` |
| Production JWK Set URL | same (or a separate prod JWKS later) |
| SMART on FHIR Version | R4 |
| SMART Scope Version | SMART v1 |

After saving, wait up to ~60 minutes for sandbox key sync.

## Connector env (private — keep local / secret store)

```bash
export EPIC_CLIENT_ID='<non-production-client-id>'
export EPIC_PRIVATE_KEY_PATH='/home/manish/projects/personal/epic-private-pkcs8.pem'
# or: export EPIC_PRIVATE_KEY="$(cat /home/manish/projects/personal/epic-private-pkcs8.pem)"
export EPIC_JWT_KID='epic-connector-1'
export EPIC_JWT_JKU='https://<user>.github.io/epic-jwks/jwks.json'
export EPIC_SCOPES='system/*.read'   # optional if scopes come from app registration
```

Signing algorithm expected by this connector: **RS384**.

## Key metadata

| Item | Value |
|------|--------|
| `kid` | `epic-connector-1` |
| `alg` | `RS384` |
| `kty` | `RSA` |
| Key size | 2048-bit |
| Private key (local only) | `~/projects/personal/epic-private-pkcs8.pem` |
