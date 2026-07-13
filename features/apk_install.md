# APK Install

You manage the earning app on each board directly from the **appliance web
interface** — install, update and remove APKs from the device list.

> ⚠️ APK installs run through the appliance web interface, **never through the
> proxy tunnel** or over your endpoints' traffic.

## Typical flow

1. Open the appliance device list.
2. For each board, remove the legacy ProxyHive Agent and the Unity app.
3. Install **UNetwork**.
4. Assign an endpoint and use the [Farmer app](/features/adb) to activate the
   license.

## Whitelist

Installable apps are governed by an **APK whitelist**. The same whitelist drives
the [Debloat](/features/debloat) function, which removes apps that are not on it.
See [APK Whitelist](/rules/apk_whitelist).

> 📷 **Screenshot:** _The appliance device list with the APK install / remove actions._
