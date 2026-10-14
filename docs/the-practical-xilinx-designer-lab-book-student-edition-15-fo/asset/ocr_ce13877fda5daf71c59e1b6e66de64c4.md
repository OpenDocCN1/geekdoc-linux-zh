**empty** radio button to bring up an empty editor window. Type the following lines into the window if you are using an XS95 Board:

```
NET Hooterville      LOC=p50;
NET Mayberry         LOC=p48;
NET SilerCity        LOC=p47;
NET MtPilot          LOC=p46;
NET Hwy3             LOC=p21;
```

or enter this if you are using an XS40 Board:

```
NET ‘HOOTERVILLE’    LOC=‘p47’;
NET ‘MAYBERRY’       LOC=‘p46’;
NET ‘SILERCITY’      LOC=‘p45’;
NET ‘MTPILOT’        LOC=‘p44’;
NET ‘HWY3’           LOC=‘p25’;
```

(Note that we had to use upper-case letters for the names in the second UCF because the TRIPGENI.SCH schematic only allows upper-case letters for I/O terminal names.)

Then use the **File → Save As...** menu item to save the file as TRIPGENI.UCF. All this UCF does is tell the Foundation Series Implementation tools to assign the 4 city inputs to pins 46, 47, 48 and 50, and to assign the Hwy3 output to pin 21 of the XC95108. We already know from our knowledge of the XS95 Board that pins 46, 47, 48 and 50 can be driven from the PC parallel port while pin 21 drives the bottom-most, horizontal segment of the 7-segment LED. (You can fill in the equivalent pin numbers for the XC4005XL on the XS40 Board.)

Which method of entering pin assignments should you use? If you are only doing designs for one type of board (either the XS40 or XS95 Board), then it is probably easier to embed the pin assignments in the design file. However, if you plan to implement your designs on both boards, then placing the pin assignments in a separate UCF is a cleaner approach. Since the examples in this book are intended for both boards, I will use UCFs exclusively to assign pins.

# Compiling the Logic Design

Once the pin-assignments are entered and we are back in the **Project Manager** window, click on the [toolbar button] or select the **Implementation → Implement Design...** menu item to begin the compilation process. The **Implement Design** window of Figure 2.28 will appear. The **Device and Speed** should mirror what you typed in when you started the project, and the **version and revision** names should be **ver1** and **rev1**, respectively. (You can change any of these if you want.)