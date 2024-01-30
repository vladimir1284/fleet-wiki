---
title: Database
---

# Database server
For the database we will be using postgresql on a docker image.

## Docker installation
It is important to install docker from [this instructions](https://docs.docker.com/engine/install/ubuntu/) and not from **snap** in order to be able to persist data.

## Postgresql configuration
We use the following command:
```
sudo docker run -v /var/lib/postgresql/data:/var/lib/postgresql/data -p 5432:5432 --restart=always --name postgres -e POSTGRES_PASSWORD=[MyPassword] -d postgres
```

In this way, the data will persist in the host machine directory `/var/lib/postgresql/data`.

In order to allow remote connections, the `/var/lib/postgresql/data/pg_hba.conf` file must be edited as explained [here](https://medium.com/@vinjenks/dockerized-local-postgres-and-scram-authentication-a-quick-fix-21c432951bd) to be :
```
# TYPE  DATABASE        USER            ADDRESS                 METHOD

# "local" is for Unix domain socket connections only
local   all             all                                     scram-sha-256
# IPv4 local connections:
host    all             all             127.0.0.1/32            scram-sha-256
# IPv6 local connections:
host    all             all             ::1/128                 scram-sha-256
# Allow replication connections from localhost, by a user with the
# replication privilege.
local   replication     all                                     scram-sha-256
host    replication     all             127.0.0.1/32            scram-sha-256
host    replication     all             ::1/128                 scram-sha-256
```
### Installing PgAdmin 4
We must follow [this tutorial](https://medium.com/@marvinjungre/get-postgresql-and-pgadmin-4-up-and-running-with-docker-4a8d81048aea) for setting up PgAdmin 4 to manage the database.
The execution line is:
```
sudo docker run --restart=always --name pgadmin-container -p 5050:80 -e PGADMIN_DEFAULT_EMAIL=vladimir.rdguez@gmail.com -e PGADMIN_DEFAULT_PASSWORD=[MyPassword] -d dpage/pgadmin4

```
We also need to configure a reverse proxy for this service as:

```
# /etc/nginx/sites-available/pgadmin
server {
    server_name  pgadmin.crabdance.com;
    index index.html index.htm;
    access_log /var/log/nginx/nodeapp.log;
    error_log  /var/log/nginx/nodeapp-error.log error;

    location / {
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header Host $http_host;
        proxy_pass http://127.0.0.1:5050;
        proxy_redirect off;
    }
}

```

We need to configure the SSL certificate as explained [here](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-22-04).

In order to access the database, the IP address of the postgres container should be queried as follows:
```
sudo docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' postgres
```
