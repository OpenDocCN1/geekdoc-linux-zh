In this example, you invoke bc and set scale to 4, meaning that you want it to calculate any fraction to four decimal places. You ask it to calculate 8/3, which gives 2.6666 and then a more complex calculation. Note that spaces are optional. Finally you enter quit to return to the shell prompt, bc can handle addition (+), subtraction (-), multiplication (*), division (/), remainder or modulo (%), and integer exponentiation (^). It can accurately compute some numbers of any size

```
9238472938742937 * 29384729347298472
27147092868732339864748626982264
```

and we can be used in shell variable assignment to assign calculated values to variables:

```
AVERAGE=`echo "scale=4; $PRICE/$UNITS" | bc`
```

The echo command is used here to print directives that are piped to bc. The first directive sets the scale to 4; the second directive is a division operation. These directives are piped to bc, which does the calculations and returns the result. The backquotes allow the result from bc to be stored in the variable AVERAGE.

You can also convert between different number bases using bc:

```
bc
ibase=16
obase=8
400
100
77
2F
10*3
18
quit
$
```

obase=16 sets the output base to hexadecimal; ibase=8 sets the input base to octal. It is important to set the output base first. First you enter 400. It shows an octal 400 is a hex 100. Next you enter 77. It shows an octal 77 is a hex 3F. Then you multiply 10 and 3, which equals 24 because 10 octal is 8 in decimal and 8*3 is 24. However, because the output base is hex, bc converts 24 in decimal to hex, which gives 18 as the reported result.

# Summary

In this chapter, you learned about several miscellaneous tools:

+   - eval
+   - :
+   - type