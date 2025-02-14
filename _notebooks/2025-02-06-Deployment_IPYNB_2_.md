---
layout: post
title: Deployment
description: Blog for Deployment Instructions
type: issues
comments: True
---

# Deployment

## Step 1: Prerequisits 
- Review the frontend and backend servers to make sure everything you want to show on your website is there and working.
- Have a deployment blog for your group, and include steps, terms, visuals and the purpose and process of deployment.
- Create an issue on flocker-frontend kanban board with roles for everybody on the group.
- Get account credentials from Mr. Mortensen
- Use the AWS cockpit to begin deployment process.

## Step 2: Testing your Server
- Make sure that your localhost is working (frontend to backend integration). Use postman and other tools to check backend functionality. If there is a problem locally with a feature or the whole website, you need to debug and fix it before deploying.

## Step 3: Subdomain
- Setup the DNS endpoint through AWS Route 53.
- Server: https://takeabyte.stu.nighthawkcodingsociety.com/
- Domain: stu.nighthawkcodingsociety.com
- Subdomain: takeabyte

## Step 4: Ports
- You need to select a port for your website, 8887 is Mortensens, our groups port is 8403.

## Backend Changes
- main.py: Prepare the localhost test server port to run on 8403 for consistency (change all of the 8887 to 8403)


```python
if __name__ == "__main__":
   with app.app_context():
       app.run(debug=True, host="0.0.0.0", port="8403")
```

- Dockerfile: Change this file to run the server as a virtual machine on the deployment host.


```python
FROM docker.io/python:3.12.4

WORKDIR /

# --- [Install python and pip] ---
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y python3 python3-pip git
COPY . /

RUN pip install --no-cache-dir -r requirements.txt
RUN pip install gunicorn

ENV GUNICORN_CMD_ARGS="--workers=3 --bind=0.0.0.0:8403"

EXPOSE 8403

# Define environment variable
ENV FLASK_ENV=deploy

CMD [ "gunicorn", "main:app" ]
```

- docker-compose.yml: Change this file to be the make for Docker.


```python
version: '3'
services:
        web:
                image: takeabyte
                build: .
                env_file:
                        - .env # This file is optional; defaults will be used if it does not exist
                ports:
                        - "8403:8403"
                volumes:
                        - ./instance:/instance
                restart: unless-stopped
```

nginx_file: Change file for reverse proxy (internet -> application -> back to requester)


```python
server {
    listen 80;
    listen [::]:80;
    server_name takeabyte.stu.nighthawkcodingsociety.com;

    location / {
            proxy_pass http://localhost:8403;

        # Preflighted requests
        if ($request_method = OPTIONS) {
                add_header "Access-Control-Allow-Credentials" "true" always;
                add_header "Access-Control-Allow-Origin"  "https://nighthawkcoders.github.io" always;
                add_header "Access-Control-Allow-Methods" "GET, POST, PUT, DELETE, OPTIONS, HEAD" always;
                add_header "Access-Control-Allow-MaxAge" 600 always;
                add_header "Access-Control-Allow-Headers" "Authorization, Origin, X-Origin, X-Requested-With, Content-Type, Accept" always;
                return 204;
        }
    }
}
```

## Frontend Changes:
- assets/api/config.js: Change the frontend to access your domain, ports must match to your localhost, port, and domain settings.


```python
export var pythonURI;
if (location.hostname === "localhost") {
        pythonURI = "http://localhost:8403";
} else if (location.hostname === "127.0.0.1") {
        pythonURI = "http://127.0.0.1:8403";
} else {
        pythonURI =  "https://takeabyte.stu.nighthawkcodingsociety.com";
}
```

## Step 5: Launching an EC2 Instance
- Log into AWS Console: Go to EC2 Dashboard. To login to the deployment server on AWS EC2, you need to use the cockpit backdoor. https://cockpit.stu.nighthawkcodingsociety.com/

- Then you will need to launch a new EC2 instance

## Step 6: Deployment
- Make sure your port is open (8403) using `docker ps`

- Make sure your `Dockerfile` and `docker-compose.yml` match the port (8403) discovered with the `docker ps` on AWS EC2.
- Test `docker-compose up` or `sudo docker-compose up` 
- After it is done building, type in `http://localhost:8403`

## Step 7: Server Setup
- `cd ~` 
- Clone your backend repo: `git clone https://github.com/lalita1809/takeabyte_backend.git`
- Navigate to the repo: `cd takeabyte_backend`
- Build your site using `docker-compose up -d --build`
- Test your site using `curl localhost:8403`
    - Make sure your see a bunch of html code lines in your terminal (represents the content of your home page). If you see an error message, it means your server is not running properly, and you need to debug on your localhost. If there is a broken pipe error, you need to check your ports in docker-compose.yml and all the Docker file. Check docker ps to make sure that your port is only being used by your group, not any other group.
- Configure Route 53 DNS for the subdomain. 

## Step 8: Nginx Setup


```python
cd /etc/nginx/sites-available
sudo nano takeabyte.nginx_file takeabyte.stu
cd /etc/nginx/sites-enabled
sudo ln -s /etc/nginx/sites-available/takeabyte.stu /etc/nginx/sites-enabled
sudo nginx -t
sudo systemctl restart nginx
```

Use the


```python
cat takeabyte.stu
```

to check if the contents of the nginx file are correctly copied into takeabyte.stu in sites available.

secure the server with Cerbot (SSL):


```python
sudo cerbot --nginx
```

## Step 9: Update Deployment Process
- pull the latest changes in from the repository


```python
cd ~/takeabyte_backend
docker-compose down 
git pull
docker-compose build
docker-compose up -d
sudo cp -f takeabyte.nginx_file /etc/nginx/sites-available/takeabyte.stu
```

troubleshoot if there are any errors


```python
curl localhost:8403
docker-compose ps
docker ps
```
