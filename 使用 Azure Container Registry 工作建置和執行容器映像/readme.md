https://docs.microsoft.com/zh-tw/azure/container-registry/container-registry-quickstart-task-cli

建立容器登錄庫
使用 az acr create 命令建立容器登錄。 登錄名稱在 Azure 內必須是唯一的，且包含 5-50 個英數字元。 下列範例將使用 myContainerRegistry008。 請將此更新為唯一的值。

試試看
az acr create --resource-group myResourceGroup \
  --name myContainerRegistry008 --sku Basic

p.s 注意，Registry 的名稱必須是唯一，不能有人使用

要先登入 Registry
```
az acr login --name myregistryRD 
```

## 從 Dockerfile 建置和推送映像

https://docs.microsoft.com/en-US/cli/azure/acr#az_acr_build

要推送映像到 Azure Container Registry，必須先有映像。 
先拉一個 Azure 的鏡像下來
在此範例中 hello-world ，從Microsoft Container Registry提取映射。

```
docker pull mcr.microsoft.com/hello-world
```
您必須使用登錄登入伺服器的完整名稱來標記映像，才能將映像推送至您的登錄。 
登入伺服器名稱的格式< 為 registry-name.azurecr.io > (必須是小寫) ，
例如 mycontainerregistry.azurecr.io。

使用 docker tag 命令來標記映像。 將 <login-server> 取代為 ACR 執行個體的登入伺服器名稱。


* 建立只有行的 Dockerfile

Dockerfile
```
FROM mcr.microsoft.com/hello-world

```

* 執行 az acr build 命令來建置映射，並在成功建置映像後，將其推送至您的登錄。 

```
az acr build --image sample/hello-world:v1 \
  --registry myregistryRD  \
  --file Dockerfile . 
  
```
