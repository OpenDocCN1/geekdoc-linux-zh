```
22  [.C.] -> [ 3, 3];
23  [.C.] -> [ 4, 6];
24  [.C.] -> [ 5, 10];
25  [.C.] -> [ 6, 15];
26  [.C.] -> [ 7, 21];
27
28  END
```

The beginning of this design (as for all ABEL designs) defines the module name. Following the module name are the declarations of the module. On line 3, the clock input is defined. On line 4, the nodes that will contain the information for x are declared as an 8-bit register. Line 5 declares the output pins for total, an 8-bit register. On line 7 and 8, the 8 bits are renamed to a single variable name, allowing the equations to be written quickly and clearly. Line 10 is an ABEL compiler directive which limits the lookahead carry chain of the adder to 4 bits. On line 12, the EQUATIONS keyword signifies the end of the Declarations section and the beginning of the logic descriptions.

Every register must have a clock associated with it and in this design, line 13 specifies that the x and total registers are clocked by the input myclock. The actual logic assignments on lines 15 and 16 determine how the registers are affected when myclock goes high. At the rising clock edge, x (after clock) will get the value of x (before clock) + 1, and total (after clock) will get the value of total (before clock) + x (before clock). Figure B.2 shows a block diagram of the circuit described by this code.

![](bbox=[0.429, 0.55, 0.783, 0.831])

**Figure B.2**  Block Diagram