https://docs.microsoft.com/zh-tw/azure/aks/ingress-basic?tabs=azure-cli

* 注意
```
以 Nginx 為基礎的 Kubernetes 有兩個開放原始碼輸入控制器：一個是由 Kubernetes 社群維護 (kubernetes/ingress-nginx) ，
另一個是由 NGINX， Inc. 維護， (nginxinc/kubernetes-ingress) 。

本文將使用 Kubernetes 社群輸入控制器。
https://github.com/kubernetes/ingress-nginx

```

*基本設定

若要建立基本 NGINX 輸入控制器而不自訂預設值，您將使用 Helm。

```
NAMESPACE=ingress-basic

helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update

helm install ingress-nginx ingress-nginx/ingress-nginx \
  --create-namespace \
  --namespace $NAMESPACE \
  --set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz
  ```
