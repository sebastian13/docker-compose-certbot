# Certbot
This docker-compose.yml users the **official certbot** container. 

The container will use the network **www-network**, which is the network my nginx proxy is using.

Take a look at my implementation of a [nginx-proxy](https://github.com/sebastian13/docker-compose-nginx-proxy). I suggest using it together with this docker-compose example.

## Receive a Certificate

Get a Let's Encrypt Certificate by defining your Domain + Email-Address in *example.com.yml* and start it via

`docker-compose -f example.com.yml up`

You should receive the message: "Congratulations! Your certificate and chain have been saved ..."

## Renew your Certificates
Use rancher's crontab to automatically renew your certs.

```
version: '3'

services:
  crontab:
    image: rancher/container-crontab:v0.3.0
    container_name: crontab
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```

Then run

`docker-compose -f renew.yml up -d`