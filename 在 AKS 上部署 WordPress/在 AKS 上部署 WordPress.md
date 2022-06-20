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

* 建立專案目錄
```
my-wordpress-app

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
