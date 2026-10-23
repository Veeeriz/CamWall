---
layout: page
title: Getting started
permalink: /getting-started/
---

## 1. Prepare Frigate

- Enable **go2rtc restreaming** for each camera. CamWall plays the restream at `rtsp://<frigate>:8554/<stream name>`. The stream name is read from Frigate's config and does not have to match the camera name.
- Decide on a port:
  - **5000** — no login, but "mark reviewed" is unavailable.
  - **8971** — HTTPS with a Frigate login; everything works. Self-signed certificates are accepted once and then remembered.
- Turn on **recording** for every camera whose events you want in the timeline. Frigate only creates alerts and detections (review items) for cameras that record; live detection banners work either way. To keep only the footage around events, not continuous video:

  ```yaml
  record:
    enabled: true
    continuous:
      days: 0       # no continuous footage (older Frigate: retain: days: 0)
    alerts:
      retain:
        days: 7
    detections:
      retain:
        days: 3
  ```

## 2. Add your server

Open CamWall, enter your Frigate address, and CamWall discovers your cameras, their streams and channels.

Cameras without Frigate can be added directly with an RTSP address.

## 3. Optional

- **Substreams** for lighter wall tiles — taken from Frigate, ONVIF or the camera brand's paths.
- **PTZ** — set each camera to *Automatic*, *Through Frigate* or *Direct (ONVIF)*. Direct control needs the camera's ONVIF login, which is often different from its RTSP login.
- **MQTT** — for live events and PTZ when Frigate's WebSocket isn't available.

## Tips

- Older Apple TVs (e.g. the 2017 Apple TV 4K) handle about four full-quality streams at once. Use substreams on the wall.
- Hold OK on any tile for quick actions: fullscreen, reconnect, stop/start, main/substream, PTZ, arrange.
- Turn on **Stay Awake** to keep the wall on screen without the screensaver.
