That is all the internal wiring. Now we can connect the I/O terminals. First, create a CIN input terminal and wire it to the input of the IBUS module. Then create an output terminal named COUT and wire it to the OBUS module's output. This takes care of getting the carry input into the circuit and getting the carry output out.

We need to use buses to connect the IBUS8 and OBUS8 modules to terminals. Select Mode → Draw Buses and click on the input to the IBUS8 that drives the AIB bus. Move the cursor slightly to the left and double-click to end the bus. In the Edit Bus window that appears, type A in the Bus Name field since this is where the A operand will enter the circuit. Then set the upper and lower bounds of the bus range to 7 and 0. Select Input as the I/O Marker. Then click OK to finish the creation of the I/O bus. A bold input terminal symbol labeled A[7:0] will appear which is connected to the input of the IBUS8 module. Repeat this process to create a B[7:0] bus connected to the second IBUS8 module.

For the output of the adder, click on the output of the OBUS8 module, move the cursor slightly to the right, and double-click. Set the bus name to be SUM and select Output as the I/O Marker. Then click OK and the SUM[7:0] set of output terminals will appear.

Figure 4.14 and Figure 4.15 are the top and bottom portions of the final schematic for the 8-bit adder after all the bus connections are completed.

Save the schematic once it is finished. Then use the Options → Create Netlist, Options → Integrity Test, and Options → Export Netlist... menu items to create, check, and export the netlist (in EDIF 200 format) for the 8-bit adder. Then close the Schematic Editor window.

At this point, we can do a simulation of the 8-bit adder to see if it works. Click on the button to start the simulator. Use the Signal → Add Signals... menu item to add the A bus, B bus, SUM bus, and CIN and COUT signals to the Waveform Viewer window (see Figure 4.16).

The A and B inputs are displayed as buses, but we will need to assign individual input lines to bits of the binary counter in the Stimulator Selection window. Therefore, we need to expand the buses into their individual signals. Click on the A bus name in the Waveform viewer and then select Signal → Bus → Flatten. This lets you see the individual bus signals. Repeat the process for the B bus.

Now open the Stimulator Selection window. We will attach the lower bits of both the A and B inputs to the binary counter. Click on A0 in the Waveform Viewer and then on Bc0 of the binary counter in the Stimulator Selection window. Then click on B0 in the Waveform Viewer and on Bc1 in the Stimulator Selection window. Repeat this process for A1, B1, A2, and B2