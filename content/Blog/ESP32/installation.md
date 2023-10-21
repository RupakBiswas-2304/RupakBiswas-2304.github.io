---
title: "ESP-IDF Installation"
date: 2022-12-20T09:03:20-08:00
draft: false
---

## Installation of ESP-IDF
(windows)

- Install ESP-IDF installer from [here](https://dl.espressif.com/dl/esp-idf/?idf=4.4)
- For linux and mac get it from [here](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/linux-macos-setup.html)
- Goto [here](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/get-started/#get-started-get-esp-idf) for brief installation guide
- Open installer and check all the check all the checkbox and do a default installation

## How to flash microPython firmware in esp32 
[ linux & windows ]

- go to [micropython offical site](https://www.espressif.com/en/support/download/athttps://micropython.org/download/#esp32)  
- Select esp32 or any other board if you are using
- make sure to have esptool.py installed or do `pip install esptool` instead
- Download the firmware ( latest prefferable )
- erase the flash memory
        ``` esptool.py --port /dev/ttyusb0 erase_flash```

- flase the downloaded firmware
        ```esptool.py --chip esp32 --port /dev/ttyUSB0 --baud 460800 write_flash -z 0x1000 esp32-20190125-v1.10.bin```

- for windows users, port might be com7/com8 etc instead of /dev/ttyusb0, go to device manager and check the port number

## how to flash defualt firmware in esp32 ? 
[ linux & windows ]

- go to https://www.espressif.com/en/support/download/at. (or google search esp firmware)
- download the firmware according to your board version.
- make sure to have esptool.py installed or do `pip install esptool` insteed
- erase the flash memory
        ``` esptool.py --port /dev/ttyusb0 erase_flash```

- flase the downloaded firmware
        ``` esptool.py --port /dev/ttyusb0 --baud 460800 write_flash --flash_size=detect 0 factory/factory_wroom-32.bin```

- for windows users, port might be com7/com8 etc instead of /dev/ttyusb0, go to device manager and check the port number
- 