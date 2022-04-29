---
title: How to run NGINX-Proxy-Manager using Docker Swarm?
excerpt_separator: <!--end_excerpt-->
---

NGINX-Proxy-Manager is a very simple method to set a NGINX Ingress. In this tutorial we present a very simple way to run it on your for your Docker Swarm cluster.

<!--end_excerpt-->

Step 1: Make sure you initialized Docker Swarm

```bash
docker swarm init
```

Step 2: Create an external network

```
docker network create --driver overlay --opt encrypted --attachable --scope "swarm" proxy_net
```

Step 3: Run nginx-admin as a Swarm service

```yaml
version: '3.6'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    networks:
      - proxy_net
    ports:
      - target: 80
        published: 80
        protocol: tcp
        mode: host

      - target: 443
        published: 443
        protocol: tcp
        mode: host

      - "81:81"
    volumes:
      - data:/data
      - letsencrypt:/etc/letsencrypt

volumes:
  data:
  letsencrypt:

networks:
  proxy_net:
    external: true
```
