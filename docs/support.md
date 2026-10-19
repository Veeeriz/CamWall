---
layout: page
title: Support
permalink: /support/
---

## Contact

- **Email:** <camwall@veerman.se> — usually answered within a few days.
- **Bugs and feature requests:** [GitHub Issues](https://github.com/veeriz/CamWall/issues/new/choose) (needs a GitHub account).
- **Guides and FAQ:** the [wiki](https://github.com/veeriz/CamWall/wiki).

When reporting a problem, include your Apple TV model, tvOS version, CamWall version, Frigate version and camera brands. **Never send passwords.**

## Common questions

**A camera shows an error card or stays black.**
Check that Frigate's go2rtc restream is enabled for the camera (CamWall plays `rtsp://<frigate>:8554/<stream>`) and that the Apple TV can reach port 8554. Use the tile's quick actions (hold OK) to reconnect.

**Some cameras don't start playing on the wall.**
Each Apple TV model can decode only a limited number of streams at once, so CamWall caps how many autoplay. Use substreams for wall tiles, or turn the limit off in Settings.

**"Mark reviewed" is missing.**
On Frigate's port 5000 every user is anonymous, so review state can't be saved. Connect on port 8971 with a Frigate login.

**PTZ doesn't move my camera.**
Try switching the camera's PTZ setting between *Through Frigate* and *Direct*. Some cameras (e.g. Tapo) refuse direct ONVIF control and work through Frigate instead.

**Can I try CamWall without cameras?**
Yes — choose Demo mode on first launch.

**Does CamWall work away from home?**
Only if your Apple TV can reach your Frigate server, for example over a VPN. CamWall has no cloud relay.

More in [Getting started](../getting-started/) and the [wiki](https://github.com/veeriz/CamWall/wiki).
