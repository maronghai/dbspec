# markdb

Database Schema Design and Modeling Tool

Design Database Schema Without Writing SQL

## hello world

```
# user

id n ++
name s
password s

version n
create_at t
update_at t
```

```sql
CREATE TABLE (
  id int AUTO_INCREMENT PRIMARY KEY,
  name varchar(255),
  password varchar(255),

  version int,
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
