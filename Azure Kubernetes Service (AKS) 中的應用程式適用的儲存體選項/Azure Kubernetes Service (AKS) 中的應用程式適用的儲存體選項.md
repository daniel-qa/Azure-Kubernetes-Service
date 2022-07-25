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

* Ultra 磁碟
* 進階 SSD
* 標準 SSD
* 標準 HDD

生產與開發工作負載, 建議使用進階版 SSD。

由於 Azure 磁片會掛接為 ReadWriteOnce，因此只能供單一 Pod 使用。 

需要同時供多個節點存取的存放磁碟區，請使用 Azure 檔案儲存體。

```

## Azure 檔案

```
使用Azure 檔案儲存體，將 Azure 儲存體帳戶支援的 SMB 3.1.1 共用或 NFS 4.1 共用掛接至 Pod。 
檔案可讓您跨多個節點和 Pod 共用資料，而且可以使用：

由高效能 SSD 支援的 Azure 進階版儲存體
由一般 HDD 支援的 Azure 標準儲存體

```


## emptyDir
```
通常用來作為 Pod 的暫存空間。 Pod 內的所有容器都可存取磁碟區上的資料。 寫入此磁片區類型的資料只會保存 Pod 的存留期。 刪除 Pod 之後，就會刪除磁片區。 此磁片區通常會使用基礎本機節點磁片儲存體，不過它也可以只存在於節點的記憶體中。
```
