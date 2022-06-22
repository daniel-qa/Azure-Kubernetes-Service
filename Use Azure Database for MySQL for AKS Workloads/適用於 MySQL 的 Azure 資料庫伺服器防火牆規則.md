
# 適用於 MySQL 的 Azure 資料庫伺服器防火牆規則
https://docs.microsoft.com/zh-tw/azure/mysql/single-server/concepts-firewall-rules

* 連接資料庫的指令 Sample
```
mysql -hmydbrd.mysql.database.azure.com -udbadmin@mydbrd -p

```

```
防火牆會防止對您資料庫伺服器的所有存取，直到您指定哪些電腦擁有權限。 此防火牆會根據每一個要求的來源 IP 位址來授與伺服器存取權。
從伺服器資源的左窗格，移至 [連線安全性]。 
選取 [新增目前的用戶端 IP 位址]，然後選取 [儲存]。

```


![](https://docs.microsoft.com/zh-tw/azure/mysql/single-server/media/quickstart-create-mysql-server-database-using-azure-portal/add-current-ip-firewall.png)


* 防火牆概觀

![](https://docs.microsoft.com/zh-tw/azure/mysql/single-server/media/concepts-firewall-rules/1-firewall-concept.png)


* 允許外部使用者
```
允許 Azure 連線，可以允許 Azure 服務去存取 MySQL db，但無法允許外部使用者連線。
```
