---
Title: Box Control
---
Box-level hardware is managed on the appliance **Settings** page (`/settings`).

## USB / OTG slots

The Settings page lists the appliance's **USB and OTG slots** and the board
connected to each. Use it to see how your boards map to physical ports and to
manage the slots.

![The appliance Settings page listing the USB/OTG slots, each switchable between Proxy, USB, Power and Off.](/images/features/box-settings.png)

> ⚠️ Do not put a USB hub between the host and the boards. If you need more ports,
> use a PCIe USB expansion. See [Requirements](/getting_started/requirements).

## Fan control

The Settings page also exposes **fan control** for the appliance, so you can keep
the host cool under load. An active cooler is recommended, especially on a
Raspberry Pi 5.

![The fan control section on the appliance Settings page, with the cooling level slider and live voltage readout.](/images/features/fan-control.png)
