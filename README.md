# ECE 528/L - Robotics and Embedded Systems Lab
**CSU Northridge**

**Department of Electrical and Computer Engineering**

## GPIO Lab
The GPIO lab interfaces with the following:

* User buttons and LEDs of the TI MSP432 LaunchPad
* PMOD SWT (4 Slide Switches) - [Product Link](https://digilent.com/reference/pmod/pmodswt/start)
* PMOD 8LD (8 LEDs) - [Product Link](https://digilent.com/shop/pmod-8ld-eight-high-brightness-leds/)

## Overview

The lab introduced GPIO programming on the MSP432 LaunchPad. It included configuring pins as inputs/outputs, reading buttons and switches, and using LEDs and the RGB LED.

The PMOD 8LD and PMOD SWT are connected to the header pins of the MSP432 LaunchPad. The MSP432 LaunchPad also uses a 48 MHz clock.

The buttons are configured to be active-low and used the pull-up resistors in the MSP432 LaunchPad. When pressed, the buttons connect to the GND and provides a value of 0V.

The pins are configured by changing the values of the memory-mapped registers. A digital I/O pin can be configured to be either an input or output.

By clearing SEL0 and SEL1 register, it configures the pins as GPIO pins instead of being used for other peripheral functions.
```
PX->SEL0
PX->SEL1
```
By setting DIR register to 1, it decides that the GPIO pin is an output. While setting it to 0, it decides that the pin is an input.
```
PX->DIR
```
The internal resistor can be configured as either a pull-up resistor or pull-down resistor. 

By setting the REN register to 1, it enables the pin's internal resistor
```
PX->REN
```
By setting the OUT register to 1, it chooses that the internal resistor is a pull-up resistor.

```
PX->OUT
```
The following design showcases the required behavior for the components. 
The design uses the button to turn the LED and RGB LED in the MSP432 LaunchPad as well as the LEDs in the PMOD 8LD. Several functions were implemented in the program to highlight different patterns on the PMOD 8LD depending on which switch is enabled. 

When SWT1 is enabled while the other switches are not, an 8-bit binary up counter is displayed on the PMOD 8LD module that counts down from 0 to 255.

When SWT2 is enabled while the other switches are not, an 8-bit binary down counter is displayed on the PMOD 8LD module that counts down from 255 to 0.

When SWT3 is enabled while the other switches are not, an 8-bit ring counter is displayed on the PMOD 8LD. The function turns on the LED for the least significant bit then shifts to the left until it wraps back to the original position.

When SWT4 is enabled while the other switches are not, an 8-bit ring counter is displayed on the PMOD 8LD. However, the function turns on the LED for the most significant bit then shifts to the right and wraps back to to the original position.

When SWT0 and and SWT1 are enabled while the other switches are not, it implements a Johnson counter in the PMOND 8LD. It starts the sequence at all zeroes and updates the patter nby shifting left by one bit and inserting the inverted previous MSB into Bit 0.

The functions included a delay rate specified in the lab document. The document also had specific behavior for the LEDs and RGB led depending on which switches are enabled or disabled. It is included in the design as well.

## Components Used:

- MSP432 LaunchPad
- USB-A to Micro-USB Cable
- PMOD 8LD
- PMOD SWT

## Known Issues/Limitations

No known issues/limitations were encountered during the lab.

## Author Contribution

Gil connected the PMOD 8LD and PMOD SWT to the MSP432 LaunchPad. He also modified the program to fit the needs of the lab.

Michael helped with the code needed to implement the counters to the PMOD 8LD.

## References

None