---
Title: Traffic guard
---

Traffic is billed by the gigabyte, and a board can start downloading something entirely
on its own — a system update, a vendor bloatware installer, an app that decides to
refresh itself. Left alone, one board can spend a noticeable part of your balance
overnight while you are asleep.

The **traffic guard** watches every board's traffic and steps in before that happens.
It is on by default.

## What it does

A board that pulls more than **5 MB within 60 seconds** is taken off its paid endpoint
for **20 minutes**, and the account owner gets an e-mail.

Being "taken off the endpoint" does not mean the board is switched off:

- It keeps working, over the appliance's own internet line instead of the paid one.
- That traffic is **not billed** — it runs over your own connection.
- It also switches to your router's DNS, so whatever it was downloading can finish.

That last part matters. A board held with its download half-finished would only try
again after the hold and be held again, forever. Letting it complete over your own line
ends the loop: after 20 minutes the board returns to its endpoint with nothing left to
fetch.

## What it is not

It is not a punishment and not a fault. A board that trips the guard has done nothing
wrong — something on it wanted a large download, and the guard made sure you did not
pay for it. Boards recover by themselves; there is nothing to reset.

## Where to see it

**Settings → Watchdogs** on the appliance shows whether the guard is on, the limit it
applies, and any board it is currently holding with the time remaining.

## Turning it off

The same page has the switch. Off means nothing limits how much a single board can pull
through its paid endpoint, and one phone downloading a system update can run through a
large part of your balance unnoticed.

There is one honest reason to switch it off: a deliberate bulk transfer that you want to
run over the endpoints and do not want interrupted. Switch it back on afterwards — a
guard left off is only noticed on the bill.

Switching it off releases any board it is holding at that moment.

## If a board is held right after you re-enable its proxy

Boards remember DNS answers for about four minutes. If you switch a board's proxy back
on straight after [updating it](/features/proxy), a download can briefly continue over
the endpoint and trip the guard. Nothing is broken — wait for the hold to pass, and it
will not happen again once the board's cache has expired.
