
![](img/5124daf79d2807d81e49f49c22f1f8c1_285_0.png)

**Figure 8.14** FIFO interface signals.

![](img/5124daf79d2807d81e49f49c22f1f8c1_285_1.png)

**Figure 8.15** FIFO components.

**wrptr:** The write pointer also increments in the wrap-around sequence 0, 1, ..., N − 1, 0, 1. A write operation increments the pointer, but no write is performed if the FIFO is full. If that happened, then the read pointer would be one behind the write pointer and the FIFO would then contain twice as many data bytes. Thus, N − 1 bytes of data would be lost.

**Multiplexer:** This component directs either the read or write pointer to the address inputs of the RAM depending on the operation being performed.

**Comparator:** The read and write pointer values must be compared for equality to determine when the FIFO is full or empty.

## Control logic:

This is the block where you throw all the stuff you do not know how to do yet. It controls the write enable line of the RAM and the address multiplexer. It also controls the incrementing of both the read and write pointers depending upon whether the FIFO is empty or full.

The circuitry for a FIFO pointer is shown in Figure 8.16. The pointer has clk, clr, and stop inputs, which cause the pointer to increment, asynchronously clear to zero, or stop incrementing, respectively. The register is made of D flip-flops, which hold the current address in the pointer. The pointer changes its value on the rising edge of the clk signal. If stop = 0, then the multiplexer steers the incremented value of the register back into the register so that an increment occurs. If stop = 1, the register just reloads its current value.

![](img/5124daf79d2807d81e49f49c22f1f8c1_286_0.png)

**Figure 8.16** FIFO pointer module.

The FIFO pointer module is used twice to build the read and write pointers. The clocks for these pointers are the rd and wr inputs. Both rd and wr are normally high and are pulsed low to cause a read or write operation, respectively. The rising edge at the end of either a read or a write pulse causes the respective pointer to change state. The empty or full outputs are used to stop the increment of rdptr or wrptr, respectively. The global reset line is also hooked to the clr input of each pointer so that they can both be reset to zero upon startup.

The outputs of both pointers go to the equality comparator and the multiplexer. The multiplexer selects which pointer addresses the RAM using the rd input. If rd is low (i.e., a read operation), then the read pointer addresses the RAM. Otherwise, the write pointer addresses the RAM. It is important that the write pointer should address the RAM whenever there is not a read operation. If you built the opposite arrangement so that the read pointer normally addressed the RAM except when a write occurred, there is the possibility of corrupting data in the FIFO. This occurs because the write address does not have enough time to propagate through the multiplexer and enable the correct RAM location for writing before the write pulse gets to the RAM. Thus, the location addressed by the read pointer may get written into instead. You can avoid this

problem by always addressing the RAM with the write pointer except when a read operation occurs. (This does mean that you have to wait a bit longer to read the output of the FIFO so that the address has time to settle and the RAM has time to access the memory location. But no erroneous data can slip into the FIFO during a read operation.)

The control logic to determine whether the FIFO is empty or full is described next. The FIFO is definitely neither empty nor full if the read and write pointers store different addresses. But how do you determine whether the FIFO is actually empty or full when the read and write pointers have the same value? (Look at Figures 8.13a and 8.13g to see that pointer equality is not enough to distinguish empty from full.) The answer lies in recording the type of the previous operation on the FIFO. If the previous operation was a write, then the FIFO cannot be empty because something was just written into it. Conversely, if the previous operation was a read, then the FIFO cannot be full because something was just read from it. So we can state the logic as follows:

- If the read and write pointers are equal and the last operation was a write, then the FIFO is full.
- If the read and write pointers are equal and the last operation was a read, then the FIFO is empty.

The logic is simple so all that remains is finding a way to record the type of the previous operation. Obviously, you need a flip-flop, but where does its clock come from? Figure 8.17 shows the circuitry for this. The prevop0 flip-flop can

![](img/5124daf79d2807d81e49f49c22f1f8c1_287_0.png)

**Figure 8.17** FIFO control logic.

be immediately set to logic 1 to indicate a write operation if we tie the D input high and clock the flip-flop with the falling edge of the write line. Conversely, we can drive the asynchronous clear with the read line to reset the flip-flop when a read occurs. Otherwise, the flip-flop retains its value.
