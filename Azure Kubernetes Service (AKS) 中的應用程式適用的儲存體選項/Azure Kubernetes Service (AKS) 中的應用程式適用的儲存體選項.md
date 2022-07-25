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
## Azure NetApp Files
```
Ultra 儲存體
進階儲存體
標準儲存體
```

## Azure Blob 儲存體
```
區塊 Blob
```
## 磁碟區類型
```
Kubernetes 磁片區不僅代表用來儲存和擷取資訊的傳統磁片。 

Kubernetes 磁碟區也可用來將資料插入 Pod 中，供容器使用。

Kubernetes 中的常見磁片區類型包括：
```

### emptyDir
```
通常用來作為 Pod 的暫存空間。 
Pod 內的所有容器都可存取磁碟區上的資料。 
寫入此磁片區類型的資料只會保存 Pod 的存留期。
刪除 Pod 之後，就會刪除磁片區。
此磁片區通常會使用基礎本機節點磁片儲存體，不過它也可以只存在於節點的記憶體中。
```

### secret
...

### configMap
...

## 永續性磁碟區  ( PV )

* Persistent Volume
```
Pod 通常會預期其儲存體能持續保存。 
永續性磁碟區 (PV) 是由 Kubernetes API 建立和管理的儲存體資源，可跨個別 Pod 的存留期持續保存。

您可以使用 Azure 磁片或檔案來提供 PersistentVolume。 

```

![](https://github.com/daniel-qa/Azure-Kubernetes-Service/blob/main/PIC/persistent-volumes.png?raw=true)


```
PersistentVolume 可由叢集管理員 靜態 建立，
或 Kubernetes API 伺服器 動態 建立。 

如果 Pod 已排程並要求目前無法使用的儲存體，Kubernetes 可以建立基礎 Azure 磁片或檔案儲存體，並將其連結至 Pod。 

動態佈建會使用 StorageClass 來識別需要建立的 Azure 儲存體類型。
```

## 儲存類別
```
若要定義不同層級的儲存體 (例如進階和標準)，您可以建立 StorageClass。

StorageClass 也會定義 reclaimPolicy。 
當您刪除 Pod 和永續性磁片區不再需要時，reclaimPolicy 會控制基礎 Azure 儲存體資源的行為。 
基礎儲存體資源可以刪除或保留，以便與未來的 Pod 搭配使用。
```



* 除非指定永續性磁片區的 StorageClass，否則使用預設的 StorageClass。 
