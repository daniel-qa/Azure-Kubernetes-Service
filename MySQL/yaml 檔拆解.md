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
