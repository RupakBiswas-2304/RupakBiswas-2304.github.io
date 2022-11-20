# ESP-NOW [ micropython ]

## Installation
- This module is not available in the default firmware
- To install this module we need to flash percompiled firmware (with esp-now module) or compile the firmware from source
- To flash precompiled firmware, download the firmware from [here](https://github.com/glenn20/micropython-espnow-images)
- [source code](https://github.com/glenn20/micropython/tree/espnow-g20)
- How to flash ? go to this [link](../micropython/)

## Sender Code
```
import network
import espnow

# A WLAN interface must be active to send()/recv()
sta = network.WLAN(network.STA_IF)  # Or network.AP_IF
sta.active(True)
sta.disconnect()   # For ESP8266

e = espnow.ESPNow()
e.active(True)
peer = b'\xbb\xbb\xbb\xbb\xbb\xbb'   # MAC address of peer's wifi interface
e.add_peer(peer)

e.send("Starting...")       # Send to all peers
for i in range(100):
    e.send(peer, str(i)*20, True)
    e.send(b'end')
```

## Reciver Code
```
import network
import espnow

# A WLAN interface must be active to send()/recv()
sta = network.WLAN(network.STA_IF)
sta.active(True)
sta.disconnect()   # Because ESP8266 auto-connects to last Access Point

e = espnow.ESPNow()
e.active(True)
peer = b'\xaa\xaa\xaa\xaa\xaa\xaa'   # MAC address of peer's wifi interface
e.add_peer(peer)

while True:
    host, msg = e.recv()
    if msg:             # msg == None if timeout in recv()
        print(host, msg)
        if msg == b'end':
            break
```