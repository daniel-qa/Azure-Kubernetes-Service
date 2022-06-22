https://docs.microsoft.com/zh-tw/azure/mysql/single-server/how-to-create-users

* 建立資料庫
``` 
CREATE DATABASE testdb;
```

* 建立非管理員使用者
既然已建立資料庫，您就可以使用 CREATE USER MySQL 陳述式，建立非管理員使用者。

```
CREATE USER 'db_user'@'%' IDENTIFIED BY 'StrongPassword!';

GRANT ALL PRIVILEGES ON testdb . * TO 'db_user'@'%';

GRANT ALL PRIVILEGES ON *.* TO 'daniel'@'%';

FLUSH PRIVILEGES;
```

* 驗證使用者權限

```
USE testdb;

SHOW GRANTS FOR 'db_user'@'%';
```
* 使用新的使用者連線至資料庫

```
單一伺服器	mysql --host mydemoserver.mysql.database.azure.com --database testdb --user db_user@mydemoserver -p
彈性伺服器	mysql --host mydemoserver.mysql.database.azure.com --database testdb --user db_user -p
```
* 限制使用者的權限
```
CREATE USER 'new_master_user'@'%' IDENTIFIED BY 'StrongPassword!';

GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, RELOAD, PROCESS, REFERENCES, INDEX, ALTER, SHOW DATABASES, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, REPLICATION SLAVE, REPLICATION CLIENT, CREATE VIEW, SHOW VIEW, CREATE ROUTINE, ALTER ROUTINE, CREATE USER, EVENT, TRIGGER ON *.* TO 'new_master_user'@'%' WITH GRANT OPTION;

FLUSH PRIVILEGES;
```
```
CREATE USER 'daniel'@'%' IDENTIFIED BY 'StrongPassword!';

GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, RELOAD, PROCESS, REFERENCES, INDEX, ALTER, SHOW DATABASES, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, REPLICATION SLAVE, REPLICATION CLIENT, CREATE VIEW, SHOW VIEW, CREATE ROUTINE, ALTER ROUTINE, CREATE USER, EVENT, TRIGGER ON *.* TO 'daniel'@'%' WITH GRANT OPTION;

FLUSH PRIVILEGES;
```


