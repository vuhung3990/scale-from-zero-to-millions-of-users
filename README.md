README

# 1. database setup
helm install -f mysql-value.yaml  mysql bitnami/mysql

# grant permission
# master pod -> terminal
# mysql -u root -p
# GRANT REPLICATION SLAVE ON *.* TO 'hungvu'@'%';

# 2. enable nginx ingress
minikube addons enable ingress

# 3. setup sample server
kubectl apply -f docker_node_server/node-server-deployment.yaml
kubectl apply -f docker_node_server/node-server-service.yaml

