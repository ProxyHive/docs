---
title: Overview
sort: 10
---

# Overview

ProxyHive is built around a self-hosted **Appliance** and a companion **Farmer**
desktop app. The main capabilities:

## Appliance

- **Board discovery** — every phone connected over USB/OTG or found on the LAN is
  detected automatically. See [DHCP](/features/dhcp).
- **Residential proxy per board** — each board is routed through its own assigned
  residential endpoint. See [Proxy](/features/proxy).
- **APK management** — install, update and remove the earning app on any board
  directly from the appliance web interface. See [APK Install](/features/apk_install).
- **Debloat** — remove unwanted vendor/bloatware apps from a board based on an APK
  whitelist. See [Debloat](/features/debloat).
- **Box control** — manage USB/OTG slots and fan control from the appliance
  settings. See [Box Control](/features/box_control).
- **Remote access** — the appliance web interface is reachable from anywhere via a
  Cloudflare tunnel, protected by an email login token.

## Farmer app

- **Multi-platform** — Windows, macOS (Intel & Apple Silicon) and Linux (x86_64 &
  arm64).
- **Board grid** — every board as a card with a live screenshot and its label.
- **Live mirror & control** — open a board and drive it to configure the license.
- **Account-gated** — the ADB tunnel is only reachable by the Farmer app with your
  account's service token; the ADB socket is never exposed openly.

![The ProxyHive Farmer app showing the board grid with live screenshots of several boards, one board opened in the mirror view running UNetwork.](/images/welcome/farmer-board-grid.jpg)
