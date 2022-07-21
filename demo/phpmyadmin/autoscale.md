

# 自動調整 Pod
```
kubectl autoscale deployment phpmyadmin --cpu-percent=50 --min=3 --max=10
```

# 手動調整 Pod
```
kubectl scale --replicas=2 deployment/phpmyadmin
```
