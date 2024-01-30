---
title: Storage
---

# Data Storage
[MinIO](https://min.io/) is an open source distributed object storage server S3 compatible.We run MinIO using docker as explained [here](https://github.com/minio/minio/blob/master/docs/docker/README.md), with the following line:

```
sudo docker run -d  -p 9000:9000   -p 9001:9001   --name minio1   -v ~/minio/data:/data   -e "MINIO_ROOT_USER=[USER]"   -e "MINIO_ROOT_PASSWORD=[PASSWORD]"   quay.io/minio/minio server /data --console-address ":9001"
```
The following configuration allows access to the api from outside and serves statics files.

```
# /etc/nginx/sites-available/minio
upstream minio_s3 {
   least_conn;
   server localhost:9000;
}

server {
   listen  [::]:80;
   server_name   minios3.crabdance.com;

   # Allow special characters in headers
   ignore_invalid_headers off;
   # Allow any size file to be uploaded.
   # Set to a value such as 1000m; to restrict file size to a specific value
   client_max_body_size 0;
   # Disable buffering
   proxy_buffering off;
   proxy_request_buffering off;

   location / {
      proxy_set_header Host $http_host;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header X-Forwarded-Proto $scheme;

      proxy_connect_timeout 300;
      # Default is HTTP/1, keepalive is only enabled in HTTP/1.1
      proxy_http_version 1.1;
      proxy_set_header Connection "";
      chunked_transfer_encoding off;

      proxy_pass http://minio_s3; # This uses the upstream directive definition to load balance
   }
}
```
For the MinIO Console Web GUI we used:
```
# /etc/nginx/sites-available/minio_ui 
server {
    server_name  minioui.strangled.net;
    index index.html index.htm;
    access_log /var/log/nginx/nodeapp.log;
    error_log  /var/log/nginx/nodeapp-error.log error;

    location / {
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header Host $http_host;
        proxy_pass http://127.0.0.1:9001;
        proxy_redirect off;
    }
}
```
We need to configure the SSL certificate, for both sites, as explained [here](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-22-04).
