---
Title: ADB & the Farmer App
---
Boards are managed over **ADB**. The appliance runs an ADB server that reaches
every board; the **ProxyHive Farmer** desktop app connects to it to view and drive
each board.

## Security

The ADB server grants full control over every board, so it is **never exposed
openly**. Each appliance sits behind a dedicated **Cloudflare Access** tunnel whose
only policy is a per-appliance service token. The Farmer app fetches that token
over your authenticated ProxyHive account and drives the tunnel — without the
token, Cloudflare rejects the connection at the edge.

## Using the Farmer app

1. Download the **[Farmer app](https://download.proxyhive.org)** for Windows, macOS
   or Linux.
2. Log in with your ProxyHive account and select your appliance.
3. You will see every board of the appliance as a card with a **live screenshot**.
4. Click a board to open a **live mirror** and configure it (e.g. activate the
   UNetwork license).

![The ProxyHive Farmer app with a board mirror open, driving the on-device UNetwork app over the account-gated ADB tunnel.](/images/welcome/farmer-board-grid.jpg)

APK installs are **not** performed over this tunnel — they go through the appliance
web interface. See [APK Install](/features/APK_Install).
