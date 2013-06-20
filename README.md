# AS5048B Breakout Board
## Description
This is a printed circuit board to break out the [AS5048B](http://www.ams.com/eng/Products/Magnetic-Position-Sensors/Rotary-Magnetic-Position-Sensors/AS5048B) rotary encoder to a four-pin I2C connection. This chip returns a 14-bit absolute radial position. The PCB also provides holes for two alignment pins, the CAD for which is given in AS5048B_Encoder_Board.dxf.

##Usage
### Mechanical
The AS5048B reads the absolute radial position of a diametrically polarized magnet which rotates above the center of the chip (center marked by yellow 'X' in dxf). Many magnet configurations can be used, we have found success with a 3mm diameter N52 magnet positioned 2mm away from the die surface of the chip. More detailed application notes are available in the [datasheet](http://www.ams.com/eng/content/download/250006/975176/143016)
### Electronics
The board needs to be populated with the AS5048B, as well as a 10μF 603 surface mount capacitor. There are pads for *SDA* *SCL* *Vcc* and *GND* on the top and bottom of the PCB, for daisy-chaining several boards together. There are pads on the back of the chip for mounting an optional [6-pin Molex connector](http://www.molex.com/molex/products/datasheet.jsp?part=active/5034800600_FFC_FPC_CONNECTORS.xml&channel=Products&Lang=en-US)

Two solder jumpers on the back of the board set the 7-bit I2C address of the chip to be:

        0b10000 A2 A1

Where A1 and A2 are the logical values of the solder-bridged jumpers.
###Code
ams-enc in [imageproc-lib](https://github.com/biomimetics/imageproc-lib) is example code to communicate with the chip. This code uses a blocking read, which is a bit of a faux-pas in a real time loop. For an example of an asynchronous update, see a different version of ams-enc in [my repository.](https://github.com/dhaldane/imageproc-lib)