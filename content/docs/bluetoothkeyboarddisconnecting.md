---
date: '2025-01-05T22:22:38Z'
draft: false
title: 'Bluetooth Keyboard keeps dropping out connection'
tags: 
- Command-Line
- Linux
---

For no specific reason I can tell my bluetooth keyboard SUBBLIM dropped the connection on my linux mint 21 machine. Bluetooth logs shows:
 
```
 bluetoothd[1109]: profiles/input/hog-lib.c:report_reference_cb() Read Report Reference descriptor failed: Request attribute has encountered an unlikely error
 bluetoothd[1109]: profiles/input/hog-lib.c:info_read_cb() HID Information read failed: Request attribute has encountered an unlikely error
```

I procedded to solve it as follows: 

```
Install sudo apt-get install blueman

load module modprobe btusb 
```

Removed the bluetooth device from the UI or you can use the command `bluetoothctl remove 54:46:6E:2F:15:5B`

You might also want to disable the autosuspend:

`echo "options btusb enable_autosuspend=N" | sudo tee /etc/modprobe.d/btusb.conf` or ` sudo sed -i 's/#IdleTimeout=30/IdleTimeout=0/g' /etc/bluetooth/input.conf` 

Then reboot to apply the changes. 
