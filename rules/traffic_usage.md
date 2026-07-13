# Traffic Usage

Endpoints must carry **UNetwork traffic only**. The appliance reveals non-UNetwork
traffic on your boards, and such traffic leads to a **permanent ban without
refund**. Non-UNetwork traffic also drives endpoint prices up for everyone.

## Forbidden traffic

- **Social media** — e.g. Facebook, Instagram, TikTok.
- **Video portals** and streaming.
- **Images / graphics** — e.g. downloading memes from tenor.com.
- **Games** and gaming backends.
- **Downloads** of any kind.

## Known violations to fix now

**Tracfone Android devices — Digital Turbine (DT Ignite / Mobile Services
Manager).** The host `download-tracfone.dtignite.com` is used as a bloatware
installer that silently downloads sponsored apps in the background. If you use
these phones, **disable that software before enabling the proxy**:

1. Open **Settings → Apps** (or Apps & Notifications).
2. Tap **See all apps** and find **Mobile Services**, **DT Ignite** or **Discover
   Bar**.
3. Tap **Force Stop**, then **Disable** or **Uninstall**.

**Swish (gaming / sports).** The domain `events.swishapps.ai` is the backend for
the Swish app (local sports / pickleball). This traffic drives prices up — **do
not** run it. No refunds if you are caught.

> ⚠️ If you do not disable bloatware/forbidden apps, your access to ProxyHive will
> be terminated **without any refund**.

Use [Debloat](/features/debloat) and the [APK Whitelist](/rules/apk_whitelist) to
keep boards clean.
