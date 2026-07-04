# Production Runbook - cPanel SSH

No secretos. No passwords/tokens/private keys/`.env`.

## Datos

- host
- usuario
- dominio/subdominio
- path
- repo/rama
- PHP
- DB name/user

DNS listo.

## 1. Key local

Nunca `/tmp`, `/private/tmp`, repo, sandbox.

```text
~/.ssh/deploy/[proyecto]/cpanel_ed25519
```

```bash
mkdir -p ~/.ssh/deploy/[proyecto]
chmod 700 ~/.ssh ~/.ssh/deploy ~/.ssh/deploy/[proyecto]
test -f ~/.ssh/deploy/[proyecto]/cpanel_ed25519.pub && cat ~/.ssh/deploy/[proyecto]/cpanel_ed25519.pub
```

Si no existe:

```bash
ssh-keygen -t ed25519 -C "[proyecto]-cpanel-deploy" -f ~/.ssh/deploy/[proyecto]/cpanel_ed25519
chmod 600 ~/.ssh/deploy/[proyecto]/cpanel_ed25519
chmod 644 ~/.ssh/deploy/[proyecto]/cpanel_ed25519.pub
cat ~/.ssh/deploy/[proyecto]/cpanel_ed25519.pub
```

SSH:

```bash
ssh -i ~/.ssh/deploy/[proyecto]/cpanel_ed25519 [usuario]@[host]
```

## 2. Repo

Privado + push. Si no: `github-private-repo.md`.

## 3. Key servidor

En server:

```bash
test -f ~/.ssh/id_ed25519.pub || ssh-keygen -t ed25519 -C "[proyecto]-server-deploy" -f ~/.ssh/id_ed25519
cat ~/.ssh/id_ed25519.pub
```

PARAR. Usuario agrega GitHub Deploy Key read-only.

## 4. cPanel

Si UAPI:

```bash
uapi Mysql create_database name='[db_name]'
uapi Mysql create_user name='[db_user]' password='[secure_password]'
uapi Mysql set_privileges_on_database user='[db_user]' database='[db_name]' privileges='ALL PRIVILEGES'
uapi SubDomain addsubdomain domain='[subdomain]' rootdomain='[root-domain]' dir='[document-root]'
```

Sin UAPI: usuario usa cPanel UI. Documentar bloqueo.

## 5. Code

```bash
git clone git@github.com:[org]/[repo].git [project-path]
cd [project-path]
```

Update:

```bash
cd [project-path]
git pull --ff-only origin [branch]
```

## 6. Laravel

Crear `.env` desde `.env.example`. No copiar secretos aqui.

```bash
composer install --no-dev --optimize-autoloader
npm ci
npm run build
php artisan key:generate --force
php artisan storage:link
php artisan config:cache
php artisan route:cache
php artisan view:cache
```

## 7. Migrate

PARAR. Preguntar.

```bash
php artisan migrate --force
```

No seed local en prod.

## 8. Webroot

PARAR. Apuntar dominio a:

```text
[project-path]/public
```

## 9. Ver

```bash
php artisan about
php artisan route:list
```

Probar home/login/flujos. Si API: `/docs`, `/openapi.json`, `/ai/api-guide.md`.

## Log no secreto

- Host:
- Usuario:
- Dominio:
- Path:
- Repo/rama:
- PHP:
- Fecha:
- Notas:
