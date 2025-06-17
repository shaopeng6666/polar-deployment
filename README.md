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

# 启动Redis
kubectl apply -f kubernetes/platform/development/services/redis.yml

# 删除Redis
kubectl delete -f kubernetes/platform/development/services/redis.yml
````