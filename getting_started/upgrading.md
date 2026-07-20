---
Title: Upgrading
Sort: 5
---
## From the legacy Agent (Unitynodes) to UNetwork

The legacy ProxyHive **Agent** is discontinued and unsupported after **15 July
2026**. To migrate:

1. Set up a **ProxyHive Appliance** — see [Installation](/getting_started/installation).
2. In the appliance device list, **unbind** endpoints that are still assigned to
   the agent.
3. **Remove** the ProxyHive Agent and the Unity app from each board.
4. **Install UNetwork** on each board and assign your endpoints.
5. Use the [Farmer app](/features/ADB) to open each board and activate its UNetwork
   license.

## Appliance updates

The appliance pulls its container images from the ProxyHive registry using the
version pinned by the platform. Updates are rolled out centrally — when a new
stack version is published, boxes pick it up on their next update cycle. You do
not build or manage images yourself.


## Inplace Stack update (Debian Bash)

```bash
cd /opt/proxyhive && set -a && . ./.env && set +a && \
curl -fsSL -H "x-appliance-token: $APPLIANCE_TOKEN" \
  "${PROXYHIVE_API_URL:-https://proxyhive.org}/api/appliance/stack" \
| python3 -c 'import json,os,sys
f=json.load(sys.stdin).get("files",{})
sys.exit("empty stack") if not f else None
for p,c in f.items():
    d=os.path.dirname(p)
    os.makedirs(d,exist_ok=True) if d else None
    open(p,"w").write(c)
print("stack:",len(f),"files")' && \
docker login registry.proxyhive.org -u box -p "$APPLIANCE_TOKEN" >/dev/null && \
docker compose pull && docker compose up -d && \
docker compose up -d --force-recreate dns proxy && \
docker compose ps
```

> Note: This is **beta**. Updates may come fast and issues may come up — but the
> platform aims to stay a step ahead.
