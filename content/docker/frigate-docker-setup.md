---
title: "Deploying Frigate NVR with Docker: Comprehensive Guide (CPU, Coral, iGPU)"
date: 2026-05-04T02:55:00-04:00
categories: ["Docker", "Frigate", "Tutorial"]
tags: ["frigate", "docker", "NVR", "cameras", "ai", "object-detection", "hardware-acceleration", "intel", "igpu", "vaapi", "self-hosted"]
draft: false
author: "GnTech"
summary: "Definitive Frigate NVR setup guide for Docker: CPU-only, Google Coral, and Intel iGPU (VAAPI) acceleration. Includes docker-compose, detection tuning, troubleshooting, and security tips."
images: ["https://images.unsplash.com/photo-1490697431894-982bcfd0cd16?ixlib=rb-4.0.3&auto=format&fit=crop&w=1200&h=600&q=80"]
---

Frigate is an advanced open-source NVR with AI detection—fast, accurate, and highly tunable. Here’s how to deploy Frigate on Docker, covering CPU, Google Coral, and Intel iGPU (hardware acceleration) setups for best performance.

## Prerequisites
- Linux server (x86, ARM, or x86 with iGPU)
- Docker and Docker Compose ([install guide](https://docs.docker.com/get-docker/))
- At least one RTSP/RTMP/HTTP camera
- SSD/fast storage recommended

## 1. Create Project Directory
```bash
mkdir -p ~/frigate && cd ~/frigate
```

## 2. Sample docker-compose.yml
Start with this as `docker-compose.yml` (supports CPU, Coral, or Intel iGPU with config tweaks):

```yaml
version: '3.9'
services:
  frigate:
    container_name: frigate
    image: blakeblackshear/frigate:stable
    privileged: true
    shm_size: '512mb'
    environment:
      - FRIGATE_RTSP_PASSWORD=yourCameraPassword
    volumes:
      - ./config:/config
      - ./media:/media
      - /etc/localtime:/etc/localtime:ro
    ports:
      - "5000:5000" # Web UI
      - "1935:1935" # RTMP (optional)
    restart: unless-stopped
#    devices:
#      - /dev/bus/usb:/dev/bus/usb        # For USB Coral
#      - /dev/dri/renderD128:/dev/dri/renderD128 # For Intel iGPU
```

Uncomment only one of the devices sections below, per your hardware.

### For Google Coral TPU (USB/PCIe)
Uncomment/add:
```yaml
    devices:
      - /dev/bus/usb:/dev/bus/usb  # USB Coral
# For PCIe, add:
#      - /dev/apex_0:/dev/apex_0
```
Frigate will detect and use it automatically for AI detection.

### For Intel iGPU (Quick Sync, VAAPI/QSV)
1. Install drivers:
   ```bash
   sudo apt install -y intel-media-va-driver vainfo
   sudo usermod -aG video $(whoami)
   reboot   # Or log out/in for group changes
   ```
2. Add device to compose:
   ```yaml
    devices:
      - /dev/dri/renderD128:/dev/dri/renderD128
   ```
3. Set Frigate config for hwaccel

## 3. Create Frigate Config
Place at `config/config.yml`. Example for iGPU (VAAPI):
```yaml
detect:
  hwaccel_args: preset-vaapi
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

See [Frigate docs](https://docs.frigate.video/configuration/hardware-acceleration/) for Coral, QSV, and VAAPI.

### CPU-Only? No hardware setup needed—leave `devices:` blank and omit `hwaccel_args` for CPU detection (least efficient).

## 4. Start Frigate
```bash
docker-compose up -d
```
Access UI: `http://your-server-ip:5000/`

## 5. Performance & Troubleshooting
- Check Frigate logs (`docker logs frigate`) for hardware detection.
- Use `vainfo` on host to verify iGPU detection (if using VAAPI).
- For Coral: check `dmesg | grep coral`.
- Got “no decoder surfaces” or “Not a supported Intel GPU”? Make sure your processor supports Quick Sync (6th gen+ Intel Core recommended).

## 6. Security Checklist
- NEVER expose port 5000 to the internet.
- Use strong passwords and separate VLANs for cameras.
- Backup configs/media.

## Resources
- [Frigate Docs](https://docs.frigate.video/)
- [Hardware Acceleration Tips](https://docs.frigate.video/configuration/hardware-acceleration/)
- [Recommended Cameras](https://docs.frigate.video/hardware/cameras/)
- [Home Assistant Integration](https://www.home-assistant.io/integrations/frigate/)

Questions, HW issues, or want automation recipes? Just ask!