https://docs.microsoft.com/zh-tw/azure/container-registry/container-registry-quickstart-task-cli

建立容器登錄庫
使用 az acr create 命令建立容器登錄。 登錄名稱在 Azure 內必須是唯一的，且包含 5-50 個英數字元。 下列範例將使用 myContainerRegistry008。 請將此更新為唯一的值。

試試看
az acr create --resource-group myResourceGroup \
  --name myContainerRegistry008 --sku Basic
