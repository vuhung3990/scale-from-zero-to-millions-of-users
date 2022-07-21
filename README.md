README

# 1. database setup
helm install -f mysql-value.yaml  mysql bitnami/mysql

# grant permission
# master pod -> terminal
# mysql -u root -p
# GRANT REPLICATION SLAVE ON *.* TO 'hungvu'@'%';

# 2. enable nginx ingress
minikube addons enable ingress

# 3. setup docker sample server
# local build image for minikube
eval $(minikube docker-env)
docker build . -t vuhung3990/sample_node_server
kubectl run sample_node_server  --image=vuhung3990/sample_node_server:latest --image-pull-policy=Never

# test
docker run -p 49160:3000 -d vuhung3990/sample_node_server
curl -i localhost:49160
docker kill <id>