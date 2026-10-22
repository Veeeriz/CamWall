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
