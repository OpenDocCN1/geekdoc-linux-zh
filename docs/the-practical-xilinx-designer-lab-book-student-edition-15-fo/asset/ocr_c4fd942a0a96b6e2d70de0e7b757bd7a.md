Pin 16 of J1 is connected to the TMS input (pin 17) of the XC4005XL’s JTAG port. Pins 14 and 17 of J1 also connect to the TCK and TDI inputs of the JTAG port, since TCK is connected to CCLK and TDI is connected to DIN (as described in the previous subsection). These pins are used to download data into the 32 KByte RAM.

Pins 2-9 of J1 are used to apply test signals to the FPGA once a new circuit has been downloaded. The signals applied through pins 2-9 and J1-4 are for use as clock signals for sequential circuitry since they pass through Schmitt-trigger inverters. (The XSPORT program accounts for these inverters.) The other signals can serve as level inputs, but they should not be used as clocks.

![](bbox=[0.444, 0.321, 0.802, 0.811])

The correspondence between the pins of J1, the pins of the XC4005XL FPGA, and the arguments of the XSPORT program are shown in Table A.3.