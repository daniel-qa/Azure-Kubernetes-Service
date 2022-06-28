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
