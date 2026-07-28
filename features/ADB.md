---
Title: ADB & the Farmer App
---
Boards are managed over **ADB**. The appliance runs an ADB server that reaches
every board; the **ProxyHive Farmer** desktop app connects to it to view and drive
each board. The Farmer app can connect to the Appliance from anywhere in the world.

If you feel more comfortable using any other mirroring software, you need to do that on the local Farmbox network.
Just connect to your computer to the same network as the farmboxes, and you can discover the Boards on 10.66.0.0/24

The Farmers app might not be the best solution to setup your phones, but its the only one able to do that from outside the local network.
It may contain bugs, it might be slow, but it also is not considered your day to day management tool for now.

## Security

The ADB server grants full control over every board, so it is **never exposed
openly**. Each appliance sits behind a dedicated **Cloudflare Access** tunnel whose
only policy is a per-appliance service token. The Farmer app fetches that token
over your authenticated ProxyHive account and drives the tunnel — without the
token, Cloudflare rejects the connection at the edge.

## Using the Farmer app

1. Download the **[Farmer app for Windows](https://download.proxyhive.org/proxyhive-farmer-win-x64.zip)** or **[Farmer app for Linux](https://download.proxyhive.org/proxyhive-farmer-linux-x86_64.AppImage)**.
2. Log in with your ProxyHive account and select your appliance.
3. You will see every board of the appliance as a card with a **live screenshot**.
4. Click a board to open a **live mirror** and configure it (e.g. activate the
   UNetwork license).

![The ProxyHive Farmer app with a board mirror open, driving the on-device UNetwork app over the account-gated ADB tunnel.](/images/welcome/farmer-board-grid.jpg)

APK installs are **not** performed over this tunnel — they go through the appliance
web interface. See [APK Install](/features/APK_Install).

## Installing Farmers App on Linux (Debian, Ubuntu)

```bash
cd /tmp
rm -f proxyhive-farmer-linux-x86_64.AppImage
wget https://download.proxyhive.org/proxyhive-farmer-linux-x86_64.AppImage
chmod +x proxyhive-farmer-linux-x86_64.AppImage
./proxyhive-farmer-linux-x86_64.AppImage
```

