---
layout: page
title: Support
permalink: /support/
---

## Contact

- **Email:** <camwall@veerman.se> — usually answered within a few days.
- **Bugs and feature requests:** [GitHub Issues](https://github.com/Veeeriz/CamWall/issues/new/choose) (needs a GitHub account).
- **Guides and FAQ:** the [wiki](https://github.com/Veeeriz/CamWall/wiki).

When reporting a problem, include your Apple TV model, tvOS version, CamWall version, Frigate version and camera brands. **Never send passwords.**

## Trial and purchase

- **Free trial:** CamWall is free to try for 60 days with your own cameras. You start the trial yourself ("Start 60-Day Free Trial"). It costs nothing and never turns into a subscription.
- **Unlock:** after the trial, one purchase ("CamWall Unlock") keeps your cameras on the wall for good, including every 1.x update. The demo is always free.
- **Other Apple TVs and family:** the trial and the unlock belong to your Apple Account and are shared with your Family Sharing group. If an Apple TV doesn't show it, choose **Settings → Purchase → Restore Purchases**.
- **Reinstalling** doesn't restart the trial or lose the unlock.
- **Refunds** are handled by Apple: [reportaproblem.apple.com](https://reportaproblem.apple.com).
- **Ask to Buy:** a purchase waiting for a parent's approval unlocks once it's approved.

## Common questions

**A camera shows an error card or stays black.**
Check that Frigate's go2rtc restream is enabled for the camera (CamWall plays `rtsp://<frigate>:8554/<stream>`) and that the Apple TV can reach port 8554. Use the tile's quick actions (hold OK) to reconnect.

**Some cameras don't start playing on the wall.**
Each Apple TV model can decode only a limited number of streams at once, so CamWall caps how many autoplay. Use substreams for wall tiles, or turn the limit off in Settings.

**The timeline is empty for some cameras.**
Frigate only creates alerts and detections for cameras that record, so cameras with recording off have nothing to show in the timeline, even though their live detection banners work. Turn on recording for those cameras; [Getting started](../getting-started/) shows a setup that keeps only the footage around events.

**"Mark reviewed" is missing.**
On Frigate's port 5000 every user is anonymous, so review state can't be saved. Connect on port 8971 with a Frigate login.

**PTZ doesn't move my camera.**
Try switching the camera's PTZ setting between *Through Frigate* and *Direct*. Some cameras (e.g. Tapo) refuse direct ONVIF control and work through Frigate instead.

**Can I try CamWall without cameras?**
Yes — choose **Try the Demo** on first launch. The demo is always free.

**Does CamWall work away from home?**
Only if your Apple TV can reach your Frigate server, for example over a VPN. CamWall has no cloud relay.

More in [Getting started](../getting-started/) and the [wiki](https://github.com/Veeeriz/CamWall/wiki).
