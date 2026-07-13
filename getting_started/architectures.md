# Architectures

The ProxyHive Appliance ships as **multi-architecture** container images, so the
same setup works on both:

| Architecture | Typical hardware |
|---|---|
| **arm64** | Raspberry Pi 5 (Raspberry Pi OS Lite 64-bit) |
| **amd64** | x86 mini-PCs (Intel N95/N100), spare servers (Debian 13) |

When you generate a setup command in the [box configurator](/getting_started/configuration),
you select your hardware. The **Raspberry Pi 5** preset uses arm64 with the
`wlan0`/`eth0` interfaces. For anything else, choose **Custom** and set your
architecture and interface names.

The setup script detects the CPU architecture automatically and pulls the matching
image, so no manual image selection is needed on the box itself.

![The box configurator with the hardware selector; choosing "Other (mini-PC / server — custom)" reveals the WAN/LAN interface and architecture fields, here set for an amd64 mini-PC.](/images/getting-started/box-configurator.png)
