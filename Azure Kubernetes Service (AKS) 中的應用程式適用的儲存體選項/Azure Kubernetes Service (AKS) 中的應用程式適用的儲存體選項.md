https://github.com/daniel-qa/Azure-Kubernetes-Service/new/main

# Azure Kubernetes Service (AKS) 中的應用程式適用的儲存體選項

本文將介紹為 AKS 中的應用程式提供儲存體的核心概念：

* 磁碟區
* 永續性磁碟區
* 儲存類別
* 永續性磁碟區宣告

![](https://github.com/daniel-qa/Azure-Kubernetes-Service/blob/main/PIC/aks-storage-options.png?raw=true)

## 磁碟區
```

* 資料磁片區可以使用：

Azure 磁片、
Azure 檔案儲存體、
Azure NetApp Files
Azure Blob

```
## Azure 磁碟
```
使用 Azure 磁片 來建立 Kubernetes DataDisk 資源。 磁片類型包括：

Ultra 磁碟
進階 SSD
標準 SSD
標準 HDD

針對大部分的生產與開發工作負載，請使用 進階版 SSD。

由於 Azure 磁片會掛接為 ReadWriteOnce，因此只能供單一 Pod 使用。 針對可同時供多個節點存取的存放磁碟區，請使用 Azure 檔案儲存體。

```
