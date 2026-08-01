---
Title: Console basics
Sort: 6
---

## Console basics

Everything on this page is typed into an SSH session on the appliance itself. It assumes you
come from Windows and have not worked with a Linux console before. The commands below were run
on a real appliance (Debian 13), so they exist exactly as written.

## Connecting from Windows

You have two options and both are fine.

**PuTTY** — download it from
[chiark.greenend.org.uk](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html), enter
the appliance's IP address, leave the port at `22`, and click **Open**. Type a name under *Saved
Sessions* and press **Save** so you do not retype the address every time.

**Windows' own SSH** — Windows 10 and 11 ship with it. Open PowerShell and type:

```
ssh yourname@192.168.1.50
```

Two PuTTY habits that surprise everyone:

- **Right-click pastes.** There is no Ctrl+V.
- **Selecting text copies it** immediately. There is no Ctrl+C — and pressing Ctrl+C actually
  cancels the running command.

Log in with the user and password you created while installing Debian. The `proxyhive` user that
the setup created is a *system* account with no password; it is not meant for logging in.

## Running commands as administrator

Most of what follows needs administrator rights. On Linux you do not switch user — you put
`sudo` in front of the command:

```
sudo systemctl restart proxyhive.service
```

The first `sudo` in a session asks for **your own** password, not a separate one.

## Where things live

| Path | What it is |
|---|---|
| `/opt/proxyhive` | everything belonging to the box |
| `/opt/proxyhive/.env` | the box configuration you may edit |
| `/opt/proxyhive/compose.yaml` | the container stack — do not edit by hand |

Move there and look around:

```
cd /opt/proxyhive
ls -l
```

## Network interfaces

List every network interface with its state and MAC address:

```
ip -br link
```

```
lo               UNKNOWN        00:00:00:00:00:00 <LOOPBACK,UP,LOWER_UP>
eth0             UP             98:fe:54:01:87:3a <BROADCAST,MULTICAST,UP,LOWER_UP>
wlan0            UP             98:fe:54:01:87:3b <BROADCAST,MULTICAST,UP,LOWER_UP>
wlx7cdd90909627  UP             7c:dd:90:90:96:27 <BROADCAST,MULTICAST,UP,LOWER_UP>
```

`UP` means the cable is plugged in or the radio is active. Names starting with `wlx` are USB
Wi-Fi adapters; the trailing characters are their MAC address.

## IP addresses

```
ip -br addr
```

Add `show <name>` for a single interface:

```
ip -br addr show eth0
```

The default gateway — usually your router — is shown by:

```
ip route
```

## Editing the configuration

The `.env` file holds the box settings. `nano` is the editor to use; `vim` is not installed.

```
sudo nano /opt/proxyhive/.env
```

Inside nano: arrow keys move, typing edits, **Ctrl+O** then Enter saves, **Ctrl+X** leaves. The
`^` in its help bar means Ctrl.

> **A change to `.env` only takes effect after a reboot.** The network setup, including the
> Wi-Fi access point and the LAN bridge, is built once while the box starts. Editing the file
> and restarting only the containers leaves the box running the old settings while the file
> claims otherwise. Reboot with `sudo reboot`.

The interface names in `WAN_IF` and `LAN_IF` may also be written as **MAC addresses**:

```
LAN_IF=7c:dd:90:90:96:27
```

This is worth doing for USB Wi-Fi adapters. Linux may hand out `wlan0` and `wlan1` in a
different order after a reboot, and a box that comes back with its uplink and its board network
swapped is hard to diagnose. A MAC address always means the same adapter.

> `.env` contains your appliance token. Treat the file like a password — do not post its
> contents in chats, screenshots or tickets.

## Restarting and rebooting

```
sudo systemctl restart proxyhive.service       # containers only
sudo reboot                                    # full restart, applies .env changes
```

There are two units. `proxyhive-net.service` builds the network at boot; `proxyhive.service`
starts the containers. When in doubt, reboot — it runs both in the right order.

## Updating the system

```
sudo apt update
sudo apt upgrade
```

`apt update` only refreshes the package list, `apt upgrade` installs. Answer `Y` when asked. If
it says a reboot is required, do it when the boards are idle.

This updates **Debian**, not ProxyHive. The box software updates itself — see
[Upgrading](/getting_started/upgrading).

## Installing extra software

```
sudo apt install <package>
```

For example a bandwidth monitor and a nicer process list:

```
sudo apt install iftop htop
```

If a package is not found, run `sudo apt update` first.

## Logging in with an SSH key instead of a password

A key is more convenient than a password and considerably safer.

**1. Create the key.** Open **PuTTYgen** (installed alongside PuTTY), click **Generate** and
move the mouse over the empty area until the bar fills. Then:

- **Save private key** — keep this file safe, it is the one that proves who you are.
- Copy the whole text from the box labelled *Public key for pasting into OpenSSH
  authorized_keys file*. It is one long line starting with `ssh-rsa` or `ssh-ed25519`.

**2. Put the public key on the appliance.** In your SSH session:

```
mkdir -p ~/.ssh
nano ~/.ssh/authorized_keys
```

Paste the line with a right-click, save with Ctrl+O and Enter, leave with Ctrl+X. Then fix the
permissions — SSH refuses keys that others could read:

```
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

**3. Tell PuTTY to use the key.** In the session: *Connection → SSH → Auth → Credentials →
Private key file*, pick the file you saved. Enter your username under *Connection → Data →
Auto-login username*. Go back to *Session* and **Save**.

Test it in a second window before closing the one you are working in — if something is wrong
with the key you still have a way back.

With Windows' own SSH the equivalent is one command from PowerShell:

```
type $env:USERPROFILE\.ssh\id_ed25519.pub | ssh yourname@192.168.1.50 "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

## Quick checks

```
docker ps                      # which containers are running
df -h                          # free disk space
free -h                        # free memory
uptime                         # how long the box has been up
sudo journalctl -u proxyhive-net.service -b    # network setup log from this boot
```

`docker ps` should list the box containers. If one is missing or keeps restarting, the
[Troubleshooting](/troubleshooting) page is the next stop.

To leave the session, type `exit` or close the window. Anything you started stays running — the
box does not depend on your being logged in.
