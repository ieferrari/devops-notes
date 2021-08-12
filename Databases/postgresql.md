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
