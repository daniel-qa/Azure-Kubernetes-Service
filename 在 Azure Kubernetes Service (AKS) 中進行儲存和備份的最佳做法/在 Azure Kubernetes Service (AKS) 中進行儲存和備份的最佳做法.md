https://github.com/MicrosoftDocs/azure-docs.zh-tw/blob/master/articles/aks/operator-best-practices-storage.md

# 在 Azure Kubernetes Service (AKS) 中進行儲存和備份的最佳做法



在本文中，您將了解：

* 有哪些可用的儲存體類型
* 如何針對儲存體效能正確評估 AKS 節點大小
* 磁碟區的動態佈建和靜態佈建之間的差異
* 備份並保護資料磁碟區的方法

## 選擇適當的儲存體類型
**最佳做法指引** 

了解應用程式的需求以挑選正確的儲存體。 針對生產工作負載使用高效能、以 SSD 備份的儲存體。 在有多個並行連線之需求的情況下，針對網路型儲存體進行規劃。

應用程式通常會需要不同類型及速度的儲存體。 您的應用程式是否需要會連線至個別 Pod 的儲存體，或是需要會在多個 Pod 之間共用的儲存體？ 儲存體是否是要用來對資料進行唯讀存取，還是要用來寫入大量結構化資料？ 這些儲存體需求會決定應使用的最適當儲存體類型。

下表會概述可用的儲存體類型及其功能：

```


```
AKS 中針對磁碟區所提供的兩個主要儲存體類型，是由 Azure 磁碟或 Azure 檔案所支援。 為了提升安全性，這兩種儲存體預設都會使用 Azure 儲存體服務加密 (SSE) 來對待用資料進行加密。 

在 Standard 和 Premium 效能層級中都有提供 Azure 檔案儲存體和 Azure 磁片：

「進階」** 磁碟是由高效能固態硬碟 (SSD) 所支援。 針對所有生產環境工作負載，都建議使用進階磁碟。
「標準」** 磁碟是由一般磁碟 (HDD) 所支援，且適用於封存或不常存取的資料。

## 建立及使用儲存體類別來定義應用程式需求

您所使用的儲存體類型，是使用 Kubernetes「儲存體類別」** 所定義。 儲存體類別接著會參考於 Pod 或部署規格中。 這些定義會一起運作以建立適當的儲存體，並將它連線至 Pod。 如需詳細資訊，請參閱 [AKS 中的儲存體類別](https://github.com/MicrosoftDocs/azure-docs.zh-tw/blob/master/articles/aks/concepts-storage.md#storage-classes)。

* 不同的 VM 大小在本機和附加磁碟 IOPS (每秒輸入/輸出作業) 上限上，也具有儲存體效能上的差異。
