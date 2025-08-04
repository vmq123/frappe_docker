erpnext-two on ThinkpadX1:

sudo systemctl start docker
sudo systemctl status docker
docker stop mariadb-database
docker start traefik-traefik-1

### Mariadb
docker compose --project-name mariadb-two -f ./gitops/mariadb-two.yaml up -d

### ERPNext-two
docker compose --project-name erpnext-two -f ./gitops/erpnext-two.yaml up -d

docker compose --project-name erpnext-two exec backend \
  bench new-site --mariadb-user-host-login-scope=% --db-root-password osboxes.org --install-app erpnext --admin-password osboxes.org c01.vms88.com
 
//20250803: error cannot connect to mariadb

docker exec -it erpnext-two-backend-1 sh
docker stop mariadb-database
docker exec -it mariadb-database sh
docker stop erpnext-one-frontend-1 erpnext-one-queue-long-1 erpnext-one-queue-short-1 erpnext-one-backend-1 erpnext-one-websocket-1 erpnext-one-scheduler-1 erpnext-one-redis-cache-1 erpnext-one-redis-queue-1

docker exec -it erpnext-one-backend-1 sh
docker cp -R mariadb-database:/var/lib/mysql/* ~/frappe_docker/mariadb-database-var-lib-mysql




docker stop erpnext-two-frontend-1 erpnext-two-queue-long-1 erpnext-two-queue-short-1 erpnext-two-backend-1 erpnext-two-websocket-1 erpnext-two-scheduler-1 erpnext-two-redis-cache-1 erpnext-two-redis-queue-1


### Remove containter
#### List containter existed
docker ps -a -f status=exited

#### Remove
docker rm erpnext-two-frontend-1 erpnext-two-queue-long-1 erpnext-two-queue-short-1 erpnext-two-backend-1 erpnext-two-websocket-1 erpnext-two-scheduler-1 erpnext-two-redis-cache-1 erpnext-two-redis-queue-1 erpnext-two-configurator-1

### Remove image to reinstall
docker images -a

docker rmi 121b7c3be4fb 3dd46f3fe3c1 92c6f6448f78 b7f611844a19
