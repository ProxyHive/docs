---
Title: WAN
---
The **WAN** interface is the appliance's uplink to the internet. It carries the
proxied board traffic out to the residential endpoints.

- The WAN port may be **Wi-Fi or a wired NIC**.
- On a **Raspberry Pi 5** the default WAN interface is **`wlan0`** (Wi-Fi).
- On other hardware, set your own interface name in the
  [box configurator](/getting_started/configuration) — for example `eth1`,
  `wlan0` or `enp2s0`.

![The box configurator with the WAN interface field, which may be a Wi-Fi or wired NIC uplink.](/images/getting-started/box-configurator.png)

The WAN address is the appliance's own public IP. Board traffic does **not** exit
through it — each board exits through its assigned residential
[endpoint](/features/webinterface/endpoints).
