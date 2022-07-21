

kubectl autoscale deployment phpmyadmin --cpu-percent=50 --min=3 --max=10


kubectl scale --replicas=5 deployment/azure-vote-front
