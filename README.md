# tcs3472-micropython

A MicroPython library for the TCS3472 light sensing chip

## Introduction

This library drives the TAOS TCS3472 (https://cdn-shop.adafruit.com/datasheets/TCS34725.pdf) light sensing chip using the I²C protocol. It can be used on MicroPython devices using the standard built-in `machine.I2C` class (https://docs.micropython.org/en/latest/library/machine.I2C.html), such as the ESP8266 and ESP32.

It is based on the Pimoroni enviro:bit MicroPython library: https://github.com/pimoroni/micropython-envirobit.

## Usage

### Prerequisites

+ Upload the `tcs3472.py` file to the MicroPython device.
+ Connect the TCS3472 chip to your device using the I²C pins (Vcc, Ground, SDA, and SCL).

### Usage

First initialise the sensor it like so:

```
from tcs3472 import tcs3472
light_sensor = tcs3472(bus, address) 
```

`bus` should be a `machine.I2C` bus object *(required)*

`address` should be a 7-bit hexadecimal value: the I²C address of the sensor *(optional; default `0x29`)*


Your class instance, `light_sensor`, will now have the following methods:

* `light_sensor.rgb()` - returns the corrected levels of red, green and blue out of 255  
* `light_sensor.scaled()` - return the amounts of red, green and blue on a scale of 0-1 
* `light_sensor.light()` - return a raw reading of light level on a scale of 0-65535 

### Example

```
import machine
from tcs3472 import tcs3472

bus = machine.I2C(sda=machine.Pin(4), scl=machine.Pin(5)) # adjust pin numbers as per hardware
tcs = tcs3472(bus)

print("Light:", tcs.light())
print("RGB:", tcs.rgb())
```

## Copyright/Licensing

This project is Copyright (c) 2021 tti0, and is licensed under the MIT License.
