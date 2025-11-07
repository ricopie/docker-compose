# Docker Project - Home Lab Linux Server

## Docker Compose - Secret

You can generate password using `openssl rand -base64` or `openssl rand -hex`, and store that to folder `.secrets`

```console
foo@bar $ openssl rand -base64 48 | tr -dc 'A-Za-z0-9' | head -c 24

8oXFj6d6OpPsiCsAqH6WUnDt
```

Before using the random password, make sure to edit it in the compose file, with the following example. See [docs](https://docs.docker.com/build/building/secrets/#using-build-secrets) for more information.

```yaml
secret:
  MYSQL_ROOT_PASSWORD:
    file: '.secrets/mysql_root_passwd.txt'

  services:
    mariadb:
      environment:
        - MYSQL_ROOT_PASSWORD_FILE: /run/secrets/MYSQL_ROOT_PASSWORD
      secret:
        - MYSQL_ROOT_PASSWORD
```

---

### Using SSL Self-Signed with mkcert
See installation docs - [github.com/FiloSottile/mkcert](https://github.com/FiloSottile/mkcert?tab=readme-ov-file#installation)
