https://docs.microsoft.com/zh-tw/azure/aks/azure-disk-volume

# 在 AKS Azure Kubernetes Service () 中建立具有 Azure 磁片的靜態磁片區

Pod 程式常常需要存取和保存外部資料磁碟區中的資料。 

如果單一 Pod 需要存取儲存體，您可以使用 Azure 磁碟來呈現原生磁碟區給應用程式使用。 

本文會示範如何手動建立 Azure 磁碟，並將其連結到 AKS 中的 Pod。

* 注意
 Azure 磁碟一次只能掛接到一個 Pod。 
 
 如果您需要在多個 Pod 之間共用永續性磁碟區，請使用 Azure 檔案服務。
 
 
 
## 儲存體類別靜態布建

| 名稱	| 意義	| 可用值	| 強制性	| 預設值 |
|  ----  | ----  |  ----  | ----  | ----  |
| volumeAttributes.cachingMode	| 磁片主機快取設定	| None, ReadOnly, ReadWrite	| 否		| 預設值 |

volumeAttributes.cachingMode	磁片主機快取設定	None, ReadOnly, ReadWrite	否	ReadOnly

volumeHandle	Azure 磁片 URI	/subscriptions/{sub-id}/resourcegroups/{group-name}/providers/microsoft.compute/disks/{disk-id}	是	N/A
volumeAttributes.fsType	檔案系統類型	ext4、 ext3 、 ext2 、 xfs 、 btrfs Linux、 ntfs Windows	否	ext4適用于 Linux， ntfs 適用于 Windows
volumeAttributes.partition	Linux) 僅支援現有磁片 (的磁碟分割數目	1, 2, 3	否	空白 (沒有分割區)
- 請確定分割區格式類似 -part1

