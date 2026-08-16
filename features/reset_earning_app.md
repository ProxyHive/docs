---
Title: Re-registering the earning app
---
Sometimes a board keeps earning but the app reports it as **unattested** — in UNetwork's own
wording, the trust tier drops to `NONE` while the integrity check itself still passes. The board
is not broken and nothing on it is missing; the app simply needs to be registered again.

You do not need to uninstall anything. Clearing the app's data is enough, and it is much faster:
the app stays installed, only its stored login goes.

## What it does

Clearing app data **signs the board out**. You will register it again afterwards, which means
going through the sign-in and solving the Cloudflare check on that board. Plan for that before
you start — a board is not earning while it sits on the sign-in screen.

## The commands

On the appliance's **Devices** page, select the boards, then **Bulk action → ADB**, and run these
three in order:

```
shell am force-stop io.unetwork.app
shell pm clear io.unetwork.app
shell monkey -p io.unetwork.app -c android.intent.category.LAUNCHER 1
```

The first stops the app so the second is not fighting a running process. The second wipes its
data — it answers `Success`. The third starts it again, so the board comes up on the sign-in
screen ready for you.

Then open each board's mirror and sign in as usual. The board's licence stays assigned to it
throughout; you do not need to re-assign it.

## Why the screen may turn sideways afterwards

Clearing app data makes Android restore its display defaults, and on most boards that default is
**auto-rotate on**. Boards lie flat or on their side in a rack, so the next screen that appears
can come up in landscape. Your appliance corrects this by itself within a few minutes, and
immediately for any board you open in the mirror. If you want it upright right away on a board
you are not mirroring:

```
shell settings put system accelerometer_rotation 0
shell settings put system user_rotation 0
```

## If the trust tier does not come back

Re-registering fixes the case where the app lost its footing. If a board still reports a low
trust tier after signing in again, that is decided on UNetwork's side, not on the board — the
integrity check has already passed. Bring it up in the support topic with the board's licence ID
and we will take it from there.
