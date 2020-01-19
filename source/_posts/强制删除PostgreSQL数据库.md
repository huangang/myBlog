title: 强制删除PostgreSQL数据库
date: 2020-01-19 11:05:21
tags: ['PostgreSQL']
---
1.链接数据库    
``` bash
psql -h localhost postgres postgres
# /Library/PostgreSQL/9.4/bin/psql -h localhost postgres postgres
```
<!-- more -->

2.强制断开连接到该数据库的所有客户端的连接
``` bash
UPDATE pg_database SET datallowconn = 'false' WHERE datname = 'mydb';

SELECT pg_terminate_backend(pid)
FROM pg_stat_activity
WHERE datname = 'mydb';
```

3.删除数据库
``` bash
DROP DATABASE mydb;
```
