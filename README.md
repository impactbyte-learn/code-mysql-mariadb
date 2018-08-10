# Code MySQL/MariaDB

[![Greenkeeper badge](https://badges.greenkeeper.io/impactbyte-learn/code-mysql-mariadb.svg)](https://greenkeeper.io/)

Example code on how to use MySQL/MariaDB, in order to create a users & todos database/dataset.

## Data Schema

### Users

| Field      | Type            | Null | Key   |
| ---------- | --------------- | ---- | ----- |
| `id`       | `int(11)`       | `NO` | `PRI` |
| `email`    | `varchar(100)`  | `NO` |       |
| `password` | `varchar(100)`  | `NO` |       |
| `name`     | `varchar(100)`  | `NO` |       |
| `username` | `varchar(50)`   | `NO` |       |
| `gender`   | `enum('M','F')` |      |       |

### Todos

| Field     | Type           | Null | Key   |
| --------- | -------------- | ---- | ----- |
| `id`      | `int(11)`      | `NO` | `PRI` |
| `text`    | `varchar(140)` | `NO` |       |
| `user_id` | `int(11)`      | `NO` | `MUL` |

---

## Installation

### macOS

```sh
brew install mariadb mycli
brew services start mariadb
```

### Ubuntu

- [Install MariaDB 10.3 on Ubuntu 18.04 and CentOS 7 - Computingforgeeks](https://computingforgeeks.com/install-mariadb-10-on-ubuntu-18-04-and-centos-7)
- [How To Install MySQL on Ubuntu 18.04 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-18-04)

---

## Usage

### Login with root

```sh
mycli -uroot
```

### Create new user

```sql
CREATE USER 'haidar'@'localhost' IDENTIFIED BY 'passwordtext';
GRANT ALL PRIVILEGES ON *.* to 'haidar'@'localhost' WITH GRANT OPTION;
exit;
```

### Login with new user

```sh
mycli -uhaidar -ppasswordtext
```

### Create and use initial database

```sql
SHOW DATABASES;
CREATE DATABASE glintsacademy;
SHOW DATABASES;
USE glintsacademy;
```

### Create tables

```sql
CREATE TABLE users (
   id INT NOT NULL AUTO_INCREMENT,
   email VARCHAR(100) NOT NULL,
   password VARCHAR(100) NOT NULL,
   name VARCHAR(100) NOT NULL,
   username VARCHAR(50) NOT NULL,
   gender ENUM('M','F'),
   PRIMARY KEY(id)
);

CREATE TABLE todos (
   id INT NOT NULL AUTO_INCREMENT,
   text VARCHAR(140) NOT NULL,
   user_id INT NOT NULL,
   PRIMARY KEY(id),
   FOREIGN KEY(user_id) REFERENCES users(id)
);
```

### Show tables and description

**Command:**

```sql
SHOW TABLES;
DESC users;
DESC todos;
```

**Result:**

```txt
+----------+--------------+------+-----+---------+----------------+
| Field    | Type         | Null | Key | Default | Extra          |
+----------+--------------+------+-----+---------+----------------+
| id       | int(11)      | NO   | PRI | <null>  | auto_increment |
| name     | varchar(100) | NO   |     | <null>  |                |
| email    | varchar(100) | NO   |     | <null>  |                |
| password | varchar(100) | NO   |     | <null>  |                |
+----------+--------------+------+-----+---------+----------------+
```

```txt
+---------+--------------+------+-----+---------+----------------+
| Field   | Type         | Null | Key | Default | Extra          |
+---------+--------------+------+-----+---------+----------------+
| id      | int(11)      | NO   | PRI | <null>  | auto_increment |
| text    | varchar(140) | NO   |     | <null>  |                |
| user_id | int(11)      | NO   | MUL | <null>  |                |
+---------+--------------+------+-----+---------+----------------+
```

### Select all data from tables

```sql
SELECT * FROM users;
SELECT * FROM todos;
```

### Alter table datatype and add constraint

```sql
/* DO NOT USE THIS IN PRODUCTION */
SET FOREIGN_KEY_CHECKS = 0;
ALTER TABLE users CHANGE id id INT AUTO_INCREMENT;
SET FOREIGN_KEY_CHECKS = 1;
```

```sql
ALTER TABLE users
ADD CONSTRAINT constraint_unique UNIQUE(id, email);
```

### Insert data to tables

**Command:**

```sql
INSERT INTO users (name, email, password)
VALUES
    ('Haidar', 'haidar@impactbyte.com', 'halodunia'),
    ('Jakarta', 'jakarta@impactbyte.com', 'halojakarta'),
    ('Batam', 'batam@impactbyte.com', 'halobatam');
```

```sql
INSERT INTO todos (text, user_id)
VALUES
    ('Learn data design', 1),
    ('Install DBMS', 1),
    ('Learn SQL syntax', 1),
    ('Establish company', 2),
    ('Exchange partnership', 2);
```

**Result:**

```txt
Query OK, ? rows affected
Time: 0.001s
```

### Select all data from tables

**Command:**

```sql
SELECT * FROM users, todos;
```

**Result:**

```txt
+----+---------+------------------------+-------------+
| id | name    | email                  | password    |
+----+---------+------------------------+-------------+
| 1  | Haidar  | haidar@impactbyte.com  | halodunia   |
| 2  | Jakarta | jakarta@impactbyte.com | halojakarta |
| 3  | Batam   | batam@impactbyte.com   | halobatam   |
+----+---------+------------------------+-------------+
```

```txt
+----+----------------------+---------+
| id | text                 | user_id |
+----+----------------------+---------+
| 1  | Learn data design    | 1       |
| 2  | Install DBMS         | 1       |
| 3  | Learn SQL syntax     | 1       |
| 4  | Establish company    | 2       |
| 5  | Exchange partnership | 2       |
```

### Delete rows in tables

```sh
DELETE FROM users;
DELETE FROM todos;
```
