
![](img/5124daf79d2807d81e49f49c22f1f8c1_262_0.png)

### Figure 7.20 Beginning screen for the CNT3SE_4 design.

![](img/5124daf79d2807d81e49f49c22f1f8c1_262_1.png)

### Figure 7.21 Adding the 3 states for the CNT3SE_4 design.

### Figure 7.22 Adding state transitions for the CNT3SE_4 design.

in the drawing area. A box will appear in which you can type the Boolean equation that expresses when this transition should be taken. (You have to write the expressions using ABEL or VHDL operators depending upon which HDL you selected.) After typing in the expression, you can use the mouse to move the text to a convenient spot near the arrow. Figure 7.23 shows our state machine after all the transitions have been labeled with conditions.

![](img/5124daf79d2807d81e49f49c22f1f8c1_264_0.png)

### Figure 7.23 Labeling the state transitions with conditions.

Even though the transition conditions include the RESET input, it is always a good idea to include an explicit reset condition. Select the FSM → Reset menu item (or click on the button) and drop the triangular reset symbol into the drawing area. Then connect it with a transition arrow to the state that should be entered when a reset occurs (this is the reset state). Label the transition with a Boolean expression which, if true, will cause the state machine to enter the reset state. You can click the right mouse button on the reset symbol to select whether the reset is asynchronous or synchronous. The state machine with an explicit, synchronous reset is shown in Figure 7.24.

![](img/5124daf79d2807d81e49f49c22f1f8c1_265_0.png)

### Figure 7.24 Adding a reset to the state machine.

> (Given that an explicit reset has been added to the state machine, do we really need to include the RESET input in all the other state transition conditions? The answer is no. The only reason I have kept the more complicated expressions is to keep this example close to the state machine diagram in Figure 7.6.)

Finally, we have to set the actions that will occur in each state. In this example, the only action is to set the value that will appear on the outputs. Select the **FSM → Action → State** menu item (or use the ![button](icon) button) and then click on one of the states. A text box connected to the state circle will appear. You can type an expression for the two outputs in this box. (For example, in state S0 the outputs should both be zero so I entered the ABEL statement OUTPUT=^b00.) Then you can move the box with the text to a convenient location. Figure 7.25 shows our state machine after all the states have been labeled with actions.

![](img/5124daf79d2807d81e49f49c22f1f8c1_265_1.png)

### Figure 7.25 Labeling the states with output actions.

After the state machine is drawn, select the **File → Save** menu item. Now we can generate the HDL code that corresponds to our drawing. Select the **Synthesis → HDL Code Generation** menu item to create the ABEL code shown in Listing 7.7. (By now you should be familiar enough with the ABEL’s STATE_DIAGRAM construct to detect the correspondence between the code and the graphical state machine.) Then select the **Synthesis → Synthesize** menu item to generate the netlist from the ABEL code.

At this point, you can use the **Document → Add** menu item in the **Project Manager** window to add either the CNT3SE.ABL file or the CNT3SE.ASF file (which holds the graphical rendition of the counter) to the project. Then you can use the Foundation Series Implementation Tools to compile it for the XC4005XL FPGA or XC9500S CPLD.

### Listing 7.7 ABEL code generated for the CNT3SE state machine.

```abel
001- "*
002- "* File: L:\xcproj\CNT3SE_9\Cnt3se.abl
003- "* created:09/23/98 14:17:30
004- "* from: 'L:\xcproj\CNT3SE_9\Cnt3se.asf'
005- "* by: fsm2hdl - version: 2.0.1.49
006- "*
007- module cnt3se
008- Title 'cnt3se'
009-
010- Declarations
011-
012- "clocks
013- CLK PIN;
014-
015- "input ports
016- RESET PIN;
017- UP PIN;
018-
019- "output ports
020- OUTPUT1..OUTPUT0 PIN;
021- OUTPUT = [OUTPUT1..OUTPUT0];
022-
023- "******** SYMBOLIC state machine: Sreg0 *****
024- Sreg0 STATE REGISTER;
025- S0, S1, S2 STATE;
026-
027-
028- Equations
029-
030- "diagram ACTIONS
031-
032- "************ state machine: Sreg0 *************
033- "clock signals definitions
034- Sreg0.clk = CLK;
035-
036- state_diagram Sreg0
037- SYNC_RESET S0 : RESET;
038-
039-
040- State S0:
041-
```
