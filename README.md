# ESP32 uCommMgr.py

## WiFi Client
This Micropython library has the BLE and WiFi connection function. When you pass some string like 'myDevice' as below, it will be the part of the mDNS hostname. The hostname would be myDevice-2cf0c0, where 2cf0c0 is the last three bytes of the MAC address.
```python
    nic = ComMgr.startWiFi('myDevice')                  # pass the name as the argumen for the hostname
```

## BLE Client

```python
    #startBLE(name, myBLECallback=None)
    startBLE('myDevice', myCallback)
```

This starts the BLE service with the given name and the callback if specified. The `name` will be the BLE device name once started, myBLECallback is the optional callback function you can define and pass. 

This callback process the passed message if the message is what it is supposed to handle and should return `True`, otherwise return `False`. If it returns `False` the libray's built-in remaining callback will continue processing.

# Library Installation
* Connect ESP32 to the Internet and run the following code
```python
import network
nic = network.WLAN(network.STA_IF)
nic.active(True)
nic.connect('ssid', 'password')
nic.ifconfig()          # check if the WiFi is connected or wait until connected

import mip
mip.install('github:yhur/uComMgr/package.json')
```
