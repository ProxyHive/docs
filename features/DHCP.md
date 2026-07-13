---
Title: DHCP
---
The appliance runs a **DHCP server** on its LAN interface for the boards. Boards
connected to the LAN NIC receive an address on the appliance's private board
network and become discoverable automatically.

- The board network is a private subnet on the **LAN** interface (see
  [LAN](/networking/LAN)).
- Boards found over DHCP (or over USB/OTG) appear in the appliance device list
  without any manual entry.
- The appliance's own DHCP does not interfere with your home router — it only
  serves the isolated board network behind the LAN NIC.

![The appliance device list showing boards discovered on the LAN, each mapped to a slot.](/images/features/device-proxy-ip.png)

This is why the **LAN port must be a wired NIC**: the appliance owns that segment
and hands out addresses to the boards on it.
