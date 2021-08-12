# heruku deploy, for django

## Install Requirements

    cd app_folder
    sudo apt update
    sudo apt install snapd
    sudo apt-get install heroku


agregar el achivo .keep (para arreglar [este](https://stackoverflow.com/questions/36442043/trying-to-push-my-app-to-heroku-gives-me-this-error-filenotfounderror-errno-2) error)

    touch .keep

Guardar cambios con git y hacer un push a heroku

    git add .
    git commit -m "Demo"
    git push <appName>  master
    heroku open


***
## Para usar postgresql en la aplicación de heroku

instalar paquetes

    sudo pip3 install psycopg2-binary
    sudo pip3 install dj-database-url

agregar a requerimets.txt

    psycopg2-binary
    dj-database-url


agregar a settings.py

    import dj_database_url
    DATABASES['default'] = dj_database_url.config(conn_max_age=600, ssl_require=True)

***
ver documentacion  
* [set-up-postgres-on-linux](https://devcenter.heroku.com/articles/heroku-postgresql#set-up-postgres-on-linux)
* [creating-a-backup](https://devcenter.heroku.com/articles/heroku-postgres-backups#creating-a-backup)


ver estado de la base de datos

    heroku pg:info


pg:push pushes data from a local database into a remote Heroku Postgres database. The command looks like this:


    PGUSER=basemaster PGPASSWORD=my-password  heroku pg:push my_app HEROKU_POSTGRESQL_AQUA_URL --app my_app


    PGUSER=basemaster PGPASSWORD=my-password heroku pg:pull HEROKU_POSTGRESQL_PURPLE_URL my_app --app my_app

pip install psycopg2-binary


***
cambiar pass local postgres:

    sudo passwd postgres

crear nuevo usuario en posgres

    su postgres
    psql
    CREATE USER "user" WITH PASSWORD 'my_pasword';




CREAR POSTGRESQL DB EN HEROKU

    heroku addons:create heroku-postgresql:hobby-dev
HEROKU_POSTGRESQL_AQUA_URL

VER DB INSTALADAS EN HEROKU

    heroku addons


CONECTARSE A NUESTRA DB EN HEROKU

    heroku pg:psql


resetear POSTGRESQL DB EN HEROKU

    heroku pg:reset HEROKU_POSTGRESQL_RED_URL


borrar db en heroku

    heroku addons:destroy HEROKU_POSTGRESQL_PURPLE



***


## PUSH DB FROM LOCAL TO HEROKU      
PGUSER debe ser igual a usuario que ejecuta el heroku pg:push !!!!!!!!!!

    user@localhost$ PGUSER=user PGPASSWORD=my_pasword heroku pg:push my_app HEROKU_POSTGRESQL_AQUA --app my_app

    grant all user root ownership from dbeaver


***
## CONNECT TO DJANGO

    pip install dj-database-url
