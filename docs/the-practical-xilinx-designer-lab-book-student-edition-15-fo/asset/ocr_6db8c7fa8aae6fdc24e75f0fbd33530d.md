# Table 3.8 Truth-table for a 2-bit adder with carry input and output.

| Input1 | Input0 | Carry Input | Sum Output | Carry Output |
|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 | 0 |
| 0 | 1 | 0 | 1 | 0 |
| 0 | 1 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 | 0 |
| 1 | 0 | 1 | 0 | 1 |
| 1 | 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 1 | 1 |

![](bbox=[0.38, 0.35, 0.78, 0.58])

# Figure 3.11 Logic circuitry for a 1-bit adder.

# Experimental

# 1-Bit Adder for the XS40 Board

Let's build the 1-bit adder using schematics for both the XC4005XL and the XC95108. First, create a schematic mode project called ADD1_40 that will hold the design for the XC4005XL (Figure 3.12).

Start the schematic editor and connect the gates as shown in Figure 3.11. Figure 3.13 shows the 1-bit adder with the additional input and output buffers.

Once the schematic is complete, save it as ADD1.SCH. Then generate a netlist using the Options → Create Netlist menu item and export it in EDIF 200 format using the Options → Export Netlist... menu item. (You can also activate the Options → Integrity Test to make sure everything is OK before you move on.) Then exit the schematic editor.

Now let's do a simulation to make sure the adder is functioning correctly. Click on the button in the Flow tab of the Project Manager window. Within the simulator, use the Signal → Add Signals... menu item to add the input