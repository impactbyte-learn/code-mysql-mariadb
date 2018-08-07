# Code MySQL/MariaDB

## Installation

### macOS

```sh
brew install mariadb mycli
brew services start mariadb
```

## Usage

### Login with root

```sh
mycli -uroot
```

```sql
CREATE USER 'haidar'@'localhost' IDENTIFIED BY 'passwordtext';
GRANT ALL PRIVILEGES ON *.* to 'haidar'@'localhost' WITH GRANT OPTION;
exit;
```

```sh
mycli -uhaidar -ppasswordtext
```

```sql
SHOW DATABASES;
CREATE DATABASE glintsacademy;
SHOW DATABASES;
```
