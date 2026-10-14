# Listing 8.3  ABEL version of a 4-bit wide synchronous memory built from 4 register modules.

```
001- MODULE MEM2
002- TITLE 'A 4x4 synchronous memory built from DFFs'
003-
004- DECLARATIONS
005-
006- WEB        PIN;              "active-low write-enable input
007- CLK        PIN;              "clock input
008- A1..A0     PIN;              "2-bit address inputs
009- INP3..INP0 PIN;              "4-bit input data bus
010- RGA3..RGA0 NODE ISTYPE 'REG'; "first 4-bit register
011- RGB3..RGB0 NODE ISTYPE 'REG'; "second 4-bit register
012- RGC3..RGC0 NODE ISTYPE 'REG'; "third 4-bit register
013- RGD3..RGD0 NODE ISTYPE 'REG'; "fourth 4-bit register
014- OUTP3..OUTP0 PIN ISTYPE 'COM'; "4-bit output data bus
015- S6..S0     PIN ISTYPE 'COM';   "LED driver outputs
016-
017- A   = [A1..A0];       "synonym for the address bus
018- INP = [INP3..INP0];   "synonym for input bus
019- OUTP = [OUTP3..OUTP0]; "synonym for output bus
020- RGA = [RGA3..RGA0];   "synonym for first register
021- RGB = [RGB3..RGB0];   "synonym for second register
022- RGC = [RGC3..RGC0];   "synonym for third register
023- RGD = [RGD3..RGD0];   "synonym for fourth register
024- S   = [S6..S0];       "synonym for LED drivers
025- W0  = ((A==0) & !WEB); "write signal for first register
026- W1  = ((A==1) & !WEB); "write signal for second register
027- W2  = ((A==2) & !WEB); "write signal for third register
028- W3  = ((A==3) & !WEB); "write signal for fourth register
029-
030- EQUATIONS
031-
032- "write signal for each register controls multiplexer which
033- "directs input bus or register contents back into register
034- RGA := W0 & INP # !W0 & RGA;
035- RGB := W1 & INP # !W1 & RGB;
036- RGC := W2 & INP # !W2 & RGC;
037- RGD := W3 & INP # !W3 & RGD;
038-
039- RGA.CLK = CLK; "all registers get the same clock
040- RGB.CLK = CLK; "so the entire memory is synchronous
041- RGC.CLK = CLK;
042- RGD.CLK = CLK;
043-
044- "a simple address decoder that passes the value from
045- "one of the registers to the output bus
046- WHEN        (A==0) THEN OUTP=RGA;
047- ELSE WHEN   (A==1) THEN OUTP=RGB;
048- ELSE WHEN   (A==2) THEN OUTP=RGC;
```