---
title: Choosing hardware
sort: 15
---

## Choosing hardware

This page gives **requirements, not shopping links**. A product listing is out of stock or
replaced by a different revision within months, and a recommendation that has quietly rotted is
worse than none — you would buy it in good faith. Chipsets, port counts and interface rules stay
true for years, and they work on whichever Amazon you actually buy from.

So: match the specification, search your local shop for it, and use the known-good parts named
here as a reference point rather than a shopping list.

# Answer these two questions first

Everything else follows from them.

**1. How do the boards reach the appliance — cable or WiFi?**

Some boxes have a LAN port; some do not, and their boards join over WiFi. Standalone phones have
no LAN either.

| Your situation | What the appliance needs |
|---|---|
| Boxes have LAN | **two LAN ports** — one for your network, one for the boards |
| Boards over WiFi, uplink by cable | one LAN port and a **good WiFi adapter** for the boards |
| Uplink over WiFi, boards by cable | a WiFi adapter for the uplink and **one LAN port** for the boards |

Two LAN ports is the best default. It is the simplest to reason about, the least to go wrong, and
it leaves the radio free.

**2. How are the boxes managed over USB before the boards switch to OTG?**

Box control runs over USB (a CH340 serial channel per box). If the appliance is to do that
itself, it needs enough USB *controllers* — see below. If a separate machine handles it, the
appliance does not.

This one question decides whether you need a PCIe controller card at all.

# The appliance

**Operating system:** Debian 13 (Trixie), installed from the netinstall image. Take
`openssh-server` and the standard system utilities; **leave the desktop out**. A GNOME
installation on an appliance is a few gigabytes of software that nobody will ever look at, and
every one of those packages is something to keep updated.

**No GPU is needed.** Nothing here renders anything.

**CPU:** not critical. A Ryzen mini PC, an Intel N95 box, a Raspberry Pi 5 — all of them work.
Cores matter more than clock speed once you get past a few boxes.

**Storage: fast local storage, and not a cheap SD card.** It does not have to be NVMe; a decent
SATA SSD or eMMC is fine. What kills appliances is a slow or worn card, and they wear out because
the agent writes state continuously. Budget at least 32 GB — container images account for most of
it, and old ones accumulate between updates.

**Sizing, measured rather than estimated.** A Raspberry Pi 5 with 8 GB running 40 boards:

| | |
|---|---|
| Memory in use | 730 MB of 7.9 GB |
| Load average | 0.62 across four cores |
| Agent CPU | 23% of one core |
| Everything else | under 1% |

That is roughly 18 MB of memory per board on top of a small base, and the agent's work scales with
the number of boards. Extrapolating to a full appliance of ten boxes:

- **4 GB of RAM is enough**, 8 GB is comfortable and cheap
- **four cores** is the sensible floor — one core would be saturated by the agent alone

# USB controllers, if the appliance manages the boxes

This is the one place where the obvious purchase is the wrong one.

**Go by controller count and PCIe lanes, never by port count.** A card advertising 7, 10 or 19
ports on PCIe x1 is a *single* USB host controller with hub chips fanning out behind it. The
physics is not subtle: a PCIe x1 link carries about 8 Gbit/s and one USB 3 controller alone wants
5 of them. Seven real controllers never fit there.

What you are looking for is the phrase **"independent"** or **"dedicated controllers"**, on a
**PCIe x4** card. Known good, and what we run: **StarTech PEXUSB3S44V** — four separate
controllers, four ports, one host per port.

**Rule of thumb: one controller per box.** Eight or ten boxes on one appliance therefore means
two of those cards, and a mini PC with the slots to take them.

A trap worth naming because it looks like a bargain: multi-port "all-in-one" kits for the
Raspberry Pi 5. The Pi 5 has exactly one PCIe 2.0 x1 lane, so a "4-channel USB 3.2" adapter board
is one VL805 controller behind a hub — and there is no second lane to add a proper card to later.
For USB-managed boxes at any density, that is a dead end.

# WiFi, if boards join over the air

**The Pi's onboard radio tops out at about 20 clients.** That is a firmware limit, not a
configuration one — no setting raises it. Forty boards on WiFi therefore need either a second
radio or a proper access point.

| Boards on WiFi | What works |
|---|---|
| Up to ~50 | a good USB WiFi adapter dedicated to the boards |
| 300+ (say 15 boxes) | a real access point in bridge mode, rated for that many clients |

Note the number an access point is actually rated for. Consumer units advertise a client count
they cannot sustain; look for the figure in the specification sheet, not on the box.

**If you run two radios, name them properly.** The kernel hands out `wlan0` and `wlan1` in probe
order, and that order is a race: on our own appliance the same dongle came up as `wlan0` after one
reboot and `wlan1` after the next, with nothing changed. Whatever is tied to the name then swaps
role — the uplink lands on the wrong band, or the access point lands on the onboard radio with
its 20-client limit, which is precisely the limit the second radio was bought to escape.

The fix is to take USB radios out of the `wlanN` namespace with a udev rule, so they keep a stable
name like `wlx7cdd90909627`. Our own appliance does exactly that.

# Limits you cannot design around

- **241 addresses per appliance, hard.** Every board gets one, and so does every tunnel.
- **200 addresses is the soft limit.** Nothing enforces it; treat it as the line beyond which you
  are on your own.
- **Ten boxes per appliance.** Past that, split the load across a second one — it is cheaper than
  the failure modes.

# Switches

Nothing special is required. Enough ports for the boxes, gigabit, and an unmanaged switch is
perfectly adequate — the boards produce little traffic each and none of the ProxyHive setup needs
VLANs or managed features.

# In short

| You need | Look for |
|---|---|
| Appliance | Debian 13 netinstall, no desktop, 4+ cores, 4–8 GB, SSD or eMMC, ideally 2 LAN ports |
| USB card | "4 independent controllers", PCIe **x4** — one controller per box |
| WiFi for boards | dedicated adapter up to ~50 boards, a rated access point in bridge mode beyond |
| Switch | unmanaged gigabit, enough ports |

If you are unsure which of the two layouts applies to you, ask in the group before ordering. The
cost of the wrong card is a week and a return; the cost of asking is a message.
