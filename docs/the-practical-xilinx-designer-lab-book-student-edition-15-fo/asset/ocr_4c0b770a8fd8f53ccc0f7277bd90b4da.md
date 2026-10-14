# Figure 4.2 Construction of a parity generator.

# Listing 4.1 ABEL description of a 2-bit even-parity generator.

```
001- MODULE evpar2
002- INTERFACE (b0,b1)->par;"define interface
003- TITLE '2-bit even-parity generator'
004- DECLARATIONS
005- b1..b0 PIN;"declare interface pins
006- par PIN ISTYPE 'COM';
007- EQUATIONS
008- par = b1 $ b0;      "just a simple XOR
009- END evpar2        "end 2-bit parity module
```

actually declared in lines 5 and 6 following the DECLARATIONS keyword. The Boolean equation on line 8 XORs the b0 and b1 inputs and outputs the parity on the odd output. (The output is called odd because it goes to a logic one if the inputs have odd parity. The total combination of input bits and the output

![](bbox=[0.22, 0.05, 0.45, 0.25])

![](bbox=[0.55, 0.05, 0.85, 0.25])

![](bbox=[0.35, 0.3, 0.78, 0.6])