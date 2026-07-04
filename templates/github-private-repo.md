# GitHub Private Repo

Repo privado desde inicio.

## `gh`

```bash
gh auth status
```

Si falla: puede estar logueado en terminal real, no sandbox. Pedir al usuario ejecutar o aprobar acceso.

## Crear

```bash
git init
git add .
git commit -m "chore: initial project scaffold"
gh repo create [org-or-user]/[repo] --private --source=. --remote=origin --push
```

Repo ya existe:

```bash
git remote add origin git@github.com:[org-or-user]/[repo].git
git push -u origin main
```

## Reglas

- Privado.
- `.env` nunca.
- `.env.example` completo.
- Commits convencionales.
- Pint antes commit si Laravel instalado.

## Deploy key servidor

1. En servidor: generar/ver `~/.ssh/id_ed25519.pub`.
2. Mostrar pubkey.
3. PARAR.
4. Usuario agrega Deploy Key read-only en GitHub.
5. Luego clone/pull.
