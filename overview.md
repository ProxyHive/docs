---
title: Overview
sort: 10
---
ProxyHive is built around a self-hosted **Appliance**. The main capabilities:

## Appliance

- **Board discovery** — every phone connected over USB/OTG or found on the LAN is
  detected automatically. See [DHCP](/features/DHCP).
- **Residential proxy per board** — each board is routed through its own assigned
  residential endpoint. See [Proxy](/features/proxy).
- **APK management** — install, update and remove the earning app on any board
  directly from the appliance web interface. See [APK Install](/features/APK_Install).
- **Debloat** — remove unwanted vendor/bloatware apps from a board based on an APK
  whitelist. See [Debloat](/features/debloat).
- **Box control** — manage USB/OTG slots and fan control from the appliance
  settings. See [Box Control](/features/box_control).
- **Remote access** — the appliance web interface is reachable from anywhere via a
  Cloudflare tunnel, protected by an email login token.

## Board mirroring

- **In the browser** — no desktop app; the appliance web interface does it all.
- **Live mirror & control** — open a board and drive it with mouse and keyboard to
  activate its licence. See [ADB & board mirroring](/features/ADB).
- **Clipboard** — paste text from your computer straight onto the board.
- **Never exposed** — the ADB socket listens on the appliance's loopback only and is
  reachable exclusively through the logged-in web interface.
