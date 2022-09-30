docker pull mysql:5.7

docker run --name mysql-5.7 -e MYSQL_ROOT_PASSWORD=root -d mysql:5.7


docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' workspace_mysql

docker exec -it workspace_php /bin/ash