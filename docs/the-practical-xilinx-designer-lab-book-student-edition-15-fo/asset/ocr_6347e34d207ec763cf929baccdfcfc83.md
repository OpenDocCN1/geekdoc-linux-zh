to COUT The shorter names will be easier to display when we use these modules to build larger adders.

+   2. Bypass each IBUF and OBUF buffer with a wire that connects its input to its output.

+   3. Remove the IBUF and OBUF buffers. Since we are going to encapsulate the 1-bit adder into a module, we do not necessarily want the module's I/O to be attached to pins of the CPLD. Notice that the I/O terminal will disappear along with the buffer if you did not wire the buffer's input to its output. That is the reason for the previous step.

Once you have completed all these steps, your schematic should look like Figure 4.9. Next, we have to create a symbol to represent the 1-bit adder for when we use it in other schematics. To do this, select the Hierarchy → Create Macro Symbol from Current Sheet menu item. The Create Symbol window shown in Figure 4.10 will appear. Type the name by which you want to refer to the 1-bit adder module into the Symbol Name field (I chose MY_ADD1, but you might want to be more creative). You can also enter a phrase into the Comment field to reference the function of this module. Then click on OK. Then you will be informed that MY_ADD1 has been added to the list of symbols and asked if you want to modify the symbol for MY_ADD1. Just click on No.

![](bbox=[0.38, 0.59, 0.88, 0.86])

Figure 4.9 ADD1.SCH modified for encapsulation into a module (compare with Figure 3.13).