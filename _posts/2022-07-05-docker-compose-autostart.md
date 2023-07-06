---
title: How to make a docker-compose application to autostart as a service?
excerpt_separator: <!--end_excerpt-->
---

In this tutorial we explain how to enable on-boot autostart for a docker-compose application using systemd on Ubuntu.

<!--end_excerpt-->

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
ExecStart=/usr/bin/docker compose up -d
ExecStop=/usr/bin/docker compose down
TimeoutStartSec=0

[Install]
WantedBy=multi-user.target
```

On some older systems, Docker Compose might be standalone. In this case, you should change two lines as:
```
ExecStart=/usr/local/bin/docker-compose up -d
ExecStop=/usr/local/bin/docker-compose down
```

To start the service use systemctl:
```
# Autostart systemd service
sudo systemctl enable docker-compose-example.service
# Start systemd service now
sudo systemctl start docker-compose-example.service
```
