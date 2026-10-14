# Figure 4.20 The xse library has been created in the ADD8_95 HDL mode project.

Now we have to add VHDL source files to the xse library, so right-click on and select Add Source Files to "xse" from the pop-up menu that appears. This will cause an Add Document window to come into view. Select the XSE.VHD file and click on Open. The XSE.VHD file will be added to the library and the Project Manager window will appear as in figure 4.21.

Now we can create the top-level VHDL file that describes an 8-bit adder using the fulladd module from the xse library. Listing 4.6 shows this VHDL code which is stored in the BYTEADD.VHD file.

The first major difference in this file is that the xse library is appended to the LIBRARY statement on line 4 Then the USE statement on line 6 gives the rest of the file access to all the components of the adder package of the xse library.

![](bbox=[0.32, 0.07, 0.88, 0.6])