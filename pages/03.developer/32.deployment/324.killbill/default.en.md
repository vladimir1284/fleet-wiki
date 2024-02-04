# Running Kill Bill

## Docker compose

The following compose file is [available](https://github.com/killbill/killbill-cloud/blob/master/docker/compose/docker-compose.kb.yml) for running the latest Kill Bill stack.

! It is important to add the line `- SECRET_KEY_BASE=[RADOM_SECRET]` as it is in the following dockerfile for **kaui** to work properly. We also had to add the **links** section to **killbill** and **kaui** containers.

```yml
# KB stack
version: '3.2'
volumes:
  db:
services:
  killbill:
    image: killbill/killbill:latest
    ports:
      - "8080:8080"
      - "8000:8000"
      - "12345:12345"
    environment:
      - KILLBILL_DAO_URL=jdbc:mysql://db:3306/killbill
      - KILLBILL_DAO_USER=root
      - KILLBILL_DAO_PASSWORD=[DB_PASSWORD]
      - KILLBILL_METRICS_INFLUXDB=false
      - KILLBILL_METRICS_INFLUXDB_HOST=host.docker.internal
      - KILLBILL_METRICS_INFLUXDB_PORT=8086
    links:
      - db 
  kaui:
    image: killbill/kaui:latest
    ports:
      - "9090:8080"
    environment:
      - KAUI_CONFIG_DAO_URL=jdbc:mariadb://db:3306/kaui
      - KAUI_CONFIG_DAO_USER=root
      - KAUI_CONFIG_DAO_PASSWORD=[DB_PASSWORD]
      - KAUI_KILLBILL_URL=http://killbill:8080
      - KAUI_KILLBILL_API_KEY=[API_KEY]
      - KAUI_KILLBILL_API_SECRET=[API_SECRET]
      - SECRET_KEY_BASE=[RADOM_SECRET]
    links:
      - db 
      - killbill 
  db:
    image: killbill/mariadb:0.24
    volumes:
      - type: volume
        source: db
        target: /var/lib/mysql
    expose:
      - "3306"
    environment:
      - MYSQL_ROOT_PASSWORD=[DB_PASSWORD]
```

The above configuration can be compiled with te following line:

`docker-compose -f docker-compose.kb.yml -p kb up`

## Nginx

We make two proxy redirection from **Nginx** for **KillBill** and **kaui** servers.

```
# /etc/nginx/sites-available/killbill
server {
    server_name  killbill.towithouston.com;
    index index.html index.htm;
    access_log /var/log/nginx/nodeapp.log;
    error_log  /var/log/nginx/nodeapp-error.log error;

    location / {
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header Host $http_host;
        proxy_pass http://127.0.0.1:8080;
        proxy_redirect off;
    }
}
```
```
# /etc/nginx/sites-available/kaui
server {
    server_name  kaui.towithouston.com;
    index index.html index.htm;
    access_log /var/log/nginx/nodeapp.log;
    error_log  /var/log/nginx/nodeapp-error.log error;

    location / {
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header Host $http_host;
        proxy_pass http://127.0.0.1:9090;
        proxy_redirect off;
    }
}
```
We needed to modify the `/etc/nginx/nginx.conf` for extending the timeout:

```	
http {
    ...
    # set client body size to 100 MB #
    client_max_body_size 100M;
    proxy_read_timeout 600s;
}
```
