---
title: More than 240 boards
sort: 40
---

## More than 240 boards on one appliance

The board network is a `/24` by default: `10.66.0.0/24`, with addresses handed out from
`10.66.0.10` to `10.66.0.250`. That is **241 boards**, which covers twelve boxes of twenty and is
more than almost anybody needs.

If you need more, the network can be widened to a `/22` — `10.66.0.0/22`, **1022 addresses**,
with a pool of 1009. It is a single line in your configuration, and it is off unless you set it.

# Before you start

**This changes the netmask every board is given over DHCP.** It is not a setting that only
affects the appliance, and that is why it is opt-in rather than the default.

The good news is that the change is designed not to interrupt anything: `10.66.0.0/24` sits
entirely inside `10.66.0.0/22`, and your gateway stays `10.66.0.1`. Boards already running keep
their address and their gateway, and pick up the wider mask when their lease renews — within the
hour. Nothing is torn down.

**Take a backup of `.env` first.** It is one file and it is the only thing here you cannot
regenerate. See the "Under the hood" page.

# Making the change

Edit `/opt/proxyhive/.env` and add:

```
LAN_CIDR=10.66.0.0/22
```

Then re-create the agent so it reads the new value:

```
cd /opt/proxyhive
docker compose up -d --force-recreate agent
```

**`up -d --force-recreate`, not `restart`.** Compose passes the environment through when a
container is *created*; a restart keeps the old values and the change appears to do nothing.

Give it about a minute. The appliance widens the bridge, the routing and the DHCP pool by itself,
and re-creates the DNS service so the new pool takes effect.

# Checking it worked

```
ip -4 -o addr show dev br-lan          # 10.66.0.1/22, and nothing else
ip route show table 100 | grep br-lan  # 10.66.0.0/22 dev br-lan
grep dhcp-range /opt/proxyhive/config/dns.conf
```

The pool line should read `10.66.0.10,10.66.3.250,255.255.252.0`.

The bridge must carry **only** `10.66.0.1/22`. If you also see `10.66.0.1/24` next to it,
something has gone wrong — the narrower one wins and your boards are on the smaller network while
everything looks correct at a glance. Tell us rather than deleting it yourself.

Your boards will still show `10.66.0.x` addresses, and that is fine — they simply have not
renewed yet. New boards get addresses from the wider range immediately.

# Going back

Remove the line, or set it to `10.66.0.0/24`, and re-create the agent the same way. Do this only
if you have fewer than 241 boards: with more, the ones outside `10.66.0.x` lose their address and
will not come back until their slot is power-cycled.

# What this does not solve

More addresses is not more capacity everywhere else. Before going past a few hundred boards, check
that the rest keeps up — see "Choosing hardware" for what an appliance of that size needs, and
remember the practical ceiling of ten boxes per appliance.

If a board loses its gateway it does **not** re-negotiate its network connection. It stays down
until the slot is power-cycled, which needs someone at the appliance. That is why this page tells
you to widen the network rather than to move it, and why we do not change it for you.
