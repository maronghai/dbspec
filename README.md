# DB SPEC

Database Schema Design and Modeling Tool

Design Database Schema Without Writing SQL

## hello world

user.dbs

```
# user // TABLE OF USER  ；define a `user` table with comment 'TABLE OF USER'

id n ++ !

name
password s100
avatar   S

balance m
version N =0
status  1 =0 // [0,1]

delete_at t
create_at t=
update_at t+
```

user.sql

```sql
CREATE TABLE `user` (
  `id`        int AUTO_INCREMENT PRIMARY KEY,

  `name`      varchar(255),
  `password`  varchar(100),
  `avatar`    text,

  `balance`   decimal(16, 2),
  `version`   bigint DEFAULT 0,
  `status`    int(1) DEFAULT 0 COMMENT '[0,1]',

  `delete_at` datetime,
  `create_at` datetime DEFAULT CURRENT_TIMESTAMP,
  `update_at` datetime DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,

  COMMENT = 'TABLE OF USER'
)
```

## Schema

mark | MySQL
-|-
`$` | schema name

demo.dbs

```
$ demo  ; /(?:^|\n)\$\s*\w+/
```

demo.sql

```sql
create DATABASE `demo`
```

## Table

mark | MySQL
-|-
`#` | table name

user.dbs

```
# user
```

user.sql

```sql
CREATE TABLE `user` (
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

id      n
version N
status  1

balance  m
balance6 M
balancex 16,6
```

user.sql

```sql
CREATE TABLE `user` (
  `id`       int,
  `version`  bigint,
  `status`   int(1),

  `balance`  decimal(16, 2),
  `balance6` decimal(20, 6),
  `balancex` decimal(16, 6)
)
```

## STRING

mark | MySQL
-|-
| | varchar(255)
`s\d+` | varchar(\d+)
`S` | text

user.dbs

```
# user

name
password s100
avatar S

```

user.sql

```sql
CREATE TABLE `user` (
  `name`     varchar(255),
  `password` varchar(100),
  `avatar`   text
)
```

## DATETIME

mark | MySQL 
-|-
`t` | datetime
`t=` | datetime DEFAULT CURRENT_TIMESTAMP
`t+` | datetime DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP

user.dbs

```
# user

delete_at t
create_at t=
update_at t+

```

user.sql

```sql
CREATE TABLE `user` (
  `delete_at` datetime,
  `create_at` datetime DEFAULT CURRENT_TIMESTAMP,
  `update_at` datetime DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
)
```

## AUTO INCREMENT

mark | MySQL
-|-
`++` | AUTO_INCREMENT

user.dbs

```
# user
id n ++
```

user.sql

```sql
CREATE TABLE `user` (
  `id` int AUTO_INCREMENT
)
```

## PRIMARY KEY

mark | MySQL
-|-
`!` | PRIMARY KEY

user.dbs

```
# user
id n !
```

user.sql

```sql
CREATE TABLE `user` (
  `id` int PRIMARY KEY
)
```

## DEFAULT

mark | MySQL
-|-
`=` | DEFAULT

user.dbs

```
# user
status 1 =1
```

user.sql

```sql
CREATE TABLE `user` (
  `status` int(1) DEFAULT 1
)
```

## COMMENT

mark | MySQL
-|-
`//`, `--` | comment

user.dbs

```
# user -- TABLE OF USER
status 1 =1 // [0,1]
```

user.sql

```sql
CREATE TABLE `user` (
  `status` int(1) DEFAULT 1 COMMENT '[0,1]',
  COMMENT = 'TABLE OF USER'
)
```

## TEMPLATE

mark | MySQL
-|-
`#?`  | template name. default name is empty.
`...` | slot. default slot is at the end of the template.

template.dbs

```
#?

id n ++ !
...           ; Here is a slot
version   N
status    1

delete_at t
create_at t=
update_at t+  ;
```

user.dbs

```
# user // TABLE OF USER

name
password s100
avatar   S

balance  m
```

user.sql

```sql
CREATE TABLE `user` (
  `id`        int AUTO_INCREMENT PRIMARY KEY,

  `name`      varchar(255),
  `password`  varchar(100),
  `avatar`    text,

  `balance`   decimal(16, 2),
  `version`   bigint DEFAULT 0,
  `status`    int(1) DEFAULT 0 COMMENT '[0,1]',

  `delete_at` datetime,
  `create_at` datetime DEFAULT CURRENT_TIMESTAMP,
  `update_at` datetime DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,

  COMMENT = 'TABLE OF USER'
)
```

### Named Template

all.spec

```
#? 1

id n ++ !

#1 user  ; define a `user` table using template named `1`

name
```

all.sql

```sql
CREATE TABLE `user` (
  `id`   int AUTO_INCREMENT PRIMARY KEY,
  `name` varchar(255)
)
```


## Ecosystem

1. [DB CREATE](https://github.com/maronghai/dbcreate)

## License

[MIT](https://opensource.org/licenses/MIT)

Copyright (c) 2023-present, Ronghai Ma
