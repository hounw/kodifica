# [Nombre proyecto]

## Leer primero

```bash
tail -n 80 project-journal.md
```

- `product-definition.md` = que construir
- `technical-definition.md` = como funciona
- `project-journal.md` = que paso y por que
- `production-runbook.md` = deploy cPanel SSH
- `github-private-repo.md` = repo privado + deploy keys
- `app-overview.md` = `php artisan about`
- `routes.md` = `php artisan route:list`
- Si API: `ai/api-guide.md` + `/openapi.json`

## Reglas

- Stack: Laravel 11+, PHP 8.3+, MySQL 8, Livewire, Flux UI.
- Repo GitHub privado.
- Commits convencionales.
- Planear con herramienta. No mantener `implementation-plan.md`.
- Antes commit: `./vendor/bin/pint`.
- Despues commit:
  ```bash
  php artisan about > app-overview.md
  php artisan route:list > routes.md
  ```
- Despues commit: entrada en `project-journal.md`.
- Si cambia alcance/reglas/roles/flujos: actualizar `product-definition.md`.
- Si cambia arquitectura/datos/auth/API/infra/deploy: actualizar `technical-definition.md`.
- `.env` nunca repo. `.env.example` completo.
- No secretos en Markdown.
- Llaves privadas nunca en `/tmp`, `/private/tmp`, repo, sandbox. Usar `~/.ssh/deploy/[proyecto]/`.

## Produccion

- Seguir `production-runbook.md`.
- Llave cPanel: `~/.ssh/deploy/[proyecto]/cpanel_ed25519`, permiso `600`.
- PARAR antes migraciones.
- PARAR antes document root a `/public`.
- Datos no secretos al runbook.

## API

Si API:

- `/api/v1/...`
- Scramble: `/docs`, `/openapi.json`, `ai/api-guide.md`
- OpenAPI = verdad
- Bearer auth, permisos, rate limits, idempotencia, errores
- Operation IDs limpios, no Laravel-ish
