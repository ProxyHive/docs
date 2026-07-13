---
Title: Management
---
The appliance is managed through its **local web interface**, reachable from
anywhere in the world through a secure Cloudflare tunnel.

## Access

- The web interface is exposed over a per-appliance **Cloudflare tunnel** — there
  is no open port on your home network.
- To log in, enter your **ProxyHive e-mail**; you receive a **login token** to
  access the appliance.
- Once logged in you see all USB/OTG devices and can debloat, install/remove APKs,
  and assign endpoints. See [Configuration](/getting_started/configuration).

![The ProxyHive Appliance login screen, which signs in with your account e-mail via a one-time code.](/images/networking/appliance-login.png)

## Board management

Day-to-day board control — live mirror and license activation — is done with the
**[Farmer app](/features/ADB)**, which reaches the boards over a separate
account-gated ADB tunnel.
