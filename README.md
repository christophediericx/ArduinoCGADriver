# ArduinoCGADriver
ArduinoCGADriver is an Arduino sketch that drives a CGA screen directly from an Arduino (UNO) without any additional hardware. The code implements a (currently only monochrome - green) 100x70 resolution / framebuffer.

![ArduinoCGADriver](https://github.com/christophediericx/ArduinoCGADriver/blob/master/images/ArduinoCGADriver.png)

> *Compatibility note: This library has only been tested with UNO based Arduino boards.

## Wiring the CGA Connector ##

Wiring the Arduino to the CGA connector is very straighforward. The CGA pinout  has 9 pins in total: 2 grounds (GND), 1 reserved pin, Hsync, VSync and seperate pins for R, G, B and I (intensity).

Wire digital 8 tp GREEN, digital 9 to RED, digital 10 to BLUE, digital 11 to HSync, digital 12 to VSync. Wire a direct 5V connection to Intensity. Connect GND to GND.

## Timing and resolution ##

Our general signal timing has to be spot-on in order to be stable, so we'll carefully line up instructions. We definitely also need to disable interrupts.

CGA has a horizontal frequency of around 15Khz (there is a tolerance for timings which are ~close~). We will have to be able to emit a single horizontal line in approximately 67μs. Since the Arduino runs at 16Mhz (with a single instruction taking 62.5ns), we have approximately only 1072 CPU cyles to work with per line (67μs / 62.5 ns).

In a horizontal signal, our "left blanking and overscan" phase will take 71 cycles (approximately 4.43μs).

Next we'll emit 100 pixels at 8 instructions each (for a total duration of 50μs).

The "right overscan and blanking" phase will be timed to take 115 cycles (7.18μs).

After that we'll pull HSync high for around 71 cycles (4.43μs).

Because we can only emit 100 pixels horizontally (and have less of a timing constraint vertically) we'll basically emit three identical horizontal lines in a row (resulting in a vertical resolution of '70'.

## Framebuffer ##

The main constraint here is the Arduino's RAM size. The current version (implementing a green monochrome buffer @ 1 bit per pixel) uses 700 bytes of precious SRAM already. 8 colors are easy to achieve on the RGBI connection, but implementing any reasonable resolution is hard (since we would need 3 bits per pixels stored).

It should be fairly easy to change the code to emit 4 colors though (2 bits per pixel, a 1400 byte framebuffer for 100x70).



