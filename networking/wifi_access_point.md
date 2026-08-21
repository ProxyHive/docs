---
title: Wi-Fi for boards — use an access point
sort: 30
---

## Wi-Fi for boards — use an access point

If your boards connect over Wi-Fi, use a **dedicated access point** on the board network
instead of a USB Wi-Fi dongle in the appliance. A dongle works for a handful of boards and
then stops — silently.

### Why not a USB dongle

USB Wi-Fi adapters are built to be a *client*, not an access point. Running one as an AP
works, but every chipset has a limit on how many devices it will accept, and that limit is
usually far lower than a rack of boards.

The commonly recommended MediaTek MT7921 adapters (BrosTrend AX9L / AXE3000, ALFA AWUS036AXML
and others) stop accepting new clients at around a dozen. Boards beyond that simply never
connect. There is no error on the board — it keeps retrying forever. In the appliance log it
looks like this:

```
STA a0:c9:a0:a7:26:96 IEEE 802.11: Could not add STA to kernel driver
```

The limit lives in the adapter's firmware. It cannot be raised by configuration, and no
setting in the appliance changes it.

**Do not try to solve this with a second dongle.** Two adapters broadcasting the same network
name do not double your capacity: a board picks whichever it hears best, and if that one is
full it is refused — it does not move to the other one.

### What an access point does instead

A proper access point is designed for many clients at once, has real antennas, and handles
dozens of boards without complaint. Used in **Access Point mode** it does not create its own
network — it passes traffic straight through to the appliance, which keeps handing out
addresses and routing every board through its endpoint exactly as before.

Any access point will do. The TP-Link Deco M4R is a common and inexpensive choice, and the
steps below use it as the example.

### Setting up a TP-Link Deco M4R

The Deco must be set up normally first — Access Point mode is a setting you change
afterwards, not an installation option.

1. Power the Deco and set it up through the **Deco app** as you normally would.
2. Update the firmware: **More → System → Update Deco**.
3. Go to **More → Advanced → Operation Mode**.
4. Choose **Access Point** and tap **Save**.
5. Confirm the reboot. After about two minutes the LED turns solid green — the Deco is now
   an access point.

The network name and password you set during setup stay the same. Your boards use those,
not the appliance's own Wi-Fi settings.

### Where to plug it in

The access point belongs on the **board network**, never on the internet side.

**Directly at the appliance** — connect the Deco's Ethernet port to the appliance's
[LAN](/networking/LAN) port.

**Or on the same switch as your farm boxes** — if your boards already run over a switch on
the LAN port, plug the access point into that switch. Wired boxes and Wi-Fi boards share one
network and one DHCP server, and it makes no difference which way a board arrives:

```
Appliance  ──[WAN]── your router / internet
           └─[LAN]── switch ─┬─ farm box 1
                             ├─ farm box 2
                             └─ access point ))) Wi-Fi boards
```

Both ways are equivalent. Use the switch whenever you have more than one thing to connect,
which is the normal case.

### Switching off the appliance's own Wi-Fi

Once the access point serves your boards, the appliance no longer needs a Wi-Fi interface of
its own. In `/opt/proxyhive/.env`, leave only the wired interface in `LAN_IF`:

```
LAN_IF=enp2s0
```

Reboot the appliance afterwards. See [configuration](/getting_started/configuration) for
details on this file.

### Things to watch

**Same network, not a new one.** In Access Point mode the Deco must not run its own DHCP.
The setting above takes care of that; if boards come up with addresses outside your board
range, the Deco is still in Router mode.

**One network name.** Do not run the access point *and* the appliance's own Wi-Fi with
different names at the same time — boards will settle on whichever they find first and you
lose track of where each one is.

**Wireless debugging** must be enabled on every board that connects over Wi-Fi, the same as
with any other Wi-Fi setup. See [ADB](/features/ADB).
