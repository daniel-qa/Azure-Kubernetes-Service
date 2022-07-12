https://docs.microsoft.com/zh-cn/azure/aks/cluster-container-registry-integration?tabs=azure-cli

# 使用 Azure 容器注册表从 Azure Kubernetes 服务进行身份验证


## 为现有的 AKS 群集配置 ACR 集成
```
az aks update -n myAKSCluster -g myResourceGroup --attach-acr <acr-name>
az aks update -n MyCluster -g CoreServiceRG-Test --attach-acr myRegistryRD

* 确保你具有正确的 AKS 凭据
az aks get-credentials -g CoreServiceRG-Test -n MyCluster
```

* 使用 ACR 和 AKS 
 将映像导入 ACR
 通过运行以下命令，将映像从 Docker Hub 导入到 ACR：

```
az acr import  -n <acr-name> --source docker.io/library/nginx:latest --image nginx:v1

az acr import  -n myRegistryRD --source docker.io/library/nginx:latest --image nginx:v1

```


* 确保你具有正确的 AKS 凭据

```
az aks get-credentials -g CoreServiceRG-Test -n myRegistryRD
```

* 将示例映像从 ACR 部署到 AKS

acr-nginx.yaml 

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx0-deployment
  labels:
    app: nginx0-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx0
  template:
    metadata:
      labels:
        app: nginx0
    spec:
      containers:
      - name: nginx
        image: myregistryrd.azurecr.io/nginx:v1
        ports:
        - containerPort: 80

```
