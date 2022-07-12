https://docs.microsoft.com/zh-tw/azure/aks/load-balancer-standard

# 在 Azure Kubernetes Service (AKS) 中使用公用Standard Load Balancer



## 使用公用標準負載平衡器

public-svc.yaml 的服務資訊清單：

```
apiVersion: v1
kind: Service
metadata:
  name: public-svc
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: public-app
 ```   

* 部署
* 
```
kubectl apply -f public-svc.yaml

```
