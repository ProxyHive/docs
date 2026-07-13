# Requirements

## Operating system

The appliance is validated **only on Debian 13 (Trixie)**. The setup script
refuses to run on any other release. On a Raspberry Pi, install **Raspberry Pi OS
Lite (64-bit)** which is Debian-based; on x86 hardware install **Debian 13
(Trixie)**.

## Hardware — Raspberry Pi

- **Raspberry Pi 5** with at least **4 GB RAM** (8 GB recommended).
- If you run **more than 2 boxes**, add a **PCIe USB expansion**.
- An active **cooler** for the Pi is strongly recommended.
- A fast **SD card, 16 GB or larger**.

Typical investment: **$175–$250** to run up to **8 boxes**. A 4 GB Pi 5 can run
**2 boxes**.

> ⚠️ **Do not use a USB hub** between the Pi and the boxes — it will malfunction
> heavily. Use a PCIe USB expansion instead.

## Hardware — x86 (mini-PC / server)

Any x86-64 machine (for example an Intel N95/N100 mini-PC or a spare server)
running Debian 13. See [Architectures](/getting_started/architectures) and set
your interfaces in the [box configurator](/getting_started/configuration).

## Network

- A **WAN** uplink — Wi-Fi or a wired NIC. See [WAN](/networking/wan).
- A **LAN** port — a **wired NIC** connected to the boards. See [LAN](/networking/lan).

![A Raspberry Pi 5 in a metal case fitted with a PCIe-to-USB expansion board, providing eight USB 3.0 ports for connecting boards; the inset shows the Pi 5 mounted inside.](/images/getting-started/pi5-pcie-usb-case.jpg)
