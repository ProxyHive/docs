# Debloat

Each board in the appliance device list has a **Debloat** action. Debloat removes
apps from the board that are **not on the APK whitelist**, cutting background
traffic and reducing the risk of policy violations.

## Why debloat

Some devices ship with vendor software that generates traffic on its own — for
example bloatware installers that silently download sponsored apps. If such
software runs while an endpoint is active, it produces forbidden traffic and can
get your account banned. See [Traffic Usage](/rules/traffic_usage).

Debloat helps you strip a board down to **UNetwork only**.

## How to use it

1. Open the appliance **device list**.
2. Select the board and choose **Debloat**.
3. The board is reduced to the apps on the [APK Whitelist](/rules/apk_whitelist);
   everything else is removed or disabled.

![The Debloat confirmation dialog on a board, warning that every non-system app not on the whitelist will be uninstalled.](/images/features/debloat-confirm.png)

> ⚠️ You are still responsible for the board. If your device ships bloatware that
> Debloat cannot fully remove, disable it manually before enabling the proxy —
> see [Traffic Usage](/rules/traffic_usage).
