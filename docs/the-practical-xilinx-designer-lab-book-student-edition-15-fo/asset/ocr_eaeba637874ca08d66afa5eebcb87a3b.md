effectively making ripple-carry adders. Without this statement, the logic synthesis tools will try to create carry look-ahead circuitry for all 7 bits of the PC incrementer and the 5 bits of the ALU adder.

The GNOME1.ABL file should compile successfully for the XC95108 CPLD. The utilization of the XC95108 is:

| Design Name | Device | Macrocells Used | Product Terms Used | Pins Used |
|---|---|---:|---:|---:|
| gnom1_95 | XC95108-20-PC84 | 75/108 (69%) | 230/540 (42%) | 35/69 (50%) |

You can see that there are 33 macrocells and 310 product terms left free in the CPLD. After limiting the carry chain length, the equivalent statistics when GNOME is mapped to the XC4005 FPGA are:

# Design Summary

| Metric | Value |
|---|---:|
| Number of errors | 0 |
| Number of warnings | 3 |
| Number of CLBs | 116 out of 196 (59%) |
| CLB Flip-Flops | 23 |
| CLB Latches | 0 |
| 4 input LUTs | 213 |
| 3 input LUTs | 34 |
| Number of bonded IOBs | 35 out of 65 (53%) |
| IOB Flops | 0 |
| IOB Latches | 0 |
| Total equivalent gate count for design | 1524 |

The GNOME1.ABL file can be compiled for the XS95 Board using these pin assignment constraints:

```
NET clock    LOC=P46;
NET reset    LOC=P47;
NET csb      LOC=P65;
NET web      LOC=P63;
NET oeb      LOC=P62;
NET data0    LOC=P44;
NET data1    LOC=P43;
NET data2    LOC=P41;
NET data3    LOC=P40;
NET data4    LOC=P39;
NET data5    LOC=P37;
NET data6    LOC=P36;
NET data7    LOC=P35;
NET addr0    LOC=P75;
```