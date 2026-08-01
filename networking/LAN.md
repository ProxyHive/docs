---
Title: LAN
---
The **LAN** interface connects the appliance to the boards. The appliance owns this
segment, runs [DHCP](/features/DHCP) on it, and routes each board through its
assigned endpoint.

- Set your own NIC name in the
  [box configurator](/getting_started/configuration) — for example `eth0` or
  `enp3s0`.
- The LAN port can be a wired NIC or Wi-Fi / Dongle like ALFA AWUS036ACM (MT7612U) for the boards
  network.
- If you use WLAN for the LAN interface, do NOT use the onboard wlan0 broadcom chip, it cant handle the devices, use a dongle.

If you use the Appliance WIFI AP for the phones, make sure "Wireless debugging" is activated!

![Enable Wireless USB Debugging](/images/networking/adb-debug-wireless.jpg)


You can use multiple LAN Interfaces to connect boards to the appliance
The following combination of devices is possible (sample interface names):
- LAN_IF=eth
- LAN_IF=wlan
- LAN_IF=eth0,wlan

```Do NOT use 2 wifi interfaces on LAN_IF, they would share SSID and Password and phones would switch the connections all the time```


