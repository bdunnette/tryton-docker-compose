# tryton-docker-compose

Quickly set up a [Tryton](https://www.tryton.org/) server using [Docker Compose](https://docs.docker.com/compose/) (or [Podman](https://docs.podman.io/en/latest/markdown/podman-compose.1.html)!)

## Installation

1. Copy example.env to .env
2. Edit variables in .env 
   + [VERSION](https://github.com/bdunnette/tryton-docker-compose/blob/bf5165935343b611336a8ea1652d6a0a40271d56/example.env#L1) sets Tryton server version (add `-office` after version number to enable reports in other formats like PDF)
   + [PG_VERSION](https://github.com/bdunnette/tryton-docker-compose/blob/bf5165935343b611336a8ea1652d6a0a40271d56/example.env#L2) sets Postgres database version
   + [PASSWORD](https://github.com/bdunnette/tryton-docker-compose/blob/bf5165935343b611336a8ea1652d6a0a40271d56/example.env#L4) is the default password for the `admin` user
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
podman-compose exec postgres sh -c "pg_dump -U postgres tryton > tryton-demo.sql"
podman cp tryton_postgres_1:tryton-demo.sql .
```

or, using `pg_dump` format:

```bash
podman-compose exec postgres sh -c "pg_dump -U postgres -Fc tryton > tryton-demo.dump"
podman cp tryton_postgres_1:tryton-demo.dump .
```

## Restore database

```bash
podman-compose exec postgres sh -c "psql -U postgres tryton < tryton-demo.sql"
```

if using `pg_dump` format:

```bash
podman-compose exec postgres sh -c "pg_restore -U postgres -d tryton tryton-demo.dump"
```
