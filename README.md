# Docker
````
# 使用Docker Compose启动服务
docker-compose up -d

# 使用Docker Compose停止服务
docker-compose down

# Docker Compose只启动Postgresql
docker-compose up -d polar-postgres
````

# Kubernetes
````
# 启动Postgresql
kubectl apply -f kubernetes/platform/development/services/postgresql.yml

# 删除Postgresql
kubectl delete -f kubernetes/platform/development/services/postgresql.yml

# 启动目录下所有服务
kubectl apply -f kubernetes/platform/development/services

# 删除目录下所有服务
kubectl delete -f kubernetes/platform/development/services
````