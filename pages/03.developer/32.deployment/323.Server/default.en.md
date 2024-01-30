---
title: Server
---

## Building the code
We need to clone the repo, install the dependencies and build. 
```
git clone https://github.com/vladimir1284/fleet-towit
cd fleet-towit
pnpm install
pnpm dev
```
Finally we run the dev server to make sure that everything is ok.

## Data migration
We make our first migration and seeding with the following command:

`npx prisma migrate dev`

The seeding is vital for having an initial **admin** company and a user of this company in order to be able to login into the site. Then, that user can create companies and other users.

`npx prisma db seed`

## Node.js Server
[PM2](https://pm2.keymetrics.io/docs/usage/quick-start/) serves the application using Node.js. The configuration file is:

```
// /home/vladimir/ecosystem.config.js
module.exports = {
  apps : [{
    name   : "fleet",
    script : "./fleet-towit/build/index.js",
    env: {
          "DATABASE_URL": "postgresql://[DB_USER]:[DB_PASSWORD]@localhost:5432/fleet",
        },
   port: 3000
  }]
}

```
Then we can start the service with:
```
pm2 start
```
The application needs to be served by HTTPS as a requirement of the [Auth.js](https://authjs.dev/) library. Nginx plays a great role for this setup. The nginx configuration file is:

```
# /etc/nginx/sites-available/fleet
server {
    server_name  fleet.crabdance.com;
    index index.html index.htm;
    access_log /var/log/nginx/nodeapp.log;
    error_log  /var/log/nginx/nodeapp-error.log error;

    location / {
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header Host $http_host;
        proxy_pass http://127.0.0.1:3000;
        proxy_redirect off;
    }
}

```

We need to configure the SSL certificate as explained [here](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-22-04).
