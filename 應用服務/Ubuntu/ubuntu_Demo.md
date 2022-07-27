

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ubuntu
spec:
  replicas: 1
  selector:
    matchLabels:
      app: ubuntu
  template:
    metadata:
      labels:
        app: ubuntu
    spec:
      containers:
      - name: ubuntu
        image: myclusterregistry.azurecr.io/ubuntu:latest
        command: ["sleep", "123456"]
        ports:
        - containerPort: 22
        resources:
          requests:
            cpu: 250m
          limits:
            cpu: 500m
      nodeSelector:
        kubernetes.io/os: linux
        
---
apiVersion: v1
kind: Service
metadata:
  name: ubuntu-svc
spec:
  type: LoadBalancer
  ports:
    - port: 22
  selector:
    app: ubuntu
        
```       
