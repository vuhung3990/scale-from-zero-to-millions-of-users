README

# 1. database setup
helm install -f mysql-value.yaml  mysql bitnami/mysql

# grant permission
# master pod -> terminal
# mysql -u root -p
# GRANT REPLICATION SLAVE ON *.* TO 'hungvu'@'%';

# 2. enable nginx ingress & metric server
minikube addons enable ingress
minikube addons enable metrics-server
# view log http://(minikube ip):32000
minikube addons enable logviewer

# 3. setup sample server
kubectl apply -f node-server-deployment.yaml
kubectl apply -f node-server-service.yaml

# 4. setup ingress-rules
kubectl apply -f ingress-rules.yaml

# 5. HPA setup
kubectl apply -f horizontal-pod-autoscaler.yaml

# utilities
# log pods details (include internal ip)
kubectl get pods -o wide
# log ingress (include pod's internal ip)
kubectl logs -f --tail=20 -n ingress-nginx ingress-nginx-controller-5f66978484-jrr7w
# request 100000, concurency 2 (request 2 each turn)
# https://httpd.apache.org/docs/2.4/programs/ab.html
ab -n 100000 -c 2  http://sample.com/
# watch pod up/down
watch -n 1 'kubectl top pod'