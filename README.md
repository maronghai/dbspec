# MarkDB

Database Schema Design and Modeling Tool

Design Database Schema Without Writing SQL

## hello world

```
# user

id n ++

name
password s
avatar s1024

version N
status 1

create_at t
update_at t
```

```mysql
CREATE TABLE (
  id int AUTO_INCREMENT PRIMARY KEY,

  name varchar(255),
  password varchar(255),
  avatar varchar(1024),

  version bigint,
  status int(1),

  create_at datetime,
  update_at datetime
)
```

## database engines

1. MySQL
2. MSSql
3. PostgreSQL
4. Oracle®
5. SQLite
