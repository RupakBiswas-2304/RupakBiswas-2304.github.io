## How to flash defualt firmware in ESP32 ? 
[ Linux & Windows ]

- Go to https://www.espressif.com/en/support/download/at. (or google search ESP firmware)
- Download the firmware according to your board version.
- Make sure to have esptool.py installed or do `pip install esptool` insteed
- Erase the flash memory
        bash
        ``` esptool.py --port /dev/ttyUSB0 erase_flash```

- Flase the downloaded firmware
        bash
        ``` esptool.py --port /dev/ttyUSB0 --baud 460800 write_flash --flash_size=detect 0 factory/factory_WROOM-32.bin```

- For windows users, port might be COM7/COM8 etc instead of /dev/ttyUSB0, go to device manager and check the port number
