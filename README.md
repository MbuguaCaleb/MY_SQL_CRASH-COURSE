# MY_SQL_CRASH-COURSE

MySQL queries reference.

**Relational DataBase Systems**

**Mysql**

```
(a)It is an open source relational database managent system..There are also other types of databases such as NOSQL,Distributed and graph databses.


Mysql is one of the relational databases others include postgrsql,Oracle Database and Microsoft SQL server and Firebird.

(b)
Most of the relational databases uses sql..

Depending on the type of database there are very different chnges..


(c)It is a leading database for web applications.

(d)It is used for small APPS to large enterprise apps

(e)It is used with mutiple languages eg (PHP,Node,Python and C#)


(f)Cross platform...any OS

```

**Relational DATABASE\***

```

(a)Based on the relational model of data.

(b)Virtually all RDBMS use sql to manage them.

(c)Uses tables with columns and rows.

(d)Tables can relate to each other via the use of keys.


```

**TABLES AND DATATYPES **

```
Each field in the table has a specific datatype...

Common datatypes are:

(a)Numeric -INT,TINYINT,BIGINT,FLOAT.

(b)String - VARCHAR,TEXT and CHAR.

(c)Dates - DATE,DATETIME and TIMESTAMP.

```

**TABLE RELATIONSHIPS**

```
Each table has a unique identifier which is called the primary key tables can have  relationships via the foreign keys..(When a primary key of one table is a  field in the other)

This you can also have table joins where you query fro

```

**Installation and environment**

```

(a)Local

(i)Terminal/GUI install -Standalone Server.

(ii)XAMPP,MAMP,WAMP (Usually for local development)


(b)Production

(i)Terminal installation via Linux package manager eg in a D.O Server

(ii)Sofware server (C Panel,etc )


```

**ManagementTools**

```
(a)Terminal, commandline or shell...

(b)Desktop tools -MYSQL Workbench,etc.

(c)WebBased tools -PHPMyAdmin etc..


```

# QUERIES

```
(a)MySQL When stored is stored in a particular path..(linux /var/.......)

(b)IT IS A COMMON COVENTION TO USE CAPS FOR THE QUERIES...ITS BETTER..(FOR READABILITY)


```

**LogIn**

```
mysql -u root -p
```

**CREATEUSER**

```
CREATE USER 'someuser'@'localhost' IDENTIFIED BY 'somepassword';

```

**Show Users**

```

SELECT user, host FROM mysql.user;

```

**Grant All Priveleges On All Databases**

```

GRANT ALL PRIVILEGES ON * . * TO 'caleb'@'localhost';

FLUSH PRIVILEGES;


Flush privildedges clears the grants table and should be done when you assign priviledges.

```

**Show Grants**

```
SHOW GRANTS FOR 'someuser'@'localhost';


```

**Remove Grants**

```
REVOKE ALL PRIVILEGES, GRANT OPTION FROM 'someuser'@'localhost';

```

**DeleteUser**

```
DROP USER 'someuser'@'localhost';

```

**Exit**

```
exit
```

**Create Database**

```
CREATE DATABASE acme;

```

**Show Databases**

```
SHOW DATABASES

```

**SELECT DATABASE**

```
USE acme;

```

**CREATE A TABLE**

```
CREATE TABLE users(
id INT AUTO_INCREMENT,
first_name VARCHAR(100),
last_name VARCHAR(100),
email VARCHAR(50),
password VARCHAR(20),
location VARCHAR(100),
dept VARCHAR(100),
is_admin TINYINT(1),
register_date DATETIME,
PRIMARY KEY(id)
);

```

**SHOW TABLES**

```

SHOW TABLES;

```

**DELETE OR DROP TABLE**

```
DROP TABLE tablename;

```

**INSERT ROW /RECORD**

```


INSERT INTO users (first_name, last_name, email, password, location, dept, is_admin, register_date) values ('Brad', 'Traversy', 'brad@gmail.com', '123456','Massachusetts', 'development', 1, now());


```
