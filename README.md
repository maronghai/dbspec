# MarkDB-SPEC

Database Schema Design and Modeling Tool

Design Database Schema Without Writing SQL

## hello world

```
# user

id n ++

name
password s100
avatar s

balance m
version N ^ 0
status 1 ^0

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
  status int(1) DEFAULT 0,

  create_at datetime DEFAULT CURRENT_TIMESTAMP,
  update_at datetime DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
)
```

## TABLE

mark | type
-|-
`#` | table name


## NUMBER

mark | type
-|-
n | int
N | bigint
\d+ | int(\d+)
\d*\.\d+ | decimal(\d+, \d+)
m | decimal(16, 2)
M | decimal(20, 6)

## STRING

mark | type
-|-
| | varchar(255)
s\d+ | varchar(\d+)
S | text

## DATETIME

mark | type 
-|-
t | datetime
t1 | datetime DEFAULT CURRENT_TIMESTAMP
t2 | datetime DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP

## PLUS PLUS

mark | type
-|-
++ | AUTO_INCREMENT PRIMARY KEY

## DEFAULT

mark | type
-|-
^ | DEFAULT

## database engines

1. [x] MySQL
2. [ ] MSSql
3. [ ] PostgreSQL
4. [ ] Oracle®
5. [ ] SQLite
