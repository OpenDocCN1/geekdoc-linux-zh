the parity generator for all possible input combinations. The waveforms should resemble those of Figure 4.3.

Before compiling the design, place the following constraints in the EVPAR_40.UCF constraint file:

```
NET B0    LOC=P44;
NET B1    LOC=P45;
NET B2    LOC=P46;
NET B3    LOC=P47;
NET B4    LOC=P48;
NET B5    LOC=P49;
# NET B6  LOC=P32;
# NET B7  LOC=P34;
NET ODD   LOC=P25;# LED segment SO
```

The constraints for inputs B6 and B7 are commented-out so they have no effect (I just left them in there so I would not forget that these inputs were still being used). Note also that all the input and output names have been converted to upper-case since the I/O terminals in a schematic always have upper-case names.

After compiling the even-parity generator with the user-constraint file shown above, we can open the Place&Route report file and find the following information:

| Device utilization summary: |
| IO | 7/112 | 6% used |
|  | 7/61 | 11% bonded |
| LOGIC | 1/196 | 0% used |
| SPECIAL | 2/1167 | 0% used |
| IOB | 7/112 | 6% used |
| CLB | 1/196 | 0% used |
| MODE0 | 1/1 | 100% used |
| MODE2 | 1/1 | 100% used |

The last two lines indicate we were successful in our attempt to use the M0 and M2 special purpose pins as inputs.

The configuration bitstream for the even-parity generator can be downloaded into the XS40 Board like so:

```
C:\XCPROJ\EVPAR_40> XSLOAD EVPAR_40.BIT
```