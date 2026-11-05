---
layout: page
title: Getting started
permalink: /getting-started/
---

# Set up CamWall on Apple TV

Open CamWall and choose **Try the Demo** to explore the wall with sample cameras. To use your own cameras, connect to Frigate or add a standalone RTSP stream. Start with one camera and confirm playback before filling the wall.

## Option 1 · Frigate

1. Make sure the Apple TV can reach your Frigate server and its go2rtc RTSP port. In Frigate, configure a go2rtc restream for your camera and check that it plays. See [Frigate's restream guide](https://docs.frigate.video/configuration/restream/).
2. On the CamWall welcome screen, enter the Frigate host or IP. Use the host reachable from the Apple TV, rather than a Docker-only hostname or the loopback address inside Frigate.
3. For a standard Frigate installation with TLS, enable **Use HTTPS (port 8971)** and enter your Frigate username and password. If you use a self-signed certificate, allow it only for your own server after checking the address. For an existing trusted internal HTTP setup, use the mapped port for Frigate's unauthenticated API (default **5000**) and an IP address or a `.local` name. Keep the unauthenticated endpoint private. [Frigate authentication and ports](https://docs.frigate.video/configuration/authentication/)
4. Leave **go2rtc RTSP port** at **8554** unless your host maps it differently. If Frigate is a Home Assistant app, you may need to enable this port in its network settings. [Frigate go2rtc troubleshooting](https://docs.frigate.video/troubleshooting/go2rtc/)
5. Select **Connect & Discover Cameras**. Open a camera on the wall and confirm live video. Use a Frigate login to save **Mark reviewed** state.

### Example configurations to start with

| Setup | What to enter or test |
| --- | --- |
| Frigate with TLS on the LAN | Your Frigate host, HTTPS enabled, API port `8971`, Frigate login, RTSP port `8554`. |
| Frigate on a trusted internal HTTP network | Your Frigate IP or `.local` host, API port `5000` if already reachable, RTSP port `8554`. Review state is unavailable on the anonymous connection. |
| Standalone RTSP camera | Start with a single H.264 stream and the RTSP path supplied by your camera vendor. Add the substream after the main stream plays. |

These examples use default ports and illustrative settings. A specific camera, firmware, codec or simultaneous stream count still needs testing on your hardware.

A minimal go2rtc entry for an existing Frigate setup looks like this. Replace the example addresses and paths with your camera's values. Merge this into your existing config rather than replacing it.

```yaml
go2rtc:
  streams:
    front_door:
      - rtsp://192.0.2.10:554/main
    front_door_sub:
      - rtsp://192.0.2.10:554/sub
```

From a device on the same network as the Apple TV, try opening `rtsp://<frigate-host>:8554/front_door` in an RTSP-capable player. The final path is the **go2rtc stream name**. Ensure Frigate's camera configuration uses the intended stream if the camera key and stream name differ.

## Option 2 · Standalone RTSP

1. On the welcome screen choose **Skip for now**. If you are in the demo, open **Settings → Exit Demo and Set Up My Cameras** first.
2. Go to **Settings → Cameras → Add Camera** and enter the camera's main RTSP URL. Use the manufacturer's path and any credentials the camera requires.
3. Save and test the camera on the wall. Add a lower-resolution substream for wall tiles if the camera provides one.

A standalone stream supplies live video. Frigate recordings and review items require a Frigate connection.

## Troubleshooting and gaps

| Symptom or question | What to check |
| --- | --- |
| Discovery fails | Check the host, API port, TLS and login. If the Apple TV is on a guest network or another VLAN, check whether it can reach Frigate. |
| Discovery works but the tile is black | Test the go2rtc RTSP stream separately. Check the RTSP port mapping and the stream name, then hold OK on the tile and choose **Reconnect**. |
| Some tiles do not autoplay | Start with fewer live streams and use substreams on the wall. Capacity depends on the Apple TV model, resolution, codec and frame rate. |
| The timeline is empty | Check recording for that camera in Frigate and verify that recordings and review items exist in Frigate itself. A live tile can play without any recordings. |
| Mark reviewed is missing | Connect through the authenticated Frigate API and run discovery again. |
| PTZ fails | Try **Through Frigate** if PTZ already works there. **Direct (ONVIF)** needs the camera's ONVIF credentials and network access. |
| Can I view cameras while away? | The Apple TV needs a route to your server or cameras, such as a VPN. CamWall has no cloud relay. |
| Can alerts appear over other Apple TV apps? | CamWall's tvOS alerts appear inside CamWall. |

For event-only recording, check the [Frigate recording documentation](https://docs.frigate.video/configuration/record/) for the syntax supported by your version. MQTT is optional for basic live viewing.

## Get help

For setup or purchase help, use the [support page](https://veeeriz.github.io/CamWall/support/). For a reproducible bug, use the [public issue form](https://github.com/Veeeriz/CamWall/issues/new/choose). Include your Apple TV model, tvOS and CamWall versions, Frigate version if applicable, and the steps that reproduce the problem. Remove credentials, tokens, camera addresses and private footage before sharing details.
