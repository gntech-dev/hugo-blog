---
title: "Deploying BookStack with Docker: Step-by-Step Guide"
date: 2026-05-04T02:48:00-04:00
categories: ["Docker", "BookStack", "Tutorial"]
tags: ["bookstack", "docker", "self-hosted", "how-to", "guide"]
draft: false
author: "GnTech"
summary: "Learn how to quickly deploy BookStack, a modern documentation platform, using Docker. Includes sample docker-compose, tips for first run, and securing your instance."
images: ["https://images.unsplash.com/photo-1515168833906-d2a3b82bce80?ixlib=rb-4.0.3&auto=format&fit=crop&w=1200&h=600&q=80"]
---

BookStack is an easy-to-use, open-source documentation platform that’s ideal for wikis, guides, and internal docs. This guide shows you how to get it running on your own server with Docker using docker-compose.

## Prerequisites
- Docker and Docker Compose installed ([installation guide](https://docs.docker.com/get-docker/))
- A domain name (optional, for HTTPS)
- At least 2GB RAM recommended

## 1. Create a Project Directory
```bash
mkdir -p ~/bookstack && cd ~/bookstack
```

## 2. Sample docker-compose.yml
Paste this into `docker-compose.yml`:

```yaml
version: '3.3'
services:
  bookstack:
    image: linuxserver/bookstack:latest
    container_name: bookstack
    environment:
      - PUID=1000
      - PGID=1000
      - DB_HOST=bookstack_db
      - DB_USER=bookstack
      - DB_PASS=supersecret
      - DB_DATABASE=bookstackapp
    volumes:
      - ./bookstack_data:/config
    ports:
      - 6875:80
    depends_on:
      - bookstack_db
    restart: unless-stopped

  bookstack_db:
    image: linuxserver/mariadb:latest
    container_name: bookstack_db
    environment:
      - PUID=1000
      - PGID=1000
      - MYSQL_ROOT_PASSWORD=mariadbrootpass
      - TZ=UTC
      - MYSQL_DATABASE=bookstackapp
      - MYSQL_USER=bookstack
      - MYSQL_PASSWORD=supersecret
    volumes:
      - ./db_data:/config
    restart: unless-stopped
```

## 3. Start the Stack
```bash
docker-compose up -d
```
Visit `http://your-server-ip:6875/` to complete setup. Default login is `admin@admin.com` / `password`. **Change these immediately.**

## 4. Securing BookStack
- Set up HTTPS using a reverse proxy (Traefik, Caddy, or Nginx).
- Restrict exposed ports.
- Change all default passwords and credentials.

## 5. Backup Tips
- Back up `bookstack_data` and `db_data` regularly.
- Test restores before running updates.

## Resources
- [BookStack Docs](https://www.bookstackapp.com/docs/)
- [BookStack DockerHub](https://hub.docker.com/r/linuxserver/bookstack)
- [Community Support](https://discord.gg/bookstackapp)

If you have questions or need advanced tweaks, let me know!