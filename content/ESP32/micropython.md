## how to flash microPython firmware in esp32 ? 
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
