---
Title: Prepare a Farm box
Sort: 4
---
## 1. Prepare boards

1. Switch your box into USB mode
2. Plug the USB cable into the appliance
3. Check that all Boards show up as USB devices
4. Clean up and prepare the boards

> ⚠️ Do not place a USB hub between the appliance and the boards. Use a PCIe USB
> expansion for more ports. See [Requirements](/getting_started/requirements).

### Clean up old Proxyhive Agent (optional, only needed if you ran the PH Agent on the phones before)
- ```adb shell am force-stop eu.proxyhive.agent```
- ```adb shell pm uninstall eu.proxyhive.agent ```
- ```adb shell settings put global http_proxy :0```

### Remove old Unity App (optional, only needed if the old Unity App is installed)
- ```adb shell am force-stop io.unitynodes.unityapp```
- ```adb shell pm uninstall io.unitynodes.unityapp```

### BATTERY 24/7 100%
- ```adb shell dumpsys battery set level 100```

### SCREEN TIME OUT
##### (prevents screen turning off and Unity app from logging off)

- ```adb shell settings put system screen_off_timeout 2147483647```

### DISABLE AUTO-ROTATE
- ```adb shell settings put system accelerometer_rotation 0```

### Enable ADB on TCPIP - This is the most important step, it switches your Boards to ADB over OTG!
- ```adb tcpip 5555```


## Now switch the box to OTG and all devices should come up with an IP Address in the 10.66.0.0/24 subnet

- Assign Endpoints to the boards (Mapping), that will enable the proxy. If you dont have free endpoint, request them or unbind unused endpoints in Proxihive Device List
- Assign a label to the Board, that makes it easier to identify them
- Install UNetwork App, use the Board Menu for this
- Configure the lease on the phone: open the board's mirror in the appliance web interface — that works from anywhere. Genfarmer & Co. are an alternative but need to run on the same subnet as the boxes
- Add the Licence-Hash to the board if you want Uptime and Rewards in the Dashboard


## Optional: Disable / Enable Auto Updates

### Samsung

##### Disable auto updates
- ```adb shell pm disable-user --user 0 com.sec.android.soagent```
- ```adb shell pm disable-user --user 0 com.wssyncmldm```
- ```adb shell pm disable-user --user 0 com.samsung.sdm```

##### Enable auto updates
- ```adb shell pm enable --user 0 com.sec.android.soagent```
- ```adb shell pm enable --user 0 com.wssyncmldm```
- ```adb shell pm enable --user 0 com.samsung.sdm```

### Xiaomi / Redmi / POCO

##### Disable auto updates
- ```adb shell pm disable-user --user 0 com.android.updater```

##### Enable auto updates
- ```adb shell pm enable --user 0 com.android.updater```

### Google Pixel / Motorola / Nokia / Nothing

##### Disable auto updates
- ```adb shell pm disable-user --user 0 com.google.android.systemupdater```

##### Enable auto updates
- ```adb shell pm enable --user 0 com.google.android.systemupdater```

### OnePlus / Oppo / Realme

##### Disable auto updates
- ```adb shell pm disable-user --user 0 com.oplus.ota```

##### Enable auto updates
- ```adb shell pm enable --user 0 com.oplus.ota```

### Huawei / Honor

##### Disable auto updates
- ```adb shell pm disable-user --user 0 com.huawei.android.hwouc```

##### Enable auto updates
- ```adb shell pm enable --user 0 com.huawei.android.hwouc```

### Sony

##### Disable auto updates
- ```adb shell pm disable-user --user 0 com.sonyericsson.updatecenter```

##### Enable auto updates
- ```adb shell pm enable --user 0 com.sonyericsson.updatecenter```







