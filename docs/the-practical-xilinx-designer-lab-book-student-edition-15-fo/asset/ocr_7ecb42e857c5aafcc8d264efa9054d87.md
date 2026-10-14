However, the Foundation Series Implementation tools that compile the ABEL file, VHDL file, or schematic do not know anything about what FPLD pins are attached to the parallel port or the LED segments. Left on their own, the tools will assign the inputs and outputs of the Trip-Genie to any pins that are convenient. So we need a way to pass our required pin assignments to the Foundation Series tools. There are three ways to do this:

+   1. Embed the pin numbers in the PIN statements of the ABEL file.
+   2. Enter the pin numbers as attributes of the IBUF and OBUF buffers in the schematic.
+   3. Create a separate User Constraint File (UCF) that lists the pin number for each input and output.

Entering the pin numbers right into the ABEL file is very easy. Figure 2.26 shows the TRIPGENI.ABL file with the pin numbers added to allow for testing the design on the XS95 Board.

![](bbox=[0.247, 0.392, 0.889, 0.765])

```
module TRIPGENI
Title 'TRIPGENI'

Declarations

Hooverville PIN 50;
Hayberry    PIN 48;
SilentCity  PIN 47;
MtPilot     PIN 46;
Hwy3        PIN 21 istype 'com';

// <Add your declarations here>

Equations

// <Add your equations here>
Hwy3 = (Hooverville & Hayberry & !Hooverville) &
       (SilentCity & !MtPilot);
end TRIPGENI
```

**Figure 2.26** The TRIPGENI.ABL file with embedded pin assignments.

In the TRIPGENI.SCH schematic, we can double-click on any IBUF or OBUF symbol to set its attributes. For example, double-clicking on the IBUF attached to the Hooverville input terminal brings up the Symbol Properties window of