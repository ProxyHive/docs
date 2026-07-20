---
Title: LAN
---
The **LAN** interface connects the appliance to the boards. The appliance owns this
segment, runs [DHCP](/features/DHCP) on it, and routes each board through its
assigned endpoint.

- The LAN port can be a wired NIC or Wi-Fi / Dongle like ALFA AWUS036ACM (MT7612U) for the boards
  network.
- If you use WLAN for the LAN interface, do NOT use the onboard wlan0 broadcom chip, it cant handle the devices, use a dongle.

If you use WIF AP on the phones, make sure "Wireless debugging" is activated!
![Enable Wireless USB Debugging](/images/networking/adb-debug-wireless.jpg)

- Set your own NIC name in the
  [box configurator](/getting_started/configuration) — for example `eth0` or
  `enp3s0`.

> ⚠️ Do not place a USB hub between the appliance and the boards. Use a PCIe USB
> expansion for more ports. See [Requirements](/getting_started/requirements).
