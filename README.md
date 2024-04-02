Here are some modifications to the Vectrex Core to get XYZ signals out of the RGB VGA port.

![alt text](https://github.com/Jokippo/Vectrex_MiSTer_XYZ/blob/master/Gerber%20and%20STL/helpiamonascope.png?raw=true)

It requires this circuit to attach the VGA port to BNC connectors suitable for an oscilloscope (Gerbers included).

![alt text](https://github.com/Jokippo/Vectrex_MiSTer_XYZ/blob/master/Gerber%20and%20STL/RGB2XZY_Circuit.PNG?raw=true)

While the VGA port only supports 6-bit per channel resolution, this circuit uses PWM in addition to a small capacitor to get the required 10-bit accuracy. This results in a reasonably stable signal. Be aware that the quality of the resulting picture will also depend on the linearity of your I/O Boards resistor DAC.

Use the potentiometers to scale the width and height of the image.

The circuit uses a cheap HW668 voltage booster to produce the 12v required to get sufficient Z channel attenuation on my particular scope (tektronix 2225). With a jumper it is possible to output lower voltages for different scopes, but it doesn't produce negative voltages that some XY monitors might need.
Likewise the X and Y channels only send positive signals, so horizontal and vertical positions will need to be adjusted on the scope. 

A potential future circuit could use level biasing if there are scopes that need it. Also the Z channel is either off or full intensity now, which could be improved as well, although not many games seem to really need this.

![alt text](https://github.com/Jokippo/Vectrex_MiSTer_XYZ/blob/master/Gerber%20and%20STL/RGB2XYZ_OSD.jpg?raw=true)

When the OSD is enabled, the core creates a raster that can scan out the regular VGA signal with the OSD to the oscilloscope. Add this to the mister.ini to output this signal in the right format:

```
[Vectrex]
video_mode=640,40,96,64,480,14,2,31,26430,0,1 ; 640x480@59.7Hz
```

This is not needed if using a seperate hdmi monitor. If not using a hdmi monitor you can use MiSTer's autoboot function to boot directly into the Vectrex core.

You can also directly connect an OPL811-OC sensor to the user port and use it as a lightpen. Included are STLs to make a lightpen. You can make a circuit with some perf board (11.5 x 80 mm).

![alt text](https://github.com/Jokippo/Vectrex_MiSTer_XYZ/blob/master/Gerber%20and%20STL/RGB2XYZ_Pen.jpg?raw=true)
![alt text](https://github.com/Jokippo/Vectrex_MiSTer_XYZ/blob/master/Gerber%20and%20STL/LightpenCircuit.jpg?raw=true)

Connect the sensor to D+/5v/ground and the button to D-/ground of a usb plug.

![alt text](https://github.com/Jokippo/Vectrex_MiSTer_XYZ/blob/master/Gerber%20and%20STL/RGB2XYZ_Case.jpg?raw=true)

Without a case the board can be plugged in directly to the vga port(not recommended). With the case (STL included) a short (30 cm or less) male to female vga cable is needed, make sure it supports the v5 pin as some cables don't have this (and the 5v output on the I/O board also needs to be enabled). 

Added options in the OSD:
```
XYZ over RGB: enables XYZ output
Rotate: rotate image
Lightpen: enables the lightpen and sets the core to use the lightpen button instead of the controller.
Lightpen Button: select which button in used for the lightpen button.
OSD Contrast: increase if OSD output is too dim.
```

Parts:
```
2x 2.2nF Capacitor 0603
1x 100uF Capacitor 1206
2x 100 Ohm Resistor 0603
2x 150 Ohm Resistor 0603
1x 10 Ohm Resistor 0603
1x 1.5 kOhm Resistor 1206
3x 10 kOhm 3296 type potentiometer
1x KST10MTF transistor
1x HW668 voltage booster 23x16mm (may not be needed depending on your scope, set jumper to position 1-2 for 5v, 2-3 for booster)
3x CONBN002 BNC Connector
1x 10090926-P154XLF VGA Connector
```
Lightpen:
```
1x OPL811-OC
1x 6x6mm tactile button
```


