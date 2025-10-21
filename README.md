# tryton-docker-compose

Quickly set up a [Tryton](https://www.tryton.org/) server using [Docker Compose](https://docs.docker.com/compose/) (or [Podman](https://docs.podman.io/en/latest/markdown/podman-compose.1.html)!)

## Installation

1. Copy example.env to .env
2. Edit variables in .env 
   + **TRYTON_VERSION** is the Tryton version to use (default: 7.0 - add '-office' to allow exporting of reports to non-OpenDocument formats like PDF)
   + **PG_VERSION** is the PostgreSQL version to use (default: 17.x)
   + **ADMIN_EMAIL** is the email for the 'admin' user (default: admin@example.com)
   + **ADMIN_PASSWORD** is the initial password for the 'admin' Tryton user (default: admin)
   + **DB_PASSWORD** is the PostgreSQL database password (default: change_this_please)

3. Start the server with `docker compose up` or `podman-compose up`

## Managing containers 

Once containers are running, you can:

### Activate modules

```bash
docker compose run --rm server trytond-admin -c /etc/trytond.conf -d tryton --all --verbose
docker compose run --rm server trytond-admin -c /etc/trytond.conf -d tryton --activate-dependencies --verbose -u production
```

### Import currencies and locations

```bash
docker compose run --rm server trytond_import_countries -c /etc/trytond.conf -d tryton
docker compose run --rm server trytond_import_currencies -c /etc/trytond.conf -d tryton
docker compose run --rm server trytond_import_postal_codes -c /etc/trytond.conf -d tryton US
```

### Backup database

```bash
podman-compose exec postgres sh -c "pg_dump -U postgres -Fc tryton > tryton-demo.dump"
podman cp tryton_postgres_1:tryton-demo.dump .
```

## Restore database

```bash
podman-compose exec postgres sh -c "pg_restore -U postgres -d tryton tryton-demo.dump"
```
