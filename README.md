Forcing SSL with nginx in AWS EB
================================

Sandbox for testing nginx configs behind an Elastic Load Balancer without having to actually deploy to AWS.

## Goals

* Force SSL for all environments
* Force WWW for prod environment
* Pass-through for health check url (/okcomputer)
* One nginx config for all environments

## Setup
In your vagrant, boot2docker, docker machine, etc, edit /etc/hosts:

```
127.0.0.1 force-ssl.com www.force-ssl.com force-ssl.staging.com force-ssl.ci.com
```

The elb container hosts the reverse proxy (ELB) that terminates SSL and sets the X-Forwarded-Proto header.
The app container is the proxied app running nginx (passenger).

## Linking and running the containers

```
docker build -t elb ./elb
docker build -t app ./app
docker run -p 8088:8088 --name app -d  app
docker run -d -p 8080:8080 -p 8443:8443 --name elb --link app:app elb 
```

## Run the tests
```
curl -LkI http://force-ssl.ci.com:8080/index.html
curl -LkI http://force-ssl.ci.com:8080/okcomputer/test.html
curl -LkI http://force-ssl.staging.com:8080/index.html
curl -LkI http://force-ssl.staging.com:8080/okcomputer/test.html
curl -LkI http://force-ssl.com:8080/index.html
curl -LkI http://force-ssl.com:8080/okcomputer/test.html
```
