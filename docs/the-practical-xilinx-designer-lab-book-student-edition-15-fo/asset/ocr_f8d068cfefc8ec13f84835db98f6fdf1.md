# Figure 4.16 Adding buses of the 8-bit adder to the Waveform Viewer window.

with successive bits of the binary counter. We have now attached varying signals from the binary counter to both the A and B buses.

We now have varying signals from the binary counter driving the lower 3 bits of the A and B buses. But we also need to attach valid logic levels to the upper bits of these buses and to the CIN input. To do this, highlight an unattached input in the Waveform Viewer window and then click on the 0 button in the Keyboard area of the Stimulator Selection window. This will tie the input to a logic 0. After connecting the rest of the inputs to 0, close the Stimulator Selection window. Your Waveform Viewer should look like the one shown in Figure 4.17.

Now that the inputs have the appropriate stimulation, we can re-assemble the buses. Click on A7 in the Waveform Viewer window, and then hold the Shift key down while clicking on A0. All the A bus inputs will be highlighted. Then select Signal → Bus → Combine. This will assemble the A7–A0 signals back into an 8-bit bus. Repeat these steps to rebuild the B bus.

Now we can run a simulation of the 8-bit adder: Click the Long button in the floating Simulator window. A portion of the resulting waveforms are shown in figure 4.18. Note that at all times the value displayed on the SUM bus equals