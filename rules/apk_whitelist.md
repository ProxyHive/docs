---
Title: APK Whitelist
---
The **APK whitelist** defines which apps are allowed to run on a board. It governs
both what you can [install](/features/APK_Install) and what the
[Debloat](/features/debloat) function keeps — everything not on the whitelist is
removed or disabled.

## Purpose

A board should run **UNetwork and nothing else**. The whitelist enforces that:

- Apps **on** the whitelist (e.g. UNetwork and required system components) are kept.
- Apps **not** on the whitelist — social media, browsers, games, bloatware
  installers — are removed when you debloat the board.

Keeping boards to the whitelist is how you stay within [Fair Use](/rules/fair_use)
and avoid the forbidden [Traffic Usage](/rules/traffic_usage) that leads to a ban.

![The Debloat confirmation dialog, which uninstalls every non-system app that is not on the APK whitelist.](/images/features/debloat-confirm.png)

## Manually whitelist APKs (here Genfarmer APKs)

Edit /opt/proxyhive/.env
Add

```
TOLERATED_PACKAGES_EXTRA=com.genfarmer.uiautomator,com.genfarmer.uiautomator.test
```
