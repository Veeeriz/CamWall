# CamWall — handoff for a new session

_Last updated 2026-10-22_

Paste this file into the new session together with your request. Select **`Veeeriz/CamWall`** as the session's repository.

---

## Context

- **CamWall** is a native tvOS app for Frigate NVR and RTSP cameras. It has a camera wall, a timeline of Frigate's events, clip playback and PTZ control. The name is a working title.
- **App source:** only on the Mac at `~/Xcode Projects/CamWall`. It is not on GitHub. The project is `CamWallApp/CamWallApp.xcodeproj`, scheme `CamWallApp`, bundle ID `dev.camwall.app`, team `HCY894W8W9`.
- **Public repo `Veeeriz/CamWall`** (moved from `veeriz/CamWall`). It holds documentation, the privacy policy and the issue tracker only.
- **Background notes in Notion:** the "tvOS Multi-Cam Viewer (Frigate)" page and its sub-page "Remote Deployment — Apple TV at friend's site".
- **Support email:** camwall@veerman.se
- **Business model:** free download, a 60–90 day trial, then a one-time purchase. StoreKit isn't built yet.

## Done

Branch `claude/camwallapp-github-appstore-l3rdu1` is pushed to `Veeeriz/CamWall`, **not merged**:

- `c4bbe03`: the website, privacy policy, support pages, wiki source and issue forms
- `8edd7f1`: links point to `Veeeriz/CamWall` and `veeeriz.github.io/CamWall`

What's in the repo:

| Path | Purpose |
|---|---|
| `docs/` | GitHub Pages site: `index.md`, `privacy.md`, `support.md`, `getting-started.md`, `acknowledgements.md`, `_config.yml` (minima theme) |
| `wiki/` | Wiki source: Home, Getting-Started, FAQ, Troubleshooting, Privacy-Policy (links to the site), Contact, `_Sidebar` |
| `.github/ISSUE_TEMPLATE/` | Bug report and feature request forms; blank issues off; an email contact link |
| `README.md`, `SUPPORT.md` | Repo landing page and help page |

The Claude GitHub App is installed on the Veeeriz org with access to CamWall only.

## To do

### On GitHub (you)
- [ ] Open a PR from `claude/camwallapp-github-appstore-l3rdu1` into `main` and merge it. The new session can open the PR if you ask.
- [ ] Make the repo **public**.
- [ ] Turn on Pages: Settings → Pages → Deploy from branch → `main`, folder `/docs`.
- [ ] Wiki: create any page once in the browser. GitHub only creates the wiki git repo after that.
- [ ] Optional: a custom domain, e.g. `camwall.veerman.se` or `camwall.dev`, so the URLs survive another move. It takes a `docs/CNAME` file and one DNS record.

### For Claude in the new session
- [ ] Open and merge the PR if you ask.
- [ ] Push `wiki/*.md` to `https://github.com/Veeeriz/CamWall.wiki.git` once the wiki exists. GitHub turns `Getting-Started.md` into the page "Getting Started".
- [ ] Check that the Pages URLs return 200 once they're live.
- [ ] Log it in Notion under the CamWall page: the URLs, the App Store checklist, the name-check result and the timeline finding.

### URLs for App Store Connect (once Pages is live)
- Privacy Policy: `https://veeeriz.github.io/CamWall/privacy/`
- Support: `https://veeeriz.github.io/CamWall/support/`

## App Store release checklist

| # | Item | Status |
|---|---|---|
| 1 | Privacy Policy URL | Page written; waiting on Pages |
| 2 | Support URL, with the email address on the page | Page written; waiting on Pages |
| 3 | App Privacy label: **Data Not Collected** | To set in App Store Connect |
| 4 | `PrivacyInfo.xcprivacy`: UserDefaults with reason `CA92.1`, plus any other required-reason APIs used by the app or VLCKit | To add in Xcode |
| 5 | `ITSAppUsesNonExemptEncryption = NO` in Info.plist (standard TLS only) | To add |
| 6 | Review notes: reviewers have no Frigate server, so tell them to use **Demo mode** | To write |
| 7 | Trial: a free non-consumable in-app purchase ("90-Day Trial"), the paid unlock, and a **Restore Purchases** button | To build |
| 8 | VLCKit LGPL-2.1 credit, in Help & About and on the website (the website page is done) | Credit in the app still to do |
| 9 | EU trader status (DSA). A trader's address, phone and email are shown publicly | To decide |
| 10 | Assets: tvOS screenshots (1920×1080 or 3840×2160), layered icon, Top Shelf image, age-rating questionnaire | To do |
| 11 | TestFlight build | To do |
| 12 | Final app name (see below) | **Decision needed** |

## Name check: "CamWall"

- **Apple App Store:** no app called CamWall found.
- **Amazon Appstore:** **"CamWall: IP Camera Viewer — RTSP & ONVIF"** already exists for Fire TV. Same kind of app on the same kind of device, so it's the main risk.
- **Others with the name:** an unreleased Flutter project (`welingtonfidelis/camwall_app`) and a desktop wallpaper tool (camwall.gitcoder.me).
- **Trademarks:** none found in web search. Still to do: search EUIPO and USPTO, and try to reserve the name in App Store Connect.
- **Options:** (A) keep the CamWall brand with a qualifier, e.g. "CamWall for Frigate" (recommended); (B) rename before any assets exist; (C) keep plain "CamWall".

## Open bug: the timeline is empty at the friend's (Tompa's) site

- **Symptom:** live alert pop-ups work, but the timeline shows nothing.
- **Cause found:** Frigate only creates review items for cameras that record. In `frigate/review/maintainer.py`, cameras with `record.enabled: false` are skipped. At Tompa's site only `Corridor` records; the other six cameras have recording off. The MQTT topics haven't changed, and the timeline reads from the web API, not MQTT.
- **Next steps:**
  1. Open `http://<frigate>:5000/api/review?cameras=Corridor&limit=5`. If it returns items, the app has a bug, which needs the app source. If it's empty, check Corridor's `review.alerts` / `review.detections` settings and labels.
  2. For the other cameras: `record: enabled: true` with `retain: days: 0`, keeping only the clips around alerts and detections for a few days.
  3. Optionally, have the app say "Recording is off for this camera" instead of showing an empty track. This needs the app source in the session.
