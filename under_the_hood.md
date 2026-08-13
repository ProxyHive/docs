---
title: Under the hood
sort: 60
---

## Under the hood

Everything on this page is about **your** appliance — the machine standing in your room. You do
not need any of it for normal use: the web interface covers day-to-day work. It is here for when
you want to look for yourself, take a backup, or understand what an update actually does.

# Where things live

The whole installation sits in one directory, `/opt/proxyhive`:

| Path | What it is |
|---|---|
| `.env` | your configuration — interface names, WiFi credentials, the appliance token |
| `compose.yaml` | which containers run, in which versions |
| `config/` | generated configuration for the proxy and DNS services |
| `state/` | board mappings, DHCP leases, discovery data, attestation results |
| `init.sh` | network setup, runs at boot |
| `update.sh` | pulls the current stack |

# The containers

Five, all managed together:

| Container | Job |
|---|---|
| `ph-agent` | the brain: talks to the boards over adb, runs the API the interface uses |
| `ph-proxy` | routes each board's traffic to its own endpoint |
| `ph-dns` | DNS for the boards, and the block list that keeps them off the wrong servers |
| `ph-ui` | the web interface you log into |
| `ph-cloudflared` | the tunnel that makes your appliance reachable from the outside |

Have a look with:

```
cd /opt/proxyhive
docker compose ps
docker compose logs -f agent      # or proxy, dns, ui, cloudflared
```

# Getting a shell on your own appliance

It is an ordinary Linux machine on your network, so ordinary SSH:

```
ssh root@<the appliance's IP on your LAN>
```

The IP is in your router, or on the appliance's own screen if it has one. This has nothing to do
with the **ProxyHive support access** toggle in Box settings — that one only controls whether
*our* support key is accepted, and it is off unless you switch it on.

# What an update does, and what it never touches

The Update button in the interface and `./update.sh` do the same thing: fetch the current stack,
pull the images, bring the containers up.

**It is non-destructive.** `.env`, `state/`, your board mappings and the tunnel are all kept.

What it *does* replace, every time, is `compose.yaml` and everything under `config/`. Those files
come from us and are overwritten without asking.

The practical consequence is worth remembering:

- **Editing `.env` is a real change.** It survives updates.
- **Editing `compose.yaml` or `config/` is not.** It works until the next update, then quietly
  reverts — and the fault comes back at the worst possible moment, when you have long since
  stopped thinking about it.

One more thing about `.env`: Docker Compose reads it when a container is **created**, not when it
is restarted. After changing a value:

```
docker compose up -d --force-recreate     # picks the new values up
docker compose restart                    # does NOT — keeps the old ones
```

# Backing it up

There is no export button. There does not need to be one: a backup is three directories and a
file, so the ordinary Linux tools do the job.

Worth saving:

```
/opt/proxyhive/.env         your configuration and the appliance token
/opt/proxyhive/config/      generated, but harmless to keep
/opt/proxyhive/state/       board mappings — the part that would take longest to redo
```

A minimal version, run from another machine or a cron job:

```
tar czf ph-backup-$(date +%F).tar.gz -C /opt/proxyhive .env config state
```

and then move it off the appliance — `rsync`, `scp`, a NAS, cloud storage, whatever you already
use. A disk that dies takes the backup sitting on it with it.

Daily, on the appliance itself:

```
0 3 * * * tar czf /tmp/ph-backup.tar.gz -C /opt/proxyhive .env config state \
          && rsync -q /tmp/ph-backup.tar.gz backup@yourserver:/backups/
```

**Treat the backup as a secret.** `.env` contains your appliance token and your WiFi password.
Anyone holding that file holds your appliance.

To restore onto new hardware: install ProxyHive as usual, stop the stack, put the three items
back, start it again.

```
cd /opt/proxyhive && docker compose down
tar xzf ph-backup.tar.gz -C /opt/proxyhive
docker compose up -d
```

# When the disk fills up

Old images are the usual culprit — every update leaves the previous version behind.

```
docker system df                 # what is actually using the space
docker image prune -a            # remove images no container uses
docker system prune              # the above, plus stopped containers and unused networks
```

Both are safe while the stack is running: anything in use is skipped. Do **not** add `--volumes`
— that would delete `state/` contents that containers hold open.

# Looking around

Nothing here changes anything:

```
df -h                    # disk
free -h                  # memory
uptime                   # load
docker stats --no-stream # per-container CPU and memory
ip -br addr              # interfaces and their addresses
iw dev                   # wireless interfaces
journalctl -u docker -n 50
```

For the boards specifically, the agent already knows more than the shell does — the Devices page
in the interface is the better starting point.
