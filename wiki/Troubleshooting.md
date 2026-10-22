# Troubleshooting

| Symptom | Try |
|---|---|
| Error card or black tile | Enable go2rtc restream for the camera; check port 8554 is reachable; hold OK → Reconnect. |
| Cameras don't autoplay | You've hit the stream limit for your Apple TV model. Use substreams or turn the limit off. |
| App slows down or quits with many cameras | Use substreams on the wall; older models handle about four full streams. |
| "Mark reviewed" missing | Connect on port 8971 with a Frigate login. |
| PTZ fails ("Authority failure") | Set the camera's PTZ to *Through Frigate*. |
| Substream shows the wrong camera | Dual-lens cameras use channels; pick the substream for the right channel. |
| Certificate warning | Expected for self-signed Frigate certificates on port 8971; accept once. |

Still stuck? See [[Contact]].
