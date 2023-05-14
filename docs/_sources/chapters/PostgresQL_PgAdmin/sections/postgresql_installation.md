# PostgresQL Installation

## PostgresQL Docker Installation

`````{tab-set}
````{tab-item} Dockerfile
```
FROM postgres:15.2-bullseye

ENV LANG en_US.utf8

RUN apt-get update && apt-get upgrade -y

RUN set -ex; \
	if ! command -v gpg > /dev/null; then \
		apt-get update; \
		apt-get install -y --no-install-recommends \
			gnupg \
			dirmngr \
		; \
		rm -rf /var/lib/apt/lists/*; \
	fi

RUN apt-get install -y curl ca-certificates gnupg postgresql-common

RUN curl https://www.postgresql.org/media/keys/ACCC4CF8.asc | gpg --dearmor | tee /etc/apt/trusted.gpg.d/apt.postgresql.org.gpg >/dev/null
RUN touch /etc/apt/sources.list.d/pgdg.list
RUN sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt bullseye-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
RUN apt install -y postgresql-common pgagent
RUN apt-get update 
COPY load_extensions.sh /docker-entrypoint-initdb.d
STOPSIGNAL SIGINT
EXPOSE 5432
```
````

````{tab-item} docker-compose
This is the docker compose for the postgresql database and pgadmin combo

```docker
version: '3'

services:
  postgres_dbserver:
    user: root
    restart: always
    build: 
      context: .
      dockerfile: postgresql_Dockerfile
    container_name: postgres_dbserver_master
    env_file:
      - postgresql_prod_env.env
    ports:
      - 54320:5432
    volumes:
      - <host-os-drive-path-in-disk>:/var/lib/postgresql/data

  pgadmin:
    image: dpage/pgadmin4:latest
    user: root
    restart: always
    env_file:
      - pgadmin4_prod_env.env
    ports:
        - 54321:5050
    volumes:
        - <host-os-drive-path-in-disk>:/var/lib/pgadmin
    depends_on:
        - postgres_dbserver

```


````
`````
