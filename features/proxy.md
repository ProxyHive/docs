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

## Switching a board's proxy off

Each board has a proxy toggle in the [Devices](/features/webinterface/devices) list.
Switched off, the board keeps working — it simply stops using its paid endpoint and
goes out over the appliance's own internet line instead.

**This also changes how the board resolves names.** While the proxy is on, the
appliance answers DNS itself and blocks the Google Play download servers: a board
should not spend your traffic budget pulling app packages through a paid residential
endpoint. With the proxy off that traffic no longer costs anything, so the board uses
your router's DNS and those downloads work normally.

That makes the toggle the way to update a board:

1. Switch the board's proxy **off**.
2. Let the Play Store finish its updates. This traffic runs over your own line and is
   not billed.
3. Switch the proxy back **on**.

> After switching back on, give the board a few minutes before judging it. Boards cache
> DNS answers for around four minutes, so a download can briefly continue over the paid
> endpoint — long enough for the traffic guard to
> park the board for a while. It releases itself; nothing is broken.

## Fair use

Endpoints carry **UNetwork traffic only**. Browsing, video, images, games and other
downloads over an endpoint are billed to you as traffic and, at scale, treated as abuse.
