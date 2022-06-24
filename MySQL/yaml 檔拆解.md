* 定義 Contains 

name, image
```
containers:
- name: azure-vote-front
  image: mcr.microsoft.com/azuredocs/azure-vote-front:v1
```

* Service 

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

多一個 namespace 
