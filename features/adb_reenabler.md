---
Title: ADB-Reenabler
---
A board that reboots stops answering the appliance. Android does not keep the setting that lets
adb reach a board over the network — it is deliberately temporary — so after a restart the board
is invisible: no mirror, no bulk actions, no proxy changes, no screenshots. On a rack of forty
boards, a power cut used to mean plugging a cable into every one of them.

**ADB-Reenabler** is a small app that lives on the board and puts that access back by itself,
about twenty seconds after every boot. Nobody has to be there when it happens.

## What you need

- The **ADB-Reenabler dongle** in the appliance. It is a Wi-Fi adapter running a network that
  leads nowhere: no internet, no route, nothing but an address. The boards never use it for
  traffic; it exists because Android refuses to enable network debugging on a device that is not
  joined to any Wi-Fi network at all.
- The **ADB-Reenabler app** on each board you want covered. Your appliance installs it for you.

Boards that reach the appliance over a cable and boards that use Wi-Fi are both covered. The app
works the same way on either.

## Setting up a board — once

Open the board in the **mirror**, start ADB-Reenabler and press **Enable ADB-Reenabler**. Android
will ask you three things. Each answer is remembered, and this is the only time you will see them:

1. **Connect to the network?** — confirm. If a second popup warns that the network has no
   internet, choose **Stay connected**, not "only this time".
2. **Allow wireless debugging on this network?** — tick **Always allow on this network**, then
   **Allow**. Without the tick, Android asks again after every reboot and the app cannot finish.
3. **Allow debugging from this computer?** — tick **Always allow from this computer**, then
   **Allow**. This is the app asking the board to trust it.

When all four lines on the screen are green, press **Done — run in background**. The app
disappears and does not need to be opened again.

> The mirror picture may drop out for a moment during this. That is expected: restoring adb
> access restarts the board's debugging service, which closes every connection to it, the
> mirror's included. Your appliance reconnects on its own.

## What happens after that

On every boot the app checks whether the board is already reachable. If it is, it does nothing
and stops. If it is not, it restores access and steps back out of the way.

It also leaves the Wi-Fi alone whenever it can. If your board is on Wi-Fi and connected, that is
all Android needs, and the appliance's network is never touched. Only a board with no Wi-Fi
connection at all reaches for it, and it lets go again as soon as the work is done.

**The dongle's network is never saved on the board.** It cannot become the board's preferred
network and Android will never connect to it on its own — the app holds that connection open for
the few seconds it needs and it ends with it. You can confirm this on any board: the dongle's
network never appears in its list of saved Wi-Fi networks.

## Wi-Fi boards: save the network properly

This is the one thing that can still leave a Wi-Fi board stranded, and it has nothing to do with
ADB-Reenabler.

If you gave a board its Wi-Fi credentials over adb — for example with `cmd wifi connect-network`
— **the board forgets them when it reboots.** Networks added that way are temporary by design.
They never enter the saved list, and after a restart the board comes up with no network at all.

Set the Wi-Fi up **on the board itself**, through Android's own Wi-Fi settings in the mirror. A
network saved there survives reboots and reconnects on its own. You can check a board with:

```
shell cmd wifi list-networks
```

If that answers `No networks`, the board has nothing to come back to.

## When it does not work

**The app never gets past the first line.** The dongle's network is not reachable. Check that the
ADB-Reenabler dongle is plugged into the appliance and that the board is close enough to it —
these are small adapters with small antennas.

**The second line fails.** Android refused to keep wireless debugging on. This is almost always
the missing **Always allow on this network** tick; run the setup again and watch for that popup.

**The third line fails.** The board no longer trusts the app's key. It will offer it again by
itself — confirm the dialog, and tick **Always allow from this computer** this time.

**A board is unreachable and its screen shows nothing useful.** Connect it by cable once and open
it in the mirror; the appliance can reach any board over USB regardless of its network state.
