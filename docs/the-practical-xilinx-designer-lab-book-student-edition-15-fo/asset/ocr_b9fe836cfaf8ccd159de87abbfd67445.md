and then issue the command:

```
XSLOAD TRIPG_40.BIT
```

to download the Hwy3 circuit into the XC4005XL FPGA on the XS40 Board.

Upon completion of the XSLOAD command, the XS95 or XS40 Board will be programmed with the Hwy3 logic.

# Testing the Downloaded Logic Design

Now we need to force the inputs to various logic levels to see if the Hwy3 circuit we downloaded to the XS95 or XS40 Board is working. The XSPORT program accepts a string of 1 and 0 bits and outputs it on the 8 data pins of the parallel port that are connected to pins of the XC95108 CPLD (XC4005XL FPGA) on the XS95 Board (XS40 Board). Given the command

```
XSPORT b₇b₆b₅b₄b₃b₂b₁b₀
```

where b₇–b₀ represent binary bits, the correspondence between the bits in the string and the pins on the XC95108 or XC4005XL is as follows:

| String Bit | XC95108 Pin | XC4005XL Pin |
|---|---|---|
| b₀ | 46 | 44 |
| b₁ | 47 | 45 |
| b₂ | 48 | 46 |
| b₃ | 50 | 47 |
| b₄ | 51 | 48 |
| b₅ | 52 | 49 |
| b₆ | 81 | 32 |
| b₇ | 80 | 34 |

XSPORT sets the most significant bits to zero if it is given fewer than 8 bits. If XSPORT is given more than 8 bits, it keeps only the 8 least-significant bits.