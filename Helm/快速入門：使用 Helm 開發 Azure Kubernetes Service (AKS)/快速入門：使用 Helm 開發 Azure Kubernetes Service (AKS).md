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
