# Getting Started

The full guide is on the website: <https://veeeriz.github.io/CamWall/getting-started/>

## Checklist

1. Apple TV on tvOS 17 or later.
2. Frigate with **go2rtc restreaming** enabled for each camera (port 8554 reachable from the Apple TV).
3. Pick a Frigate port: **5000** (no login, no "mark reviewed") or **8971** (login, everything works).
4. Enter the Frigate address in CamWall — cameras are discovered automatically.
5. Optional: substreams, PTZ (Automatic / Through Frigate / Direct ONVIF), MQTT.

## Three different logins

| Login | Used for |
|---|---|
| Frigate user | API, events, review state (port 8971) |
| Camera RTSP login | Direct RTSP cameras without Frigate |
| Camera ONVIF login | Direct PTZ and ONVIF substream detection |
