

kubectl autoscale deployment phpmyadmin --cpu-percent=50 --min=3 --max=10


kubectl scale --replicas=2 deployment/phpmyadmin
