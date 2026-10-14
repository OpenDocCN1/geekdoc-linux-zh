The output of prevop0 cannot be used directly because it changes value as soon as a read or write operation begins. The current operation must complete before the flip-flop is updated. Therefore a second flip-flop, prevop1, is used to delay the output from prevop0 until after the current operation is complete. The clock for the prevop1 flip-flop is formed from the logical AND of the read and write control lines so that a low pulse on either control line updates the prevop1 flip-flop with the value stored in prevop0.

A final piece of control logic is needed to prevent the RAM from being corrupted by a write to a full FIFO. The active-low write-enable signal to the RAM, gatewr, is driven by an OR gate that has the write control line of the FIFO and the full status signal as inputs. If the FIFO is full, then gatewr is held high so that no data can be written into the RAM. If the FIFO is not full, then the write pulse from the FIFO write control input passes through to the RAM write-enable unchanged.

# Experimental

# Building a Small Asynchronous Memory

The ABEL code for the 4-register memory with 4 bits per register (similar to the one in Figure 8.9 which we will call a 4x4 memory) is shown in Listing 8.1.

Lines 6–9 declare pins for the write and output-enable control inputs, the 2-bit address bus, and the 4-bit input data bus, respectively. Internal signals are declared on lines 10–14. Line 10 defines a 4-bit register composed of 4 D flip-flops. The other three registers are defined on lines 11–13. The signals that control writing into these registers are declared on line 14.

The 4-bit memory output bus is declared on line 15. In keeping with Figure 8.9, we are using separate input and output buses. A combined I/O bus (as in Figure 8.10) can be used if the design is targeted only toward the XC4000 FPGAs. An I/O bus requires internal tristate buses, which are not available in the XC9500 CPLD.

We also add another set of 7 outputs on line 16 to display the output from the RAM on the LED digit.

Lines 18–25 just define some shorter names for some of the signals that we declared earlier. The construction of the memory begins by connecting the input data bus to the 4 registers on lines 30–33. Note the use of the := operator to signify that the value on the input data bus is being clocked into the registers.

Lines 35–48 describe the actual signals that clock the registers. The operation of the write line for each register is described on lines 38–41 using the ABEL WHEN...THEN...ELSE construct. If the Boolean expression following the