
* nginx.yaml
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: myclusterregistry.azurecr.io/nginx:v1
        ports:
        - containerPort: 80
        env: 
          - name: PHP_UPSTREAM_CONTAINER
            value: "php-fpm"               # service name 
          - name: PHP_UPSTREAM_PORT
            value: "9000"
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-svc
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: nginx
```
