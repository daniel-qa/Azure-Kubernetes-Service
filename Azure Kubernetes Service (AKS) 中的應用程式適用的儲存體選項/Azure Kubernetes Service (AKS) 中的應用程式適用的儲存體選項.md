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
Kubernetes 通常會將個別 Pod 視為暫時的可處置資源。 

應用程式有不同的方法可供使用及保存資料。 

磁碟區就是可跨 Pod 和應用程式生命週期儲存、擷取和保存資料的方式之一。

傳統磁片區會建立為Azure 儲存體支援的 Kubernetes 資源。 

您可以手動建立要直接指派給 Pod 的資料磁片區，或讓 Kubernetes 自動建立它們。 

資料磁片區可以使用：Azure 磁片、Azure 檔案儲存體、Azure NetApp Files或Azure Blob。

```
