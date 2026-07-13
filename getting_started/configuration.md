# Configuration

## Box configurator (WAN / LAN / architecture)

When you create a setup command you pick the hardware in the **box configurator**:

- **Raspberry Pi 5** — fixes arm64 with `wlan0` (WAN) and `eth0` (LAN).
- **Other** — enter your own interfaces and architecture:
  - **WAN interface** — the uplink to the internet. May be **Wi-Fi or a wired NIC**
    (e.g. `wlan0`, `eth1`, `enp2s0`).
  - **LAN interface** — must be a **wired NIC** connected to the boards (e.g.
    `eth0`, `enp3s0`).
  - **Architecture** — `amd64` or `arm64`.

![The box configurator with the custom WAN and LAN interface fields set to eth1 and eth0 for a mini-PC, alongside the architecture selector.](/images/getting-started/box-configurator.png)

These values are stored with your connection token and written to the appliance
configuration during setup. See [WAN](/networking/wan) and [LAN](/networking/lan).

## After first login

Log in to the appliance web interface (email login token) and you will see all
your **USB and OTG devices**. From the device list you can:

1. **Unbind** any endpoints still assigned to the legacy agent.
2. **Debloat**, install and remove APKs on each board — see
   [Debloat](/features/debloat) and [APK Install](/features/apk_install).
3. Remove the ProxyHive Agent and the Unity app from the boards and install
   **UNetwork**.
4. **Assign your endpoints** to the boards.

Each board then shows a **Proxy IP** with **ADB** and **Proxy** enabled. Continue
with the [Farmer app](/features/adb) to configure the UNetwork license.
