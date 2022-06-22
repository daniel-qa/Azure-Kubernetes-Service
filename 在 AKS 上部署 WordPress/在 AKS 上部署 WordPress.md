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
* 如果您使用 Azure Container Regdistry (ACR)，請執行 az aks update 命令，以連結 ACR 帳戶與 AKS 叢集。
```
az aks update -n myAKSCluster -g wordpress-project --attach-acr <your-acr-name>
az aks update -n myCluster -g CoreServiceRG-Test --attach-acr myregistryRD
```
* 上傳鏡像至 ACR  (要先 tag 完整 acr 路徑)
```
docker push myregistryrd.azurecr.io/wordpress-blog:latest
```
* P.S 要先 login acr ，才能 push
```
az acr Login --name myregistryrd.azurecr.io
```
* 查詢 
```
az acr repository list -n myregistryrd
```
## 建立 Kubernetes 資訊清單檔
* Kubernetes 資訊清單檔會定義所需的叢集狀態，例如要執行哪些容器映像。 建立名為 mywordpress.yaml 的資訊清單檔，然後將下列 YAML 定義複製進來。
```

[ 重要 ] 
1.將 [DOCKER-HUB-USER/ACR ACCOUNT]/[YOUR-IMAGE-NAME]:[TAG] 取代為實際的 WordPress Docker 映像名稱和標籤，
例如 docker-hub-user/myblog:latest。

2.使用 MySQL 彈性伺服器的 SERVERNAME、YOUR-DATABASE-USERNAME、YOUR-DATABASE-PASSWORD 更新以下 env 區段。
```
* 使用 kubectl apply 命令來部署應用程式並指定 YAML 資訊清單的名稱：

* 參考: mywordpress.yaml

* 將 WordPress 部署至 AKS 叢集
```
kubectl apply -f mywordpress.yaml
```
輸出
```
> deployment "wordpress-blog" created
> service "php-svc" created
```
* 測試應用程式
```
kubectl get service php-svc --watch
```
輸出
```
NAME       TYPE           CLUSTER-IP   EXTERNAL-IP   PORT(S)        AGE
php-svc    LoadBalancer   10.0.37.27   <pending>     80:30572/TCP   6s
```
* 當 EXTERNAL-IP 位址從 pending 變成實際的公用 IP 位址時，請使用 CTRL-C 停止 kubectl 監看式流程。 下列範例輸出會顯示已指派給服務的有效公用 IP 位址：
輸出
```
php-svc  LoadBalancer   10.0.37.27   52.179.23.131   80:30572/TCP   2m
```
* 瀏覽 WordPress
開啟網頁瀏覽器並瀏覽至服務的外部 IP 位址，以查看您的 WordPress 安裝頁面。 
<img src="https://docs.microsoft.com/zh-tw/azure/mysql/flexible-server/media/tutorial-deploy-wordpress-on-aks/wordpress-aks-installed-success.png">

* 清除資源

若要避免 Azure 費用，您應該清除不需要的資源。 若不再需要叢集，可使用 az group delete 命令來移除資源群組、容器服務和所有相關資源。
``` 
az group delete --name wordpress-project --yes --no-wait 
```

* 常用 Kubectl 指令
```
kubetl apply -f pod.yaml
kubectl create -f pod.yaml
kubectl get pod
kubectl describe pod web-app
kubectl delete pod web-app
```
