---
Title: Debloat
---
Each board in the appliance device list has a **Debloat** action. Debloat removes
apps from the board that are **not on the APK whitelist**, cutting background
traffic and reducing the risk of policy violations.

FYI: The rules will be lifted after 2026-07-31 as we switch to a traffic paid system, you can then run whatever you want on the phones.

## Why debloat

Some devices ship with vendor software that generates traffic on its own — for
example bloatware installers that silently download sponsored apps. Traffic is
billed by the gigabyte, so that software spends your balance on downloads you never
asked for. The [traffic guard](/features/traffic_guard) catches the worst of it, but
removing the software is better than being protected from it.

Debloat helps you strip a board down to **UNetwork only**.

## How to use it

1. Open the appliance **device list**.
2. Select the board and choose **Debloat**.
3. The board is reduced to the apps on the [APK Whitelist](/rules/apk_whitelist);
   everything else is removed or disabled.

![The Debloat confirmation dialog on a board, warning that every non-system app not on the whitelist will be uninstalled.](/images/features/debloat-confirm.png)

> ⚠️ You are still responsible for the board. If your device ships bloatware that
> Debloat cannot fully remove, disable it manually before enabling the proxy —
> whatever it downloads is billed to you.
