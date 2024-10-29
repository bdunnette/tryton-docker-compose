# tryton-docker-compose

Quickly set up a [Tryton](https://www.tryton.org/) server using [Docker Compose](https://docs.docker.com/compose/) (or [Podman](https://docs.podman.io/en/latest/markdown/podman-compose.1.html)!)

1. Copy example.env to .env
2. Edit variables in .env 
   + VERSION sets Tryton server version (add `-office` after version number to enable reports in other formats like PDF)
   + PG_VERSION sets Postgres database version
   + PASSWORD is the default password for the `admin` user
3. Start the server with `docker compose up` or `podman-compose up`
