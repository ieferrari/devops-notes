# PostgreSQL
Object relational database.


***
## Linux installation
see [docs](https://wiki.postgresql.org/wiki/Apt#Documentation)

***
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
