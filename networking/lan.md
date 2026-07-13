# LAN

The **LAN** interface connects the appliance to the boards. The appliance owns this
segment, runs [DHCP](/features/dhcp) on it, and routes each board through its
assigned endpoint.

- The LAN port **must be a wired NIC** — Wi-Fi is not supported for the board
  network.
- On a **Raspberry Pi 5** the default LAN interface is **`eth0`**.
- On other hardware, set your own NIC name in the
  [box configurator](/getting_started/configuration) — for example `eth0` or
  `enp3s0`.

> 📷 **Screenshot:** _The box configurator LAN interface field._

> ⚠️ Do not place a USB hub between the appliance and the boards. Use a PCIe USB
> expansion for more ports. See [Requirements](/getting_started/requirements).
