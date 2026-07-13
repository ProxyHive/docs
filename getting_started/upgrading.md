---
Title: Upgrading
Sort: 5
---
# Upgrading

## From the legacy Agent (Unitynodes) to UNetwork

The legacy ProxyHive **Agent** is discontinued and unsupported after **15 July
2026**. To migrate:

1. Set up a **ProxyHive Appliance** — see [Installation](/getting_started/installation).
2. In the appliance device list, **unbind** endpoints that are still assigned to
   the agent.
3. **Remove** the ProxyHive Agent and the Unity app from each board.
4. **Install UNetwork** on each board and assign your endpoints.
5. Use the [Farmer app](/features/adb) to open each board and activate its UNetwork
   license.

## Appliance updates

The appliance pulls its container images from the ProxyHive registry using the
version pinned by the platform. Updates are rolled out centrally — when a new
stack version is published, boxes pick it up on their next update cycle. You do
not build or manage images yourself.

> Note: This is **beta**. Updates may come fast and issues may come up — but the
> platform aims to stay a step ahead.
