# DB SPEC

Database Schema Design and Modeling Tool

Design Database Schema Without Writing SQL

## hello world

```
# user // TABLE OF USER

id n ! ++

name
password s100
avatar s

balance m
version N ^ 0
status 1 ^0 // [0,1]

delete_at t
create_at t1
update_at t+
```

```sql
CREATE TABLE user (
  id int AUTO_INCREMENT PRIMARY KEY,

  name     varchar(255),
  password varchar(100),
  avatar   text,

  balance decimal(16, 2),
  version bigint DEFAULT 0,
  status  int(1) DEFAULT 0 COMMENT '[0,1]',

  delete_at datetime,
  create_at datetime DEFAULT CURRENT_TIMESTAMP,
  update_at datetime DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,

  COMMENT = 'TABLE OF USER'
)
```

## TABLE

mark | MySQL
-|-
`#` | table name

user.dbs

```
# user
```

user.sql

```sql
CREATE TABLE user (
)
```

## NUMBER

mark | MySQL
-|-
`n` | int
`N` | bigint
`\d+` | int(\d+)
`\d*\,\d+` | decimal(\d+, \d+)
`m` | decimal(16, 2)
`M` | decimal(20, 6)

user.dbs

```
# user

id n
version N
status 1

balance m
balance6 M
balancex 16,6
```

user.sql

```sql
CREATE TABLE user (
  id      int,
  version bigint,
  status  int(1),

  balance  decimal(16, 2),
  balance6 decimal(20, 6),
  balancex decimal(16, 6)
)
```

## STRING

mark | MySQL
-|-
| | varchar(255)
`s\d+` | varchar(\d+)
`S` | text

## DATETIME

mark | MySQL 
-|-
`t` | datetime
`t1` | datetime DEFAULT CURRENT_TIMESTAMP
`t+` | datetime DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP

## AUTO INCREMENT

mark | MySQL
-|-
`++` | AUTO_INCREMENT

## PRIMARY KEY

mark | MySQL
-|-
`!` | PRIMARY KEY

## DEFAULT

mark | MySQL
-|-
`^` | DEFAULT

## COMMENT

mark | MySQL
-|-
`//` | comment

## database engines

1. [x] MySQL
2. [ ] MSSQL
3. [ ] PostgreSQL
4. [ ] Oracle®
5. [ ] SQLite


## License

[MIT](https://opensource.org/licenses/MIT)

Copyright (c) 2023-present, Ronghai Ma
