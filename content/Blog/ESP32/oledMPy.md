---
title: "ESP32-OLED"
date: 2022-12-20T09:03:20-08:00
draft: false
---
# OLED with MicroPython on ESP32

## Connection
- VCC to 3.3V
- GND to GND
- SCL/SCK to GPIO22
- SDA to GPIO21


## Installations
- Need to install ```SSD1306 OLED Library```
- Open Editor ( Thonny or uPyCraft )
- Create a file named ```ssd1306.py```
- Copy the code from [here](https://gist.githubusercontent.com/RupakBiswas-2304/e819d3502282109896ad580f9e20c174/raw/cd134bdb78c35f4d17442a4093c4ec22e9050570/ssd1306.py)
- Save the file

## Code 
- Imports -->
```
from machine import Pin, SoftI2C
import ssd1306
from time import sleep
```
- Create I2C object -->
```
i2c = SoftI2C(scl=Pin(22), sda=Pin(21))
```
- Create OLED object -->
```
oled_width = 128
oled_height = 64
oled = ssd1306.SSD1306_I2C(oled_width, oled_height, i2c)
```

- Show text on OLED -->
```
oled.text("Hello World", 0, 0)
oled.show()
```
- Filling or clearing the screen -->
```
oled.fill(0)
oled.show()
```

- Draw a pixel -->
```
oled.pixel(0, 0, 1)
oled.show()
```

- Invert the display -->
```
oled.invert(True)
oled.show()
```
#
#
#
