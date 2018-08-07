# Code MySQL/MariaDB

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

### Create initial database

```sql
SHOW DATABASES;
CREATE DATABASE glintsacademy;
SHOW DATABASES;
```
