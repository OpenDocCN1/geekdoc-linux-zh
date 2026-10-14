```
NET cents0    LOC=P21;  # S0 LED segment
NET cents5    LOC=P23;  # S1 LED segment
NET cents10   LOC=P19;  # S2 LED segment
NET cents15   LOC=P17;  # S3 LED segment
NET cents20   LOC=P18;  # S4 LED segment
NET cents25   LOC=P14;  # S5 LED segment
```

The BIT or SVF file can also be downloaded to the XS40 or XS95 Board, respectively, and tested via the PC parallel port. The outputs of the DFFs which store the current state are connected to the segments of the LED digit. This gives a visual indication of the state of the drink machine after each operation. You can step the state machine through its paces using combinations of the following command sequences. Each sequence activates a particular input and then sends a rising clock edge to the drink dispenser controller.

| Customer Input | XSPORT Command Sequence |
|---|---|
| Reset | XSPORT 111110
XSPORT 111111
XSPORT 111110 |
| Put in a nickel | XSPORT 000010
XSPORT 000011
XSPORT 000000 |
| Put in a dime | XSPORT 000100
XSPORT 000101
XSPORT 000000 |
| Get money returned | XSPORT 001000
XSPORT 001001
XSPORT 000000 |
| Get Swill | XSPORT 010000
XSPORT 010001
XSPORT 000000 |
| Get Krunk | XSPORT 100000
XSPORT 100001
XSPORT 000000 |

# The Drink Dispenser Controller Revisited

If you were looking carefully, you would have noticed a problem in the simulation waveforms shown in Figure 7.13: the RET_DIME output that causes a dime to be returned is active during the 36-40 ns period. This occurs when a dime is entered by the rising clock edge at 36 ns and this causes the machine to move immediately from the 15¢ state to the 25¢ state with the DIME input still active until the 40 ns mark. The state machine sees the logic 1 is still