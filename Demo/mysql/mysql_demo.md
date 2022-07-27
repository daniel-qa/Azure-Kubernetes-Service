## mysql 對外服務 

* mysql.yaml
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
      - name: mysql
        image: myclusterregistry.azurecr.io/mysql:5.7
        ports:
        - containerPort: 3306
        resources:
          requests:
            cpu: 250m
          limits:
            cpu: 500m
        env:
          # 在实际中使用 secret
        - name: MYSQL_ROOT_PASSWORD
          value: root
          
---
apiVersion: v1
kind: Service
metadata:
  name: mysql-svc
spec:
  type: LoadBalancer
  ports:
    - port: 3306
  selector:
    app: mysql
```
