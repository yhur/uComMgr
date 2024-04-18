# ESP32 uCommMgr.py

## WiFi Client
This Micropython library has the BLE and WiFi connection function. This uses the configuration file `wifi.cfg` to get the ssid and wifi password. The format is as follows.
```json
{ "ssid" : "wifi ssid", "pw" : "wifi password"}
```

```python
# uComMgr32.startWiFi(name, ssid=None, pw=None)
nic = uComMgr.startWiFi('myDevice')                  
```
When you pass some string like 'myDevice' as above, this will connects to the wifi and the name will be the part of the mDNS hostname. The hostname would be myDevice-2cf0c0, where 2cf0c0 is the last three bytes of the MAC address.



## BLE Client

```python
# uComMgr32.startBLE(name, myBLECallback=None)
uComMgr.startBLE('myDevice', myCallback)
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
mip.install('github:yhur/uComMgr32')
```
