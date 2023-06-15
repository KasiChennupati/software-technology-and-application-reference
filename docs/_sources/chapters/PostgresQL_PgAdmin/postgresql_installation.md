# PostgresQL Installation

## PostgresQL Docker Installation

```docker
version: '3'

services:
  kc_postgresql:
    user: root
    restart: always
    build: 
      context: .
      dockerfile: postgresql_Dockerfile
    env_file:
      - postgresql_prod_env.env
    ports:
      - 54320:5432
    volumes:
      - /D/docker_space/data_link/kc_postgresql/postgresql/data/:/var/lib/postgresql/data/

  pgadmin:
    image: dpage/pgadmin4:latest
    user: root
    restart: always
    env_file:
      - pgadmin4_prod_env.env
    ports:
        - 54321:5050
    volumes:
        - /D/docker_space/data_link/kc_postgresql/pgadmin4/:/var/lib/pgadmin
    depends_on:
        - kc_postgresql

```

## Contributing

Do you wnat to contribute?

The best way is to raise a Github Issue !

Thank You !
