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
