## 在 AKS 上部署 WordPress
https://docs.microsoft.com/zh-tw/azure/mysql/flexible-server/tutorial-deploy-wordpress-on-aks

* 連線至叢集
```
az aks get-credentials --resource-group CoreServiceRG-Test --name MyCluster

```
* 驗證
```
kubectl get nodes
```

* 先建一個 az mysql flexible-server 

```
az mysql flexible-server create --public-access all

```

* 下載最新的 WordPress 
``` 
 https://wordpress.org/download/
```
 
* 建立專案目錄
```
my-wordpress-app

```
* 建立下列資料夾結構
```
└───my-wordpress-app
    └───public
        ├───wp-admin
        │   ├───css
      	. . . . . . .
        ├───wp-content
        │   ├───plugins
        . . . . . . .
        └───wp-includes
        . . . . . . .
        ├───wp-config-sample.php
        ├───index.php
        . . . . . . .
    └─── Dockerfile
```
** 行重新命名 wp-config-sample.php 為 wp-config.php 

** 並將行從 開頭 // ** MySQL settings - You can get this info from your web host ** // 取代為 ，直到行 define( 'DB_COLLATE', '' ); 以下列程式碼片段取代。 下列程式碼是從 Kubernetes 資訊清單檔案讀取資料庫主機 、使用者名稱和密碼。

```
//Using environment variables for DB connection information

// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */

$connectstr_dbhost = getenv('DATABASE_HOST');
$connectstr_dbusername = getenv('DATABASE_USERNAME');
$connectstr_dbpassword = getenv('DATABASE_PASSWORD');
$connectst_dbname = getenv('DATABASE_NAME');

/** MySQL database name */
define('DB_NAME', $connectst_dbname);

/** MySQL database username */
define('DB_USER', $connectstr_dbusername);

/** MySQL database password */
define('DB_PASSWORD',$connectstr_dbpassword);

/** MySQL hostname */
define('DB_HOST', $connectstr_dbhost);

/** Database Charset to use in creating database tables. */
define('DB_CHARSET', 'utf8');

/** The Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/** SSL*/
define('MYSQL_CLIENT_FLAGS', MYSQLI_CLIENT_SSL);
```


* 建立 Dockerfile
```
FROM php:7.2-apache
COPY public/ /var/www/html/
RUN docker-php-ext-install mysqli
RUN docker-php-ext-enable mysqli
```
* 建置您的 Docker 映像
```
docker build --tag myblog:latest .
```
* 將您的映像部署至 Docker Hub 或 Azure Container Registry。
如果您使用 Azure Container Regdistry (ACR)，請執行 az aks update 命令，以連結 ACR 帳戶與 AKS 叢集。
```
az aks update -n myAKSCluster -g wordpress-project --attach-acr <your-acr-name>
az aks update -n myCluster -g CoreServiceRG-Test --attach-acr myregistryRD
```
