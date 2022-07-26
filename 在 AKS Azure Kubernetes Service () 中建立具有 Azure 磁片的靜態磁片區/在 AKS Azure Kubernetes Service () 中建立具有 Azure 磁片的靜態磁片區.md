https://docs.microsoft.com/zh-tw/azure/aks/azure-disk-volume

# 在 AKS Azure Kubernetes Service () 中建立具有 Azure 磁片的靜態磁片區

Pod 程式常常需要存取和保存外部資料磁碟區中的資料。 

如果單一 Pod 需要存取儲存體，您可以使用 Azure 磁碟來呈現原生磁碟區給應用程式使用。 

本文會示範如何手動建立 Azure 磁碟，並將其連結到 AKS 中的 Pod。

* 注意

  Azure 磁碟一次只能掛接到一個 Pod。 如果您需要在多個 Pod 之間共用永續性磁碟區，請使用 Azure 檔案服務。
 
 
 
## 儲存體類別靜態布建

* 下表描述 Azure 磁片 CSI 驅動程式靜態布建的 儲存體 類別參數：

| 名稱	| 意義	| 可用值	| 強制性	| 預設值 |
|  ----  | ----  |  ----  | ----  | ----  |
| volumeHandle | Azure 磁片 URI | /subscriptions/{sub-id}/resourcegroups/{group-name}/providers/microsoft.compute/disks/{disk-id} | 是 | N/A |
| volumeAttributes.fsType | 檔案系統類型 | ext4、 ext3 、 ext2 、 xfs 、 btrfs Linux、 ntfs Windows | 否 | ext4適用于 Linux， ntfs 適用于 Windows |
| volumeAttributes.partition | Linux) 僅支援現有磁片 (的磁碟分割數目 | 1, 2, 3 | 否 | 空白 (沒有分割區)- 請確定分割區格式類似 -part1 |
| volumeAttributes.cachingMode	| 磁片主機快取設定	| None, ReadOnly, ReadWrite	| 否		| 預設值 |


## 建立 Azure 磁碟

建立與 AKS 搭配使用的 Azure 磁碟時，可以在節點資源群組中建立磁碟資源。 

此方法可讓 AKS 叢集存取和管理磁碟資源。 

如果在另一個資源群組中建立磁片須將角色授與叢集 Contributor Azure Kubernetes Service (AKS) 受控識別給磁片的資源群組。 

此範例為會在與叢集相同的資源群組中建立磁片。

1 .使用 az aks show 命令識別資源組名，並新增 --query nodeResourceGroup 參數。 

  下列範例會在 myResourceGroup 資源群組名稱中，取得 AKS 叢集名稱 myAKSCluster 的節點資源群組：

```
az aks show --resource-group myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv

MC_myResourceGroup_myAKSCluster_eastus

az aks show --resource-group CoreServiceRG-Test --name MyCluster --query nodeResourceGroup -o tsv

MC_CoreServiceRG-Test_MyCluster_japaneast

```



2.使用 az disk create 命令建立 磁片。
  
  下列範例會建立 20GiB 磁片，並在建立磁片之後輸出磁片的識別碼。  
  ```
  az disk create \
  --resource-group MC_myResourceGroup_myAKSCluster_eastus \
  --name myAKSDisk \
  --size-gb 20 \
  --query id --output tsv
  
  ```
  
  ```
  az disk create \
  --resource-group MC_CoreServiceRG-Test_MyCluster_japaneast \
  --name myAKSDisk \
  --size-gb 20 \
  --query id --output tsv
  
  ```
  
當命令成功完成之後，磁碟資源識別碼就會隨即顯示，如下列輸出範例所示。 下一節會使用此磁片識別碼來掛接磁片。

```
/subscriptions/<subscriptionID>/resourceGroups/MC_myAKSCluster_myAKSCluster_eastus/providers/Microsoft.Compute/disks/myAKSDisk

```

