# MySQL cheat-sheet

> Simple commands and examples for MySQL.


## MySQL setup with docker-compose

> Using the docker-compose.yml file in this folder.


For testing, launch with:

```sh
docker-compose up -d
mysql -h '127.0.0.1' -P 3306  -u test -p'test' test 
``` 

* user: test
* password: test
* includes an init.sql file with a demo table




For production, change the following variables:

```sh
export MYSQL_ROOT_PASSWORD=some_value
export MYSQL_DATABASE=some_value
export MYSQL_USER=some_value
export MYSQL_PASSWORD=some_value
docker-compose up -d
mysql -h '127.0.0.1' -P 3306  -u $MYSQL_USER -p'$MYSQL_PASSWORD' $MYSQL_DATABASE
```


Show tables and basic selection:

    SHOW DATABASES;
    USE exampleDataBase;
    SHOW TABLES;
    SELECT * FROM exampleTable;


Create new user

    'newusername'@'localhost' IDENTIFIED BY 'userpassword';

Grant user privileges:

    GRANT SELECT, INSERT, UPDATE, DELETE ON database1 TO 'newusername'@'localhost';

Grant total control of a db:

    GRANT ALL ON database1 TO 'newusername'@'localhost';

To make it work, the user must have access to the database and table:

    GRANT ALL ON database1 TO 'newusername'@'localhost' IDENTIFIED BY 'userpassword';
    GRANT ALL ON tabla1 TO 'newusername'@'localhost'IDENTIFIED BY 'userpassword';

Updatae permission for table:

    FLUSH PRIVILEGES

Basic data inspection:

    SHOW COLUMNS FROM [table name]
    SHOW INDEX FROM TABLENAME [table name]
    SHOW TABLE STATUS LIKE [table name]

Create new table

    CREATE TABLE personnel
    (
    id int NOT NULL AUTO_INCREMENT,
    firstname varchar(25),
    lastname varchar(20),
    nick varchar(12),
    email varchar(35),
    salary int,
    PRIMARY KEY (id),
    UNIQUE id (id)
    );
