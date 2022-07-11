https://docs.microsoft.com/zh-cn/azure/aks/cluster-container-registry-integration?tabs=azure-cli

# 使用 Azure 容器注册表从 Azure Kubernetes 服务进行身份验证




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
