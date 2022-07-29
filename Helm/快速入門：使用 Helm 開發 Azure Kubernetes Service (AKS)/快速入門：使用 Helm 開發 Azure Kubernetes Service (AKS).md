https://docs.microsoft.com/zh-tw/azure/aks/quickstart-helm?tabs=azure-cli

# 快速入門：使用 Helm 開發 Azure Kubernetes Service (AKS)

## 下載範例應用程式

本快速入門會使用 Azure 投票應用程式。 從GitHub複製應用程式，然後流覽至 azure-vote 目錄。
```
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
cd azure-voting-app-redis/azure-vote/
```
## 建置範例應用程式並將其推送至 ACR

使用上述 Dockerfile，執行 az acr build 命令來建置映射，並將映射推送至登錄。 
```
az acr build --image azure-vote-front:v1 --registry MyHelmACR --file Dockerfile .

az acr build --image azure-vote-front:v1 --registry myclusterregistry --file Dockerfile .
```

## 建立您的 Helm 圖表
使用 helm create 命令產生 Helm 圖表。
```
helm create azure-vote-front
```

* 更新 azure-vote-front/Chart.yaml 以從圖表存放庫新增 redis 圖表的 https://charts.bitnami.com/bitnami 相依性，並更新 appVersion 為 v1 。 
例如：
```
apiVersion: v2
name: azure-vote-front
description: A Helm chart for Kubernetes

dependencies:
  - name: redis
    version: 14.7.1
    repository: https://charts.bitnami.com/bitnami

...
# This is the version number of the application being deployed. This version number should be
# incremented each time you make changes to the application.
appVersion: v1
```
* 使用 helm dependency update 更新 helm 圖表相依性：
```
helm dependency update azure-vote-front
```
