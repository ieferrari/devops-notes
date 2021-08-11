# MySQL cheat-sheet
Simple commands and examples for MySQL.


Login:

    $ mysql -u root -p password

Show tables and basic selection:

    SHOW DATABASES;
    USE exampleDataBase;  //se conecta a una db
    SHOW TABLES;
    SELECT * FROM exampleTable; // muestra el contenido de una tabla


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
