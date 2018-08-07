# Code MySQL/MariaDB

## Data Schema

### Users

### Todos

### Addresses

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
   id INT NOT NULL,
   name VARCHAR(100) NOT NULL,
   email VARCHAR(100) NOT NULL,
   password VARCHAR(100) NOT NULL,
   PRIMARY KEY(id)
);

CREATE TABLE todos (
   id INT NOT NULL,
   text VARCHAR(140) NOT NULL,
   user_id INT NOT NULL,
   PRIMARY KEY(id),
   FOREIGN KEY(user_id) REFERENCES users(id)
);
```

### Show tables

```sql
SHOW TABLES;
```

### Select all data from tables

```sql
SELECT * FROM users;
SELECT * FROM todos;
```

### Insert data to tables
