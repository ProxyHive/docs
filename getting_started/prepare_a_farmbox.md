---
Title: Prepare a Farm box
Sort: 4
---
## 1. Prepare boards

1. Switch your box into USB mode
2. Plug the USB cable into the appliance
3. Check that all Boards show up as USB devices
4. Clean up and prepare the boards

### Clean up old Proxyhive Agent
- ```adb shell am force-stop eu.proxyhive.agent```
- adb shell pm uninstall eu.proxyhive.agent 
- adb shell settings put global http_proxy :0

### Remove old Unity App
- adb shell am force-stop io.unitynodes.unityapp
- adb shell pm uninstall io.unitynodes.unityapp

### BATTERY 24/7 100%
- adb shell dumpsys battery set level 100

### SCREEN TIME OUT
(prevents screen turning off and Unity app from logging off)

- adb shell settings put system screen_off_timeout 2147483647

### DISABLE AUTO-ROTATE
- adb shell settings put system accelerometer_rotation 0

### Enable ADB on TCPIP
- adb tcpip 5555


## Now switch the box to OTG and all devices should come up with an IP Address in the 10.66.x.y space

- Assign Endpoints to the boards, that will enable the proxy
- Give you Board a label
- Install UNetwork
- Use a mirror to configure the lease on the phone
- Add the Licencehash to the board



