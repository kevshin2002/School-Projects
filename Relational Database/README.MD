# Relational Database
This project was made for ECE 141B Spring 2023 with Professor Rick Gessner but redone independently of the class.

As it is currently a work in progress, please refer to the [Relational Database](https://github.com/kevshin2002/Relational-Database) repository.

## Work in Progress
- Select Command
- Update Command

## Future Features
- Left/Right Join
- Indexing
- Caching

## Commands
All commands will be followed by how long each command took beginning from tokenization to execution. The speed is dependent on your computer.

### Database Commands
#### Create
In order to create a database, you must follow this format:
```bash
create database {db-name} -- create a new DB (storage file) with the given name in your storage folder
```

Example:
```bash
create database testDB;
Query OK, 1 row affected (0.0010646 sec)
```

This command will create a file at "/Files", where the root is the location of this project. 

#### Drop
```bash
drop database {db-name} -- delete a named DB
```

Example:
```bash
drop database testDB;
Query OK, 0 row affected (0.0011903 sec)
```

This command will delete the file with the name testDB;

#### Use
```bash
use {db-name} -- tell your app to "use" a named DB for subsequent commands
```

Example:
```bash
use testDB;
Database changed (0.0002111 sec)
```

This command will open the identified file so that it can be used.

#### Show
```bash
SHOW DATABASES -- render a view of all the DB's in your storage folder
```

Example:
```bash
shoW databaseS;
+---------------+
| Database      |
+---------------+
| my_database   |
| testdb_10012A |
| testdb_1196F  |
| testdb_12292A |
| testdb_12351A |
| testdb_12462A |
| testdb_12769F |
| testdb_13437A |
| testdb_15165A |
| testdb_17372F |
| testdb_17767F |
| testdb_18133F |
| testdb_18352F |
| testdb_18900F |
| testdb_19014F |
| testdb_19024F |
| testdb_21290A |
| testdb_22257F |
| testdb_22522F |
| testdb_22567F |
| testdb_22783F |
| testdb_22865F |
| testdb_23279F |
| testdb_25415F |
| testdb_28259F |
| testdb_32723A |
| testdb_3586B  |
| testdb_3642B  |
| testdb_3877B  |
+---------------+
29 rows in set (0.0001188 sec)
```

#### Dump
```bash
DUMP DATABASE {db-name}  -- show a view of blocks in a storage file (likely empty at this point)
```

Example:
```bash
> dump database testdb_14032B;
+---------------+-------------+----------------+
| Type          | Position    | Extra          |
+---------------+-------------+----------------+
| Meta          | 0           | 00000000       |
| Schema        | 1           | Users          |
| Data          | 2           | 82025960       |
| Data          | 3           | 82025960       |
| Data          | 4           | 82025960       |
| Data          | 5           | 82025960       |
| Data          | 6           | 82025960       |
| Data          | 7           | 82025960       |
| Data          | 8           | 82025960       |
+---------------+-------------+----------------+
9 rows in set (0.00687606 sec)
```
Type :
- Meta : Index Block with indices pointing to all the other blocks
- Schema : Block containing attribute information for a table
- Data : Block containing the data for a specific table

Position : position of where the block is located in the file, with each position taking up 1024 bytes.

Extra : Name of the block with 00000000 being null and all other number-based identifiers being hashed for encryption purposes.

### Table Commands
#### Create
To create a table, you must follow this format.
```bash
create table {table-name} (attribute_1, attribute_2, ...., attribute_n)
```

An attribute is a field, and must have at least two values:
- identifier
- type

All others are optional and can be listed below:
- auto_increment: adds an incrementing number for each row
- primary_key: denotes the attribute as the primary key for the table
- null: marks an attribute as null if no value provided when inserting data
- not_null: marks an attribute as not_null if no value provided when inserting data 
- unique: marks the attribute as a unique, forcing all values to be unique.


Example: 
```bash
create table tasks (
  id INT AUTO_INCREMENT PRIMARY KEY,
  title VARCHAR(100) NOT NULL,
  price FLOAT DEFAULT 0.0,
  due_date TIMESTAMP, //2020-04-15 10:11:12
  status BOOLEAN DEFAULT FALSE,
)
Query OK, 1 rows affected (0.0004134 sec)
```

#### Drop
```bash
drop table {table-name}
```

Example:
```bash
drop table Users;
Query OK, 0 rows affected (0.000175 sec)
```

#### Insert
```bash
insert into {table-name} (attribute_1, attribute_2, ..., attribute_n) values (value1, value2, ..., value_n);
```

Example:
```bash
INSERT INTO Users (first_name, last_name, age, zip) VALUES ("Terry",     "Pratchett", 70,  92124), ("Ian",       "Tregellis", 48,  92123), ("Jody",      "Taylor",    50,  92120), ("Stephen",   "King",      74,  92125), ("Ted",       "Chiang",    56,  92120);
Query Ok, 5 rows affected (0.0010756 sec)
```

#### Select

#### Update

#### Describe
```bash
describe {table-name};
```

Example:
```bash
> describe tasks;
+-----------+--------------+------+-----+---------+-----------------------------+
| Field     | Type         | Null | Key | Default | Extra                       |
+-----------+--------------+------+-----+---------+-----------------------------+
| id        | integer      | NO   | YES | NULL    | auto_increment primary key  |
| title     | varchar(100) | NO   |     | NULL    |                             |
| price     | float        | YES  |     | 0.0     |                             |
| due_date  | date         | YES  |     | NULL    |                             |
| status    | boolean      | YES  |     | FALSE   |                             |
+-----------+--------------+------+-----+---------+-----------------------------+
5 rows in set (0.000043 sec.)
```

#### Show
```bash
show tables;
```

Example:
```bash
show tables;
+-----------+
| Tables    |
+-----------+
| Books     |
| Users     |
+-----------+
2 rows in set (4.21e-05 sec)
```

### Misc Commands
#### About
To see the developer who coded this MySQL Mock Database, type about;
```bash
about;
```

Example:
```bash
about;
Authors: Kevin Shin (0.000199 sec)
```

#### Version
To see what version the database is currently on, type version;
```bash
verison;
```

Example:
```bash
version;
Version: 0.1 (0.000158 sec)
```

#### Help
To get the list of currently supported commands, you can type help;
```bash
help;
```

Example:
```bash
 help;
create database {name} : make a new database in storage folder
drop database {name}   : delete a known database from storage folder
show databases         : list databases in storage folder
use database {name}    : load a known database for use
about                  : show members
help                   : show list of commands
quit                   : stop app
version                : show app version (0.000279 sec)
```
#### Quit
To quit the database, you can type quit;
```bash
quit;
``` 