* 定義 Contains 

name, image
```
containers:
- name: azure-vote-front
  image: mcr.microsoft.com/azuredocs/azure-vote-front:v1
```


* 部署應用程式
```
kubectl apply -f azure-vote-all-in-one-redis.yaml
```

* 設定 Service 

```
kind: Service
metadata:
name: azure-vote-back
namespace: azure-vote-1655370967663
spec:
	ports:
	  - port: 6379
selector:
  app: azure-vote-back
  
```  
* contains 細部設定
```
containers:
  - name: azure-vote-front
    image: mcr.microsoft.com/azuredocs/azure-vote-front:v1
    ports:
    - containerPort: 80
    resources:
      requests:
        cpu: 250m
      limits:
        cpu: 500m
```
