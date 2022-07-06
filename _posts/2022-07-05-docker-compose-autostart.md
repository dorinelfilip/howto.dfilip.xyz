---
title: How to make a docker-compose application to autostart as a service?
excerpt_separator: <!--end_excerpt-->
---

# On Ubuntu

Create a file `/etc/systemd/system/docker-compose-example.service` as following:

```
[Unit]
Description=Docker Compose Application Service
Requires=docker.service
After=docker.service

[Service]
Type=oneshot
RemainAfterExit=yes
User=myuser # CHANGE THIS
Group=mygroup # CHANGE THIS
WorkingDirectory=/home/dockermgr/service # CHANGE THIS
ExecStart=/usr/local/bin/docker-compose up -d
ExecStop=/usr/local/bin/docker-compose down
TimeoutStartSec=0

[Install]
WantedBy=multi-user.target
```
