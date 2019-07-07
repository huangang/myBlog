title: >-
  解决 PostgreSQL Uniqueness violation. duplicate key value violates unique
  constraint
date: 2019-07-07 19:51:34
tags: [PostgreSQL, GraphQL, hasura]
---
## 起因
最近做PostgreSQL的数据结构同步和迁移完之后发生了     
`Uniqueness violation. duplicate key value violates unique constraint`     
的错误

## 解决方法
执行下面sql语句      
``` sql
SELECT setval(pg_get_serial_sequence('table_name', 'id'), 
coalesce(max(id),1), false) FROM table_name;
``` 
