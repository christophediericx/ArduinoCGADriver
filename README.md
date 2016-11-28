# ArduinoCGADriver
Drive a CGA screen directly from an Arduino (UNO) without any additional hardware. The code implements a monochrome green 100x70 resolution and framebuffer. More information can be found [in this blog post](http://www.diericx.net/post/drive-cga-screen-with-arduino/).

![ArduinoCGADriver](https://github.com/christophediericx/ArduinoCGADriver/blob/master/Images/CGADriver.png)

> *Compatibility note: This library has only been tested with an UNO (ATMega328P based) Arduino board.

## Wiring the CGA Connector ##

Wiring the Arduino to the CGA connector is very straighforward. The CGA pinout  has 9 pins in total: 2 grounds (GND), 1 reserved pin, Hsync, VSync and seperate pins for R, G, B and I (intensity).

Wire digital 8 to GREEN, digital 9 to RED, digital 10 to BLUE, digital 11 to HSync, digital 12 to VSync. Wire a direct 5V connection to Intensity. Connect GND to GND.



