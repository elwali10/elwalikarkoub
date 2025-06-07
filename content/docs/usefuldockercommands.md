---
date: '2025-06-07T18:35:36+01:00'
draft: false
title: 'My Essential Docker Commands Cheat Sheet'
categories:
  - DevOps
tags:
  - Docker
  - Devops
  - Linux
---

Docker commands I use regularly: 

## 1. Complete Environment Cleanup
```bash
docker-compose down --remove-orphans -v --rmi all
```

 - `--remove-orphans`: Deletes containers for services not in compose file

 - `-v`: Removes attached volumes

 - `--rmi all`: Deletes all images used by services


## 2. Run Image with Interactive Shell

```
docker run -it --entrypoint bash wazuh/wazuh-certs-generator:0.0.1

docker run -it --entrypoint bash ubuntu:focal
```

 - `-it`: Interactive terminal

 - `--entrypoint bash`: Overrides default to give shell access


## 3. Find Container IP Address

```
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' $(docker ps | grep -i dashboard | awk '{print $1}')
```

 - `docker ps | grep -i dashboard`: Finds container with "dashboard" in name

 - `awk '{print $1}'`: Extracts container ID

 - `docker inspect -f`: Formats output with Go template

 - Template extracts just the IP address

## 4. Build Custom Image

```
docker build -t wazuh-dashboard-anomaly-detector:4.7.1 wazuh-dashboard/. --no-cache
```

 - `--no-cache` ensures fresh build

## 5. Tag Image for Docker Hub

```
docker tag wazuh-dashboard-anomaly-detector:4.7.1 elwali/wazuh-dashboard-anomaly-detector:4.7.1
```

 - `username/repository:version` required before pushing to any registry.

## 6. Push Image to Docker Hub

```
docker push elwali/wazuh-dashboard-anomaly-detector:4.7.1
```

Make sure to meet the following requirements: 

 - Must be logged in (docker login)

 - Proper permissions on repository

 - Correctly tagged image

## 7. System Cleanup

```
docker system prune
```
It removes: 

 - Stopped containers

 - Dangling images

 - Unused networks

 - Build cache

More aggressive cleanup: 

```
docker system prune -a --volumes
```
 - Removes all unused images and volumes

