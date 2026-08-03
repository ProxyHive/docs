---
title: Troubleshooting
sort: 30
---

## Troubleshooting

# Power failures
If your box loses power, it switches to USB and the phones lose ADB over TCP

# Phone requirements
To make a phone work on the appliances they need to have OTG AND ADB on Port 5555, or with WIFI phones at least ADB on 5555 and internet before you switch it to the appliance wifi.

# PH Agent installations
Before you switch a phone that had a PH Agent installed before to an appliance, make sure the Agent ist stopped and removed.
Then make sure the Phone has internet.
If it does not have Internet, use the adb command 

```
adb shell settings put global http_proxy :0
```
to fix it.

# No Internet connection on Devices
All Phones and laptops connected to the LAN side of the appliance will have NO INTERNET unless they have an endpoint mapped, and no software installs that blocks the proxy
You can list all installed software with the appliance, you can debloat the phone (That will be removed 1st of august and you can run any software you like). That means a laptop attached to the appliance for genfarmer wil NOT have Internet, but it can reach the phones!

# Requirements for Proxies
- If the phone has internet before you attach it to the appliance
- and it still has OTG and ADB on port 5555
- and it then has an endpoint mapped
- and it has no bloatware installed that would block the proxy

you should see ADB and PROXY green and you should see an exit IP.

# App install
After all issues above have been fixed, you can then install UNetwork onto the phone with the appliance Board menu and use genfarmer over USB to configure the app

# Play Store updates will not download

This is deliberate while a board's proxy is on. The appliance blocks Google's download
servers so app packages are not pulled through your paid endpoint, where they would be
billed as traffic — a single system component can be well over 100 MB per board.

To update a board, switch its proxy **off** in the device list, let the updates finish,
then switch it back on. With the proxy off the board uses your own internet line and
your own router's DNS, and the downloads work. See [Proxy](/features/proxy).

Give it a few minutes after switching back on: boards cache DNS answers for about four
minutes, so a download may briefly continue over the endpoint and trip the traffic
guard. The board releases itself after the hold.

# Not earning
The 3rd button (UNet OK) only becomes green when your Unity API is connected on Proxyhive, and a license hash has been assigned to the phone on the appliance

# Test Environment
The S21 Boxes are running 24/7 in the PH lab and have 100% uptime and around 20 cents per day each

# Other

So if your phone freezes, has no internet, has bloatware installed, is not certified, has no OTG, has no ADB .... Please fix that FIRST..
