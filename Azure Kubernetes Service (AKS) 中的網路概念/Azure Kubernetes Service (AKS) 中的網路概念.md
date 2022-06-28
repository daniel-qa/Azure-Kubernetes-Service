https://docs.microsoft.com/zh-tw/azure/aks/concepts-network

# Azure Kubernetes Service (AKS) 中的網路概念

## Kubernetes 基本概念
```
為了允許存取您的應用程式或在應用程式元件之間存取，Kubernetes 會提供虛擬網路的抽象層。 
Kubernetes 節點會連線到虛擬網路，並提供 Pod 的輸入和輸出連線能力。 
Kube-proxy 元件會在每個節點上執行以提供這些網路功能。
```
```
在 Kubernetes 中：

服務 會以邏輯方式將 Pod 分組，以允許透過 IP 位址或 DNS 名稱直接存取特定埠。
您可以使用 負載平衡器來散發流量。
應用程式流量的更複雜路由也可以使用 輸入控制器來達成。
Kubernetes 網路原則可以針對 Pod 的網路流量進行安全性和篩選。
Azure 平臺也會簡化 AKS 叢集的虛擬網路。 
當您建立 Kubernetes 負載平衡器時，也會建立及設定基礎 Azure 負載平衡器資源。 
當您對 Pod 開啟網路連接埠時，即會設定對應的 Azure 網路安全性群組規則。 
針對 HTTP 應用程式路由，Azure 也可以設定 外部 DNS ，因為已設定新的輸入路由。

```

## 服務

* 為了簡化應用程式工作負載的網路設定，Kubernetes 會使用 服務 ，以邏輯方式將一組 Pod 分組在一起，並提供網路連線能力。 以下是可用的服務類型：


### 叢集 IP
```
建立內部 IP 位址，以在 AKS 叢集內使用。 這非常適用於支援叢集內其他工作負載的內部專用應用程式。
```
![](https://docs.microsoft.com/zh-tw/azure/aks/media/concepts-network/aks-clusterip.png)

### NodePort
```
在基礎節點上建立埠對應，讓應用程式可以直接使用節點 IP 位址和埠來存取。
```
![](https://docs.microsoft.com/zh-tw/azure/aks/media/concepts-network/aks-nodeport.png)

### LoadBalancer
```
建立 Azure 負載平衡器資源、設定外部 IP 位址，並將要求的 Pod 連線到負載平衡器後端集區。 
若要允許客戶流量觸達應用程式，可在所需的連接埠上建立負載平衡規則。

針對輸入流量的額外控制和路由，您可以改用 輸入控制器。
```
![](https://docs.microsoft.com/zh-tw/azure/aks/media/concepts-network/aks-loadbalancer.png)

### ExternalName
```
建立特定的 DNS 專案，以方便應用程式存取。

負載平衡器和服務 IP 位址可以動態指派，或者您可以指定現有的靜態 IP 位址。 
您可以同時指派內部和外部靜態 IP 位址。 現有的靜態 IP 位址通常會系結至 DNS 專案。

您可以同時建立內部和外部負載平衡器。 由於內部負載平衡器只會指派私人 IP 位址，因此無法從網際網路加以存取。

```
