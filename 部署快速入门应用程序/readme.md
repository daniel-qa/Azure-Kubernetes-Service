* yml 檔
```
一開始會描敘 apiVersion
ex:
  - apiVersion: v1

* 再依不同的 kind ，進行區分

ex:
kind: Namespace
...
kind: Deployment
...
kind: Service

```

* Namespace 一般很簡單
```
- apiVersion: v1
  kind: Namespace
  metadata:
    name: azure-vote-1655370967663
  spec:
    finalizers:
      - kubernetes
```
* Deployment 會定義容器，名稱，硬體資源，Port 等等

```
- apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: azure-vote-back
    namespace: azure-vote-1655370967663
  spec:
    replicas: 1
    selector:
      matchLabels:
        app: azure-vote-back
    template:
      metadata:
        labels:
          app: azure-vote-back
      spec:
        nodeSelector:
          beta.kubernetes.io/os: linux
        containers:
          - name: azure-vote-back
            image: mcr.microsoft.com/oss/bitnami/redis:6.0.8
            env:
              - name: ALLOW_EMPTY_PASSWORD
                value: 'yes'
            resources:
              requests:
                cpu: 100m
                memory: 128Mi
              limits:
                cpu: 250m
                memory: 256Mi
            ports:
              - containerPort: 6379
                name: redis
                
```                

* Service 則是負責容器的對外通訊(也就是負責網路)

```
- apiVersion: v1
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
