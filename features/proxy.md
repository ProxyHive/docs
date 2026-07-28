---
Title: Proxy
---
Every board runs behind its own **residential proxy endpoint**. The board's
outbound traffic exits through a residential IP, never through the appliance's
own WAN address.

## How it works

- You request **endpoints** in the dashboard and **assign** one to each board.
- The appliance provides each board with its endpoint's credentials and
  routes only that board's traffic through it.
- The board's exit IP is a **residential** address, verified by the platform.

![A board in the device list showing its assigned residential proxy country and exit IP (redacted here).](/images/features/device-proxy-ip.png)

## Health

A board's proxy is considered healthy when it is present on the box and reporting
a live residential exit IP. You can see the proxy status per board in the
[Devices](/features/webinterface/devices) list.

## Fair use (This will end 2026-08-01, we switch to a traffic based system)

Endpoints must carry **UNetwork traffic only**. Browsing, video, images, games and
downloads over an endpoint are detected and lead to a permanent ban. See
[Traffic Usage](/rules/traffic_usage).
