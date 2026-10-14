Finally, the value on the output bus is passed to an LED decoder module on line 77. This allows the display of the 4-bit output value as a hexadecimal digit on the LED display.

Simulated waveforms of the small memory’s operation are shown in Figure 8.18. The design was targeted for an XC95108 CPLD. Four writes were made to the memory by applying an address and data value and then pulsing the WEB input low. During the interval 0–110 ns the hex values of 0xC, 0x5, 0x5, and 0xA were written to memory locations 0, 1, 2, and 3, respectively. Then the values were read back out of these locations between 120 ns and 160 ns. Note that the value read from each location matches the data that was written to it. The output enable is lowered at 160 ns and the output bus tristates to the Z state.

![](bbox=[0.234, 0.331, 0.908, 0.517])

**Figure 8.18**  Simulated waveforms for an asynchronous memory.

The following constraints are used to map the I/O of the ABEL version of the MEM1 design to the pins of the XC95108 CPLD on the XS95 Board:

```
NET WEB   LOC=P46;   # B0 argument of XSPORT
NET OE    LOC=P47;   # B1 argument of XSPORT
NET A0    LOC=P48;   # B2 argument of XSPORT
NET A1    LOC=P50;   # B3 argument of XSPORT
NET INP0  LOC=P51;   # B4 argument of XSPORT
NET INP1  LOC=P52;   # B5 argument of XSPORT
NET INP2  LOC=P81;   # B6 argument of XSPORT
NET INP3  LOC=P80;   # B7 argument of XSPORT
NET S0    LOC=P21;   # S0 LED segment
NET S1    LOC=P23;   # S1 LED segment
NET S2    LOC=P19;   # S2 LED segment
NET S3    LOC=P17;   # S3 LED segment
NET S4    LOC=P18;   # S4 LED segment
NET S5    LOC=P14;   # S5 LED segment
NET S6    LOC=P15;   # S6 LED segment
```