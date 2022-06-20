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
