# docker-mysql-nginx-deploy
In this repo we will create a docker containers with docker-compose file and deploy MySQL and Nginx in it.

### Environment Setup
To setup the environment, we will create a directory and go to that directory using below command 
```
mkdir myServer
cd myServer
```

### Create credentials for mysql
We will create password files for our db root and normal user. We can create those credentials with ``rand`` command so that it creates random numbers and letters
```
openssl rand -base64 32 > db_password.txt
openssl rand -base64 32 > db_root_password.txt
```

### Docker-compose build
We can build the docker compose file using the below command - 
```
docker-compose up
```
We should be able to see two containers up and runinng 
```
docker-compose ps
  Name                Command             State                    Ports
------------------------------------------------------------------------------------------
db-server     docker-entrypoint.sh mysqld   Up      0.0.0.0:3306->3306/tcp, 33060/tcp
web-server    nginx -g daemon off;          Up      0.0.0.0:443->443/tcp, 0.0.0.0:80->80/tcp
```

### Test the system
To test the containers we can use below methods 
```
NGINX:
http://localhost

DB:
docker exec -it db-server mysql -u root -p
```

Nginx should show the default http page and DB should ask for the root password. 
