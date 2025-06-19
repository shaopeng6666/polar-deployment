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

# Rabbitmq
````
# 管理后台
http://localhost:15672/
````

# Keycloak
````
# 管理后台
http://localhost:8080/

# 使用命令行配置Keycloak
# 进入容器并切换到keycloak的bin目录
docker exec -it polar-keycloak bash
cd /opt/keycloak/bin

# 开启认证会话
./kcadm.sh config credentials \
    --server http://localhost:8080 \
    --realm master \
    --user user \
    --password password

# 创建realm
./kcadm.sh create realms -s realm=PolarBookshop -s enabled=true

# 创建角色
./kcadm.sh create roles -r PolarBookshop -s name=employee
./kcadm.sh create roles -r PolarBookshop -s name=customer

# 创建用户isabelle并赋予角色
./kcadm.sh create users -r PolarBookshop \
    -s username=isabelle \
    -s firstName=Isabelle \
    -s lastName=Dahl \
    -s enabled=true
./kcadm.sh add-roles -r PolarBookshop \
    --uusername isabelle \
    --rolename employee \
    --rolename customer

# 创建用户bjorn并赋予角色
./kcadm.sh create users -r PolarBookshop \
    -s username=bjorn \
    -s firstName=Bjorn \
    -s lastName=Vinterberg \
    -s enabled=true
./kcadm.sh add-roles -r PolarBookshop \
    --uusername bjorn \
    --rolename customer

# 设置密码
./kcadm.sh set-password -r PolarBookshop \
    --username isabelle --new-password password
./kcadm.sh set-password -r PolarBookshop \
    --username bjorn --new-password password

# 将edge-service注册为客户端
./kcadm.sh create clients -r PolarBookshop \
 -s clientId=edge-service \
 -s enabled=true \
 -s publicClient=false \
 -s secret=polar-keycloak-secret \
 -s 'redirectUris=["http://localhost:9000","http://localhost:9000/login/oauth2/code/*"]'
````