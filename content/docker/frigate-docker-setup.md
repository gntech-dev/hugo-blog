---
title: "Deploying Frigate NVR with Docker: Full Setup Guide"
date: 2026-05-04T02:52:00-04:00
categories: ["Docker", "Frigate", "Tutorial"]
tags: ["frigate", "docker", "NVR", "cameras", "ai", "object-detection", "self-hosted"]
draft: false
author: "GnTech"
summary: "Step-by-step guide to deploying Frigate—an open-source NVR with real-time AI object detection—using Docker. Includes hardware tips, configuration, and securing your instance."
images: ["https://images.unsplash.com/photo-1490697431894-982bcfd0cd16?ixlib=rb-4.0.3&auto=format&fit=crop&w=1200&h=600&q=80"]
---

Frigate is a powerful, open-source NVR that uses AI object detection for reliable camera automation and security alerts. Here’s how to run it using Docker on your own hardware.

## Prerequisites
- Linux server (x86, ARM, or x86 with Coral TPU recommended)
- Docker and Docker Compose installed ([installation guide](https://docs.docker.com/get-docker/))
- At least one IP camera (RTSP, RTMP, or HTTP stream supported)
- SSD or fast storage for recordings

## 1. Create a Project Directory
```bash
mkdir -p ~/frigate && cd ~/frigate
```

## 2. Sample docker-compose.yml
Paste this into `docker-compose.yml`:

```yaml
version: '3.9'
services:
  frigate:
    container_name: frigate
    image: blakeblackshear/frigate:stable
    privileged: true  # Needed for hardware access (USB Coral, etc)
    shm_size: '512mb'
    devices:
      - /dev/bus/usb:/dev/bus/usb  # For USB Coral
    volumes:
      - ./config:/config
      - ./media:/media
      - /etc/localtime:/etc/localtime:ro
    ports:
      - "5000:5000"  # Web UI
      - "1935:1935"  # RTMP
    environment:
      - FRIGATE_RTSP_PASSWORD=yourCameraPassword
    restart: unless-stopped
```

## 3. Configure Frigate
Create a config file: `config/config.yml`

```yaml
mqtt:
  host: mqtt.example.com
  user: mqttuser
  password: mqttpass
cameras:
  cam1:
    ffmpeg:
      inputs:
        - path: rtsp://user:password@<CAMERA_IP>/h264
          roles:
            - detect
    detect:
      width: 1280
      height: 720
      fps: 5
record:
  enabled: True
```
Adjust to match your cameras and setup.

## 4. Start Frigate
```bash
docker-compose up -d
```
Access the UI at `http://your-server-ip:5000/`.

## 5. Hardware Acceleration (Optional)
- USB Coral (recommended for AI detection):
  - Plug in and Frigate auto-detects under `/dev/bus/usb`.
- For CPU-only systems, detection will be slower.

## 6. Securing & Maintaining Frigate
- Do not expose port 5000 to the public internet without protection.
- Set strong MQTT and camera passwords.
- Keep configs and media backed up.

## Resources
- [Frigate Docs](https://docs.frigate.video/)
- [Frigate GitHub](https://github.com/blakeblackshear/frigate)
- [Home Assistant Integration](https://www.home-assistant.io/integrations/frigate/)

Need more camera tips or automation guides? Let me know!