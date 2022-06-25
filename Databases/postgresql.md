# PostgreSQL
> Object relational database.

***
## Istallation

Docker compose:
```
services:s
      db:
        image: postgres
        restart: always
        ports: 
          - 5432:5432
        environment:
          POSTGRES_PASSWORD: "Sup3rS3cur3Pa55w0rd"
          # POSTGRES_USER: "admin"
          # POSTGRES_DB: "my_db"
        volumes:
          - ./database-data:/var/lib/postgresql/data/
```

Check the [docs](https://wiki.postgresql.org/wiki/Apt#Documentation) for Linux installation.

***
## Client installation psql

Intall from repository 13:

    sudo apt-get install postgresql-client

 Intall latest version 14:

    sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
    wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
    sudo apt-get update
    sudo apt-get -y install postgresql

***
## Connect to db-server

    pqsl -U postgres -h 0.0.0.0 -p 5432

***
## Basic commands

|  command                     |function                |
|---                           |---                     |
| \l                           | show databases         |
| create database my_database  | create a new database  |
| \c my_database               | use my_database        |




## Basic commands

    sudo su - postgres
    postgres@localhost:~$ psql
    psql (11.3 (Debian 11.3-1.pgdg90+1), servidor 10.8 (Debian 10.8-1.pgdg90+1))
    Digite «help» para obtener ayuda.

    postgres=# CREATE DATABASE basededatossur;
    CREATE DATABASE

    postgres=# CREATE USER new_username WITH PASSWORD 'my_password';
    postgres-# ALTER ROLE basemaster SET client_encoding TO 'utf8';
    ERROR:  error de sintaxis en o cerca de «ALTER»
    LÍNEA 2: ALTER ROLE basemaster SET client_encoding TO 'utf8';
             ^
    postgres=# CREATE USER new_username WITH PASSWORD 'my_password';

    CREATE ROLE
    postgres=# ALTER ROLE basemaster SET client_encoding TO 'utf8';
    ALTER ROLE
    postgres=# ALTER ROLE basemaster SET default_transaction_isolation TO 'read committed';
    ALTER ROLE
    postgres=# ALTER ROLE basemaster SET timezone TO 'UTC';
    ALTER ROLE
    postgres=# GRANT ALL PRIVILEGES ON DATABASE basededatossur TO basemaster;
    GRANT
    ALTER USER username CREATEDB;

Seleccionar base de datos para trabajar

```
\c my_database;
```

create a table inside the database:

```sql
CREATE TABLE accounts (
	user_id serial PRIMARY KEY,
	username VARCHAR ( 50 ) UNIQUE NOT NULL,
	password VARCHAR ( 50 ) NOT NULL,
	email VARCHAR ( 255 ) UNIQUE NOT NULL,
	created_on TIMESTAMP NOT NULL,
        last_login TIMESTAMP
);

```


Delete database:
```sql
DROP DATABASE [IF EXISTS] database_name;
```



# database migration

```
pg_dump -C -h localhost:5432 -U USERNAME PASSWORD | psql -h SERVER_IP:PORT -U USERNAME PASSWORD

docker exec CONTAINER_ID pg_dump -C -h localhost:5432 -U USERNAME PASSWORD | psql -h SERVER_IP -p PORT -U USERNAME PASSWORD
```