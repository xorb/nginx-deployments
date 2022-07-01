# Installation

## Step 1: Create EC2

```sh
sudo apt update
```

## Step 2: Install NginX

Install NginX and create Server blocks
https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-22-04

How to deploy node apps with Nginx
https://www.digitalocean.com/community/tutorials/how-to-set-up-a-node-js-application-for-production-on-ubuntu-20-04

Adding Certbot and https
https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-22-04

```sh
sudo apt install nginx
```

### Step 3: Install docker

Guide: https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-22-04

### Step 4: Run applications

```sh

docker build -t xorb/codecloud-landing:10 .

docker run -d -p 3000:3000 xorb/codecloud-landing:10
```

```sh
docker run -d -p 3001:80 xorb/codecloud-editor:1

docker run -d -p 3001:80 126510223803.dkr.ecr.us-east-1.amazonaws.com/codecloud-editor:10
```

### Step 5: Create Nginx server blocks

```sh
server {
        listen 80;
        listen [::]:80;

        root /var/www/codecloud.cfd/html;
        index index.html index.htm index.nginx-debian.html;

        include /etc/nginx/mime.types;
        server_name codecloud.cfd;

        location / {
            proxy_pass http://localhost:3000;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection 'upgrade';
            proxy_set_header Host $host;
            proxy_cache_bypass $http_upgrade;
        }
        location /editor {
            proxy_pass http://localhost:3001;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection 'upgrade';
            proxy_set_header Host $host;
            proxy_cache_bypass $http_upgrade;
        }
}

```

## Readings

https://stackoverflow.com/questions/53207059/react-nginx-routing-to-subdirectory
