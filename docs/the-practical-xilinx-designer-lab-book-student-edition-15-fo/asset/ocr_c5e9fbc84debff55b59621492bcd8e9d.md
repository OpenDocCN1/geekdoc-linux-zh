# Entering the Design Using the ABEL Hardware Description Language

In this section, I will show you how to enter the design for the Hwy3 output of the Trip-Genie using the ABEL HDL. (Go to the following section to see how the design is entered using the schematic editor.) ABEL is a simple design language that has matured and evolved as programmable logic progressed from PALs, PLAs, and SPLDs to FPLDs.

In the Project Manager window, select "Tools → Design Entry → HDL Editor" (or click on the button in the Flow tab of the Project Manager window). In the window that appears, click on the radio-button labeled Use HDL Design Wizard and then click on OK. Then click on Next in the Design Wizard window that appears to reach the Design Wizard-Language window. Here, select the ABEL radio-button and click on Next to move to the Design Wizard-Name window. Enter TRIPGENI as the name and click Next.

Now we should be in the Design Wizard-Ports window where we specify the inputs and outputs for our design (Figure 2.12). To add an input, click on New and then type Hooterville (for example) in the Name field. Click on the Input radio-button to set the port to be an input. Repeat these steps for the Mayberry, SilerCity, and MtPilot inputs.

![](bbox=[0.28, 0.58, 0.92, 0.9])

Figure 2.12 Adding inputs and outputs to the TRIPGENI design.