# DB Spec

Database Schema Design and Modeling Tool

Design Database Schema Without Writing SQL

## 1. Introduction

This project provides a mapping between specific symbols and corresponding data definition language (DDL) concepts. This mapping is intended to be used for parsing and converting data in various scenarios, such as databases, data analysis, and programming language parsing.

**Features:**

1. [Schema](#schema)
2. [Table](#table)
3. [Column](#column)
4. [Types](#types)
   - [Number](#number)
   - [String](#string)
   - [Datetime](#datetime)
5. [Default](#default)
6. [Auto Increment](#plus)
7. [Primary Key](#primary-key)
8. [Plus](#plus)
9. [Comment](#comment)
10. [Template](#template)

## 2. Specification

The mapping is defined as follows:

```asm
$    ; schema
#    ; table
%    ; template
...  ; slot
+    ; AUTO_INCREMENT, DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
!    ; primary key
++   ; AUTO_INCREMENT primary key
=    ; default
```

## 3. Hello World

#### user.dbs

```c
# user  // TABLE OF USER  -- define a `user` table with comment 'TABLE OF USER'

id       n++   // id of user

name           // name of user
password s100  // password of user
avatar   S     // avatar of user

balance m      // balance of user
version N =0   // version of record
status  1 =0   // status of record

delete_at t    // delete time of record
create_at t=   // create time of record
update_at t+   // update time of record
```

#### user.sql

```sql
CREATE TABLE `user` (
  `id`        int AUTO_INCREMENT PRIMARY KEY COMMENT 'id of user',

  `name`      varchar(255) COMMENT 'name of user',
  `password`  varchar(100) COMMENT 'password of user',
  `avatar`    text COMMENT 'avatar of user',

  `balance`   decimal(16, 2) COMMENT 'balance of user',
  `version`   bigint DEFAULT 0 COMMENT 'version of record',
  `status`    int(1) DEFAULT 0 COMMENT 'status of record',

  `delete_at` datetime COMMENT 'delete time of record',
  `create_at` datetime DEFAULT CURRENT_TIMESTAMP COMMENT 'create time of record',
  `update_at` datetime DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'update time of record',

  COMMENT = 'TABLE OF USER'
)
```


## 4. Schema <a name="schema"></a>

Mark | MySQL
-|-
`$` | schema name

#### schema.zz 

```asm
(?<=\n|^)
(?:\$\s*)
(?:\w+)                    ; schema name
(?:\s*)
(?:--\s*(?:.*)(?=\n|$))?   ; sql comment
(?:\n)
```

#### demo.dbs

```c
$ demo
```

#### demo.sql

```sql
create DATABASE `demo`
```

## 5. Table <a name="table"></a>

Mark | MySQL
-|-
`#` | table name

#### table.zz

```asm
(?<=\n|^)
(?:\#)
\s*
(?:\w+)                    ; table name
\s*
(?://\s*(?:.*?))?          ; table comment
(?:--\s*(?:.*)(?=\n|$))?   ; sql comment
(?:\n)
```

#### user.dbs

```
# user
```

#### user.sql

```sql
CREATE TABLE `user` (
)
```

## 6. Column <a name="column"></a>

#### column.zz

```asm
(?<=\n)
(?:\w+)                              ; name
\s*
(?:[nNmMtS]|\d+(?:,\d+)?|s(?:\d+)?)  ; types
\s*
(?:=\s*\w*)?                         ; default
\s*
(?:[+|++])?                          ; auto increment, auto increment primary key
\s*
(?:!)?                               ; primary key
\s*
(?://.*?)                            ; table comment
(?:--.*)                             ; sql comment
(?:;.*)                              ; spec comment
\n
```

## 7. Types <a name="types"></a>

Referenced the [Type Spec](https://github.com/maronghai/typespec) project.

### 7.1. Number <a name="number"></a>

Mark | Type
-|-
`n` | int
`N` | bigint
`m` | decimal(16, 2)
`M` | decimal(20, 6)
`\d+` | int(\d+)
`\d*\,\d+` | decimal(\d+, \d+)

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

### 7.2. String <a name="string"></a>

Mark | Type
-|-
| | varchar
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

### 7.3. Datetime <a name="datetime"></a>

Mark | Type 
-|-
`t` | datetime

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

## 8. Plus

1. Auto Increment
   - Auto Increment and Primary Key 
3. Default ... On Update  <a name="plus"></a>

Mark | MySQL
-|-
`n` `+`, `N` `+`, `\d+` `+` | AUTO_INCREMENT
`++` | AUTO_INCREMENT PRIMARY KEY
`t` `+` | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP

user.dbs

```
# user
id n ++
update_at t+
```

user.sql

```sql
CREATE TABLE `user` (
  `id` int AUTO_INCREMENT PRIMARY KEY
  `update_at` datetime DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
)
```

## 9.  Key  <a name="primary-key"></a>

Mark | MySQL
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

## Default <a name="default"></a>

Mark | MySQL
-|-
`=` | DEFAULT
`t` `=` | DEFAULT CURRENT_TIMESTAMP

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

## 10. Comment <a name="comment"></a>

Mark | MySQL
-|-
`//` | table or column `COMMENT`
`--` | sql comment

user.dbs

```
# user  // TABLE OF USER  -- define a `user` table 
status 1 =1 // [0,1]      -- define a `status` column, type is int(1), comment is '[0,1]'
```

user.sql

```sql
CREATE TABLE `user` ( -- define a `user` table 
  `status` int(1) DEFAULT 1 COMMENT '[0,1]', -- define a `status` column, type is int(1), comment is '[0,1]'
  COMMENT = 'TABLE OF USER'
)
```

## 11. Template <a name="template"></a>

Mark | MySQL
-|-
`%`  | template name. default name is empty.
`...` | slot. default slot is at the end of the template.

#### Default Template

template.dbs

```
%

id n++
...           -- Here is a slot
version   N
status    1

delete_at t
create_at t =
update_at t +
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

### 11.2 Named Template

all.spec

```
%1

id n++

#1 user  -- define a `user` table using template named `1`

name
```

all.sql

```sql
CREATE TABLE `user` (
  `id`   int AUTO_INCREMENT PRIMARY KEY,
  `name` varchar(255)
)
```


## 12. Ecosystem

1. [Type Spec](https://github.com/maronghai/typespec)
2. [DB Create](https://github.com/maronghai/dbcreate)
3. [ZZ](https://github.com/maronghai/zz)

## 13. License

[MIT](https://opensource.org/licenses/MIT)

Copyright (c) 2023-present, Ronghai Ma
