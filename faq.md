---
title: FAQ
sort: 20
---

# FAQ

## Why did Unitynodes stop working?

Unitynodes 1.1.5 was discontinued on **15 July 2026**. It was driven by the
legacy ProxyHive Agent. ProxyHive can no longer support Unitynodes, so the
platform has moved to **UNetwork**, running on the ProxyHive Appliance.

## Do I need new hardware?

Yes. UNetwork does not build uptime with a local software agent providing the
proxy, so a dedicated **ProxyHive Appliance** is required. See the
[Requirements](/getting_started/requirements).

## Which devices can I use?

Only headless Android boards or unused physical phones dedicated to farming.
ProxyHive is **not** for private phones, phones with a SIM card, or personal use.
See the [Rules](/rules/fair_use).

## Can I run the appliance on something other than a Raspberry Pi?

Yes. The appliance images are multi-architecture. You can run it on a Raspberry Pi
5 (arm64) or on an x86 mini-PC/server (amd64). See
[Architectures](/getting_started/architectures).

## How do I connect to my boards?

Through the **ProxyHive Farmer** desktop app. Log in with your ProxyHive account,
select your appliance, and you will see all its boards.

## Will endpoint prices change?

Endpoint pricing is expected to change as UNetwork traffic grows. Any change
applies to renewals and new endpoints and is announced in advance in the
dashboard.

## Can I connect more than one box to the appliance?

Yes. Connect a simple **unmanaged Gigabit switch** to the appliance's LAN port
and attach your boxes to that switch. The appliance serves DHCP to every board
through the switch. See [LAN](/networking/LAN).

## Can I connect both my router and my boxes to the LAN port through a switch?

No — never bridge your home router and the boards onto the appliance's LAN port.
Doing so puts **two DHCP servers** on the same network, both trying to lease
addresses to the boards *and* your home devices. It will disrupt your home LAN
for hours. Keep the appliance's LAN segment isolated to the boards only.

## Can I connect my phones over Wi-Fi?

No. Every box **must** be connected to a physical network port on the appliance.
Only the **WAN uplink** to your home router may use Wi-Fi. See
[WAN](/networking/WAN).

## Can I use an appliance with two physical LAN ports?

Yes. Instead of a Wi-Fi uplink you can use a second wired NIC for the WAN — one
NIC connected to the boards (LAN) and one to your home router (WAN).

## Can I reach my box when I am away from home?

Yes. Each box receives a public address and an FQDN, so you can reach your
appliance from anywhere in the world **without opening any ports on your
firewall**. Sign-in is only possible with the e-mail address bound to the
ProxyHive account that owns the box. See [Remote management](/networking/management).

## Can ProxyHive access my box?

Only with your consent. In the rare cases where you request support, ProxyHive
staff may access the box **with your explicit consent** to help resolve the
issue. There is no unattended access.

## Is the ADB interface secured?

Yes. The ADB socket is never exposed openly. Reaching the ADB ports of your box
requires a login that issues a **short-lived token** scoped to that box. See
[ADB](/features/ADB).
