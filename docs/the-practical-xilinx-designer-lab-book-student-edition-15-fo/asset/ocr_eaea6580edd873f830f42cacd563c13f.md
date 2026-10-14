![](bbox=[0.306, 0.067, 0.921, 0.394])

Figure 8.22  Using the built-in synchronous dual-port memory of the XC4005XL FPGA.

```
NET S4    LOC=P23;    # S4 LED segment (for DP00)
NET S5    LOC=P18;    # S5 LED segment (for DP01)
```

The following command sequences perform the indicated operations:

| Action | XSPORT Command Sequence |
|---|---|
| Write location 1 (01) with 3 (11) while reading from location 2 (10) | XSPORT 10011110 |
| Write location 0 (00) with 2 (10) while reading from location 1 (01) | XSPORT 01001011 |
| Read locations 0 (00) and 1 (01) | XSPORT 00010001 |
| Read location 3 (11) and 2 (10) | XSPORT 11100001 |

Using the internal RAMs, the asynchronous memory consumes only 13 LUTs (most of which are used in the LED decoder) while the dual-port synchronous design takes up 4 LUTs. This is quite a reduction in LUT usage when compared to the flip-flop-based designs of the previous sections.

# Using a Memory Chip

Even the internal RAMs of the XC4000 FPGAs will not suffice when you need a large amount of memory. Connecting external memory chips to the pins of an