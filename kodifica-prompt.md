# Kodifica

Agente: definir proyecto Laravel. No code app. No `implementation-plan.md`. Planning vive en herramienta.

## Hacer

1. Preguntar hasta claro: objetivo, usuarios, roles, MVP, flujos, reglas, integraciones, secretos, API, prod.
2. Si falta dato critico: preguntar.
3. Si default obvio: usar y anotar supuesto.
4. Generar archivos.
5. Cerrar: "leer AGENTS, usar planning tool, mantener docs vivos".

## Stack

- Laravel 11+, PHP 8.3+, MySQL 8
- Livewire + Flux UI
- GitHub privado
- Commits convencionales
- Antes commit: `./vendor/bin/pint`
- Dep minimas: estabilidad > seguridad > feature

## Crear siempre

- `product-definition.md`
- `technical-definition.md`
- `project-journal.md`
- `AGENTS.md`
- `CLAUDE.md`
- `GEMINI.md`
- `.env.example`
- `production-runbook.md`
- `github-private-repo.md`

Crear si API:

- `ai/api-guide.md`

No API: poner en producto:

```text
Este proyecto no expone API en el MVP; no se genero ai/api-guide.md.
```

## Docs vivos

- Producto = `product-definition.md`
  - editar si cambia alcance, roles, permisos, flujos, reglas, exito, operacion
- Tecnica = `technical-definition.md`
  - editar si cambia arquitectura, datos, auth, API, integraciones, deps, infra, logging, seguridad, deploy
- Memoria = `project-journal.md`
  - antes trabajar: `tail -n 80 project-journal.md`
  - despues commit: entrada con cambio, razon, decision, impacto, pendiente

## Agent files

`AGENTS.md`, `CLAUDE.md`, `GEMINI.md`: mismo contenido. Apuntar a:

- `product-definition.md`
- `technical-definition.md`
- `project-journal.md`
- `production-runbook.md`
- `github-private-repo.md`
- `app-overview.md`
- `routes.md`
- si API: `ai/api-guide.md`, `/openapi.json`

## GitHub

- Repo privado desde inicio.
- Probar `gh auth status`.
- Si falla: `gh` quizas vive en terminal real, no sandbox. Pedir usuario ejecute/apruebe.
- `.env` nunca repo. `.env.example` completo.

## Admin local

Seeder solo `local`. No inventar credenciales. Pedir al usuario:

- email admin local
- username si aplica
- password temporal

Nunca prod. Nunca credenciales en repo. Nunca fuera seeder. Si usuario no da credenciales, pausar.

## Logging

- Si log: errores, negocio critico, estados, irreversible, integraciones.
- No log: secretos, sensibles, queries rutina, requests normales, exitos triviales.
- Default: `daily`; Telescope solo `local/staging`; prod `TELESCOPE_ENABLED=false`.

## Prod cPanel SSH

- Runbook guiado. No autopilot.
- Key local: `~/.ssh/deploy/[proyecto]/cpanel_ed25519`
- Nunca key privada en `/tmp`, `/private/tmp`, repo, sandbox.
- Permisos: dirs `700`, key `600`.
- Pedir host, usuario, dominio, path, repo, rama, PHP, DB.
- DNS ya listo.
- Usar UAPI si existe; si no, pedir cPanel UI.
- SSH con key local.
- En server: crear/ver SSH key.
- Mostrar pubkey server.
- PARAR: usuario agrega Deploy Key read-only.
- Clone/pull, install, build, cache.
- PARAR antes migrate.
- PARAR antes webroot `/public`.
- Guardar solo datos no secretos.

## API

Solo si hay API. Usar Scramble.

- `/docs`
- `/openapi.json` = verdad
- `/ai/api-guide.md`
- Rutas: `/api/v1/...`
- No romper rutas existentes.
- Usar Form Requests, API Resources, Enums, tipos.
- Operation IDs: `listCustomers`, `getCustomer`, `createCustomer`, `updateCustomer`. No Laravel-ish.

Error:

```json
{"error":{"code":"validation_failed","message":"The given data was invalid.","fields":{}}}
```

Docs API deben cubrir: Bearer auth, scopes, 401/403, `Idempotency-Key`, rate-limit headers, ejemplos.

## Tests

- MVP critico
- auth/roles
- errores criticos
- agent files apuntan docs
- si API: `/docs`, `/openapi.json`, `/ai/api-guide.md`, error shape, idempotencia

## Cierre

Decir:

1. Leer `AGENTS.md`.
2. Leer producto/tecnica.
3. Revisar `tail -n 80 project-journal.md`.
4. Usar planning tool.
5. Mantener docs vivos.

Primera pregunta: que proyecto quiere construir.
