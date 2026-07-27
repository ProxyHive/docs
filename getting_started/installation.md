---
Title: Installation
Sort: 2
---
## 1. Prepare the host

Install **Debian 13 (Trixie)** — on a Raspberry Pi use the **Raspberry Pi Imager**
to flash **Raspberry Pi OS Lite (64-bit)**:

1. Download the [Raspberry Pi Imager](https://www.raspberrypi.com/software).
2. Choose **Raspberry Pi OS (other) → Raspberry Pi OS Lite (64-bit)**.
3. In the imaging options set a **user + password (or SSH key)** and your **Wi-Fi
   credentials**.
4. Boot the Pi, find its IP in your router's DHCP leases, and connect over SSH.

# Network helper
In case you cant setup your interfaces on install, there is a little helper that will assist in preparing the network devices for you.
It will find WIFI dongles, install the drivers, setup wifi connection (if you want WIFI as your uplink and you used the LAN Port for installation).

Download:
```
wget https://download.proxyhive.org/net-setup.sh
```
Put that file on the appliance and start it
```
bash net-setup.sh
```

Use at own risk, but it should help you fix network issues


## 2. Generate your setup command

1. Open the ProxyHive dashboard and go to **Appliances**.
2. Click **Set up a box**, give it a name, and choose your hardware (Raspberry Pi
   5 preset, or Custom with your WAN/LAN interfaces and architecture — see the
   [box configurator](/getting_started/configuration)).
3. Click **Generate setup command** and copy it.

![The "Set up a box" card in the dashboard with hardware, WAN/LAN interface and architecture fields filled in, and the generated one-line setup command ready to run over SSH.](/images/getting-started/box-configurator.png)

## 3. Run it on the host

Paste the command into the host's terminal:

```bash
curl -fsSL https://proxyhive.org/setup-pi.sh | sudo bash -s <your-token>
```

The script installs all required software (Docker, network stack) and links the
appliance to your account.

> ⚠️ The script requires **Debian 13 (Trixie)** and will refuse to run on other
> releases.

## 4. Find your appliance

Once the appliance is up, it appears in your ProxyHive menu. It is reachable from
anywhere in the world — enter your ProxyHive e-mail to receive a **login token**.

Next: [Configuration](/getting_started/configuration).
