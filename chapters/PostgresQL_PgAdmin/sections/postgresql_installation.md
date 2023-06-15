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

````{tab-item} load_extensions.sh
```
#!/bin/sh

# You could probably do this fancier and have an array of extensions
# to create, but this is mostly an illustration of what can be done

# Data Scientist and Every other Developer-Motive: Better have it and not need it than need it not have it.

createuser postgis_user
createdb postgis_db -O postgis_user

psql -v ON_ERROR_STOP=1 --username postgres <<EOF
CREATE EXTENSION IF NOT EXISTS pgcrypto;
CREATE EXTENSION IF NOT EXISTS pgaudit;
CREATE EXTENSION IF NOT EXISTS pg_repack;
CREATE EXTENSION IF NOT EXISTS hstore;
CREATE EXTENSION IF NOT EXISTS pg_trgm;
CREATE EXTENSION IF NOT EXISTS file_fdw;
CREATE EXTENSION IF NOT EXISTS dblink;
CREATE EXTENSION IF NOT EXISTS btree_gin;
CREATE EXTENSION IF NOT EXISTS btree_gist;
CREATE EXTENSION IF NOT EXISTS chkpass;
CREATE EXTENSION IF NOT EXISTS pg_cron;
CREATE EXTENSION IF NOT EXISTS lo;
CREATE EXTENSION IF NOT EXISTS pg_repack;
CREATE EXTENSION IF NOT EXISTS pglogical;
CREATE EXTENSION IF NOT EXISTS pg_stat_statements;
CREATE EXTENSION IF NOT EXISTS postgres_fdw;
CREATE EXTENSION IF NOT EXISTS seg;
CREATE EXTENSION IF NOT EXISTS sslinfo;
CREATE EXTENSION IF NOT EXISTS uuid-ossp;
CREATE EXTENSION IF NOT EXISTS xml2;
CREATE EXTENSION IF NOT EXISTS pageinspect;
CREATE EXTENSION IF NOT EXISTS pg_buffercache;
CREATE EXTENSION IF NOT EXISTS isn;
CREATE EXTENSION IF NOT EXISTS amcheck;
CREATE EXTENSION IF NOT EXISTS fuzzystrmatch;
CREATE EXTENSION IF NOT EXISTS postgresql_anonymizer;
CREATE EXTENSION IF NOT EXISTS pgagent;
select * FROM pg_extension;
EOF

psql -d postgis_db -v ON_ERROR_STOP=1 --username postgres <<EOF
CREATE EXTENSION postgis;
CREATE EXTENSION postgis_topology;
EOF
```
````
`````

In the docker compose file the environment variables we set are for the postgres superuser
