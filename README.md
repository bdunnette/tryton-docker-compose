# tryton-docker-compose

Quickly set up a [Tryton](https://www.tryton.org/) server using [Docker Compose](https://docs.docker.com/compose/) (or [Podman](https://docs.podman.io/en/latest/markdown/podman-compose.1.html)!)

1. Copy example.env to .env
2. Edit variables in .env 
   + [VERSION](https://github.com/bdunnette/tryton-docker-compose/blob/bf5165935343b611336a8ea1652d6a0a40271d56/example.env#L1) sets Tryton server version (add `-office` after version number to enable reports in other formats like PDF)
   + [PG_VERSION](https://github.com/bdunnette/tryton-docker-compose/blob/bf5165935343b611336a8ea1652d6a0a40271d56/example.env#L2) sets Postgres database version
   + [PASSWORD](https://github.com/bdunnette/tryton-docker-compose/blob/bf5165935343b611336a8ea1652d6a0a40271d56/example.env#L4) is the default password for the `admin` user
3. Start the server with `docker compose up` or `podman-compose up`
