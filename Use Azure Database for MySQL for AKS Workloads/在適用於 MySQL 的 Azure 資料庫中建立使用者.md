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

FLUSH PRIVILEGES;
```

* 驗證使用者權限

```
USE testdb;

SHOW GRANTS FOR 'db_user'@'%';
```
