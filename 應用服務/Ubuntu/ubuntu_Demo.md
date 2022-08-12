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
        image: ubuntu
        command: ["sleep", "123456"]
        ports:
        - name: ssh22
          containerPort: 22
        - name: web80
          containerPort: 80
        resources:
          requests:
            cpu: 250m
          limits:
            cpu: 500m
        volumeMounts:
          - name: azure
            mountPath: /opt
      volumes:
        - name: azure
          persistentVolumeClaim:
            claimName: my-azurefile
        
      nodeSelector:
        kubernetes.io/os: linux
        
#---
apiVersion: v1
kind: Service
metadata:
  name: ubuntu-svc
spec:
  type: LoadBalancer
  ports:
    - name: ssh22
      port: 22
    - name: web80
      port: 80
  selector:
    app: ubuntu
