Figure 2.27. The following steps assign this input buffer to a pin 47 of the XC4005XL FPGA:

+   1. Click in the Name box and type LOC.
+   2. Click in the Description box and type p47.
+   3. Click the Add button.
+   4. Click OK.

You can repeat this procedure to assign the MtPilot, SilerCity, and Mayberry inputs to pins 44, 45, and 46, respectively, and to assign the Hwy3 output to pin 25.

![](bbox=[0.38, 0.35, 0.78, 0.78])

Figure 2.27 Setting the pin assignment attribute for the Hooterville IBUF in the Trip-Genie schematic.

Finally, we can use the HDL Editor to create a UCF (User Constraint File) that assigns the I/O terminals to specific FPLD I/O pins. In the Flow tab of the Project Manager window, click on the button and then click on the create