# Technical Definition

Vivo. Cambia tecnica = editar.

## Stack

- Laravel 11+, PHP 8.3+, MySQL 8, Livewire, Flux UI, Pint, GitHub privado

## Arquitectura

- Patron:
- Modulos:
- Limites:

## Datos

- [modelo]: para / campos / relaciones / reglas

## Auth

- Login:
- Roles/permisos:
- Policies/gates:

## API

- No API MVP; o:
- Base `/api/v1`; docs `/docs`; spec `/openapi.json`; agente `ai/api-guide.md`
- Auth:
- Idempotencia:
- Rate limits:
- Error:

## Integraciones

- [integracion]: para / env / envia / recibe / error / log

## Jobs/files

- Jobs:
- Queues:
- Storage:
- Publico/privado:
- Retencion:

## Logging

- Si: errores, negocio critico, estados, irreversible, integraciones.
- No: secretos, sensibles, queries rutina, requests normales, exitos triviales.
- Default: `daily`; Telescope `local/staging`; prod `TELESCOPE_ENABLED=false`.

## Seguridad

- Secretos:
- Sensibles:
- Validacion:
- Autorizacion:
- Auditoria:
- Riesgos:

## Deploy

- cPanel + SSH
- `production-runbook.md`
- `github-private-repo.md`
- Key: `~/.ssh/deploy/[proyecto]/cpanel_ed25519`
- Webroot: `[project-path]/public`
- DNS listo

## Decisiones

- [fecha] [decision]: razon / tradeoff / impacto

## Supuestos

- 
