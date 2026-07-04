# AI API Guide

Verdad = `/openapi.json`.

## URLs

- Base: `https://[dominio]/api/v1`
- Docs: `/docs`
- Spec: `/openapi.json`
- Guia: `/ai/api-guide.md`

## Auth

```http
Authorization: Bearer [token]
```

- No token query/logs.
- Revisar scopes.
- `401` no auth. `403` no permiso.

## Version

- Usar `/api/v1/...`.
- No asumir compat majors.

## Error

```json
{"error":{"code":"validation_failed","message":"The given data was invalid.","fields":{}}}
```

Leer `error.code`.

## Idempotencia

POST riesgoso:

```http
Idempotency-Key: [stable-unique-key]
```

Misma key = mismo payload. Duda si paso = consultar estado.

## Retry

Si retry: `429`, `503`, timeout sin respuesta, endpoint seguro o key idempotente.

No retry: DELETE, update destructivo, POST sin key, `400`, `401`, `403`, `422`.

## Rate limit

Leer:

```http
X-RateLimit-Limit
X-RateLimit-Remaining
X-RateLimit-Reset
Retry-After
```

`429`: esperar `Retry-After`.

## Destructivo

- Confirmar recurso.
- Preferir preview/validate.
- No lote sin confirmacion.
- Reportar IDs.

## Endpoint docs

Cada endpoint: request ok, response ok, validation error, auth error.

## Tests

- `/docs`
- `/openapi.json` JSON valido
- `/ai/api-guide.md`
- error shape
- idempotencia
