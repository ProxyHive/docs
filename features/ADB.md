---
Title: ADB & board mirroring
---
Boards are managed over **ADB**. The appliance runs an ADB server that reaches every board, and
the appliance's own web interface uses it to view and drive them — no desktop app, no local
network. Everything happens in the browser, from anywhere in the world.

If you prefer a different mirroring tool, you can use it on the local farmbox network: connect
your computer to the same network as the farmboxes and the boards are reachable on 10.66.0.0/24.

## Security

The ADB server grants full control over every board, so it is **never exposed openly**. It
listens on the appliance's loopback interface only and is reachable exclusively through the
appliance web interface, which sits behind your ProxyHive login. The appliance itself is
published through a dedicated **Cloudflare Access** tunnel — without a valid session, Cloudflare
rejects the connection at the edge.

## Mirroring a board

1. Open your appliance's web interface and sign in with your ProxyHive e-mail.
2. Go to **Devices** — every board of this appliance is listed there.
3. Click the **mirror** icon on a board to open its live screen.
4. Drive the board with your mouse and keyboard, for example to activate its UNetwork licence.

The mirror gives you the board's real screen: touch, keyboard and clipboard all work. Use
**Paste** in the mirror's title bar (or Ctrl+V) to transfer text from your computer to the
board — handy for licence keys and wallet addresses.

APK installs do **not** run through the mirror — they have their own place in the appliance web
interface. See [APK Install](/features/APK_Install).
