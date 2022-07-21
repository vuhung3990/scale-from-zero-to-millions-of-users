README

helm install -f mysql-value.yaml  mysql bitnami/mysql

# grant permission
# master pod -> terminal
# mysql -u root -p
# GRANT REPLICATION SLAVE ON *.* TO 'hungvu'@'%';

minikube addons enable ingress

