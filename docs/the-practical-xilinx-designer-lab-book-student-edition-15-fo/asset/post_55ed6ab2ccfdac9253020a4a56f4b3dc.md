
Once you have completed entering the VHDL code into the HDL Editor window, you can use the Synthesis → Check Syntax menu item to look for errors. Close the HDL Editor window after correcting any errors. Select the Document → Add menu item in the Project Manager window to add the EVPAR.VHD file to the project. Then click on the button in the Flow tab of the Project Manager window. The Synthesis/Implementation window will appear as usual, but there is a difference. You now have a hierarchical description of a logic design and you need to tell the Foundation Series synthesis software which module is at the top of the hierarchy. To do this, click on the Top Level drop-down menu in the Synthesis/Implementation window and a list of all the modules in the EVPAR.VHD file will appear (Figure 4.4). Just select evpar8 as the top level module. You must also target the project to an XC95108 CPLD. Then click on Run to start the synthesis of a netlist for the 8-bit parity generator. Once the netlist is available, you can simulate, compile, download, and test the parity generator on the XS95 Board exactly as I discussed in the previous section. Because of the way the Foundation Series synthesis software formats VHDL I/O array names, you will have to change the format of the EVPAR_95.UCF file to look as follows:

```
NET b<0>      LOC=P46;
NET b<1>      LOC=P47;
NET b<2>      LOC=P48;
NET b<3>      LOC=P50;
NET b<4>      LOC=P51;
NET b<5>      LOC=P52;
NET b<6>      LOC=P81;
NET b<7>      LOC=P80;
NET odd       LOC=P21;# LED segment S0
```

## A Parity Generator for the XS40 Board

The ABEL or VHDL code for the even-parity modules should also work for the XC4005XL FPGA on the XS40 Board. However, when you try to compile the even-parity generator for the XS40 Board using the following user-constraints:

```
NET b0   LOC=P44;
NET b1   LOC=P45;
NET b2   LOC=P46;
NET b3   LOC=P47;
NET b4   LOC=P48;
NET b5   LOC=P49;
NET b6   LOC=P32;
NET b7   LOC=P34;
NET odd  LOC=P25;
```

![](img/5124daf79d2807d81e49f49c22f1f8c1_125_0.png)

Figure 4.4 Selecting the top-level module of a hierarchical VHDL design.

you will get an error message like this from the Foundation Series Implementation tools:

ERROR:baste:262 - Bad format for LOC constraint P34 on symbol 'b7.PAD' (pad signal=b7). No such site for this device. This may also indicate that a non-constrainable site (such as a VCC, GND, mode, configuration, or other special-purpose pin) has been used as a site name.

ERROR:baste:262 - Bad format for LOC constraint P32 on symbol 'b6.PAD' (pad signal=b6). No such site for this device. This may also indicate that a non-constrainable site (such as a VCC, GND, mode, configuration, or other special-purpose pin) has been used as a site name.

The XS40 Board uses M0 and M2 of the XC4000 FPGA (pins 32 and 34, respectively) as dedicated inputs that are driven by the PC parallel port. But M0 and M2 are also special-purpose pins that set the mode of the XC4005XL FPGA when it powers up. The Foundation Series software will not let us specify user-

## Figure 4.5 Adding the even-parity generator symbol to a schematic.

After you have gotten the inputs and outputs connected, just use the Options → Create Netlist, Options → Integrity Test, and Options → Export Netlist... menu items to create an EDIF netlist.

With the netlist generated, we can do a functional simulation. But when we open the Component Selection window to begin selecting signals for the Waveform Viewer window, the B6 and B7 inputs are not found in the Signal Selection pane (see Figure 4.7). They are absent because these inputs are attached to the special-purpose pins. But we need to drive values onto these 2 inputs to provide a full set of 8 input values to the parity generator.

The solution to our problem is to double-click on the U1 - EVPAR8 item in the Chip Selection pane. This places a list of the inputs and outputs for the parity generator module in the right-most pane of the Component Selection window. We can select the B6 and B7 input pins for the module and click on the Add button. These inputs appear as U1.B6 and U1.B7 in the Waveform Viewer window.

Once the inputs and outputs are added, the 8 inputs should be attached to the 8 lowest bits of the binary counter in the Stimulator Selection window. Then click on the button in the Simulator window a few times. This will exercise

![](img/5124daf79d2807d81e49f49c22f1f8c1_127_0.png)
