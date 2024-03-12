# DB SPEC

Database Schema Design and Modeling Tool

Design Database Schema Without Writing SQL

## hello world

```
# user // TABLE OF USER

id n ++

name
password s100
avatar s

balance m
version N ^ 0
status 1 ^0 // [0,1]

delete_at t
create_at t1
update_at t2
```

```mysql
CREATE TABLE user (
  id int AUTO_INCREMENT PRIMARY KEY,

  name varchar(255),
  password varchar(100),
  avatar text,

  balance decimal(16, 2),
  version bigint DEFAULT 0,
  status int(1) DEFAULT 0 COMMENT '[0,1]',

  delete_at datetime
  create_at datetime DEFAULT CURRENT_TIMESTAMP,
  update_at datetime DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,

  COMMENT = 'TABLE OF USER'
)
```

## TABLE

mark | MySQL
-|-
`#` | table name


## NUMBER

mark | MySQL
-|-
n | int
N | bigint
\d+ | int(\d+)
\d*\.\d+ | decimal(\d+, \d+)
m | decimal(16, 2)
M | decimal(20, 6)

## STRING

mark | MySQL
-|-
| | varchar(255)
s\d+ | varchar(\d+)
S | text

## DATETIME

mark | MySQL 
-|-
t | datetime
t1 | datetime DEFAULT CURRENT_TIMESTAMP
t2 | datetime DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP

## PLUS PLUS

mark | MySQL
-|-
++ | AUTO_INCREMENT PRIMARY KEY

## DEFAULT

mark | MySQL
-|-
^ | DEFAULT

## COMMENT

mark | MySQL
-|-
`//` | comment

## database engines

1. [x] MySQL
2. [ ] MSSql
3. [ ] PostgreSQL
4. [ ] Oracle®
5. [ ] SQLite


## License

[MIT](https://opensource.org/licenses/MIT)

Copyright (c) 2023-present, Ronghai Ma
