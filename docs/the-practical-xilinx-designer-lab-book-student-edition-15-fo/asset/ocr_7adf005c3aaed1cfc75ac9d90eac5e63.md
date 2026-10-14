The pin assignments we used in our UCF file leads to the following correspondence between the bitstring passed to XSPORT and the inputs to the Hwy3 circuit:

| String Bit | Hwy3 Input |
|---|---|
| b0 | MtPilot |
| b1 | SilerCity |
| b2 | Mayberry |
| b3 | Hooterville |
| b4 | *** Not Used *** |
| b5 | *** Not Used *** |
| b6 | *** Not Used *** |
| b7 | *** Not Used *** |

The UCF also assigned the Hwy3 output to pin 21 (pin 25) of the XC95108 CPLD (XC4005XL FPGA). This pin is attached to the lower-most, horizontal segment of the 7-segment LED digit (S0). When Hwy3 = 1, then S0 is bright. Otherwise, S0 is dark.

We can use XSPORT with all 16 combinations of inputs to completely test the Hwy3 circuit. Here are the commands you can issue and what the results should be:

| Command | Hooterville | Mayberry | SilerCity | MtPilot | Hwy3 |
|---|---|---|---|---|---|
| XSPORT 0000 | 0 | 0 | 0 | 0 | 0 (dark) |
| XSPORT 0001 | 0 | 0 | 0 | 1 | 0 (dark) |
| XSPORT 0010 | 0 | 0 | 1 | 0 | 0 (dark) |
| XSPORT 0011 | 0 | 0 | 1 | 1 | 0 (dark) |
| XSPORT 0100 | 0 | 1 | 0 | 0 | 0 (dark) |
| XSPORT 0101 | 0 | 1 | 0 | 1 | 0 (dark) |
| XSPORT 0110 | 0 | 1 | 1 | 0 | 1 (bright) |
| XSPORT 0111 | 0 | 1 | 1 | 1 | 0 (dark) |
| XSPORT 1000 | 1 | 0 | 0 | 0 | 0 (dark) |
| XSPORT 1001 | 1 | 0 | 0 | 1 | 0 (dark) |
| XSPORT 1010 | 1 | 0 | 1 | 0 | 1 (bright) |
| XSPORT 1011 | 1 | 0 | 1 | 1 | 1 |
| XSPORT 1100 | 1 | 1 | 0 | 0 | 0 (dark) |
| XSPORT 1101 | 1 | 1 | 0 | 1 | 0 (dark) |
| XSPORT 1110 | 1 | 1 | 1 | 0 | 0 (dark) |
| XSPORT 1111 | 1 | 1 | 1 | 1 | 0 (dark) |