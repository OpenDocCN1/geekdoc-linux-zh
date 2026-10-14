```
NET SUM<6>    LOC=P57;
NET SUM<7>    LOC=P51;
```

After compiling the design for the XC405XL FPGA, the configuration bitstream for the adder can be downloaded into the XS40 Board like so:

```
C:\XCPROJ\ADD8_40> XSLOAD ADD8_40.BIT
```

Now you can do actual tests with the adder. For example, to add 3 (011) and 3 (011) with the carry input set (1), you would issue the command:

```
C:\XCPROJ\ADD8_95> XSPORT 0110111
```

Then you would expect a result of 7 (111). Therefore, the lower-left, lower-right, and the bottom segments of the 7-segment LED should be on.

# An 8-Bit Adder in VHDL

In this section we will build an 8-bit adder for both the XS95 Board and then the XS40 Board using VHDL and the HDL design flow mode of the Foundation Series software. We will also see how to create our own parts library in VHDL.

Start by creating an HDL mode project called ADD8_95 in the XCPROJ-V directory. Then open an HDL Editor window and create a VHDL file called XSE.VHD which will hold a library of components for use in other designs. For now, XSE.VHD will contain only a single component that is a single-bit full adder (Listing 4.5).

The bottom portion of the XSE.VHD file (lines 21 through 42) is just the ENTITY and ARCHITECTURE sections of the fulladd design we did in chapter 3. The only new feature in this file is the PACKAGE declaration section on lines 8 through 19. Following the PACKAGE keyword is the package name we have chosen (adder) followed by a COMPONENT statement declaring the interface to the fulladd module. This COMPONENT statement has exactly the same form as we used in the EVPAR.VHD file when all the modules were declared in the same file. If there were multiple modules we wanted to place in the adder package, then we would have multiple COMPONENT statements in the PACKAGE section.