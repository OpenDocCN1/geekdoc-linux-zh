problem by always addressing the RAM with the write pointer except when a read operation occurs. (This does mean that you have to wait a bit longer to read the output of the FIFO so that the address has time to settle and the RAM has time to access the memory location. But no erroneous data can slip into the FIFO during a read operation.)

The control logic to determine whether the FIFO is empty or full is described next. The FIFO is definitely neither empty nor full if the read and write pointers store different addresses. But how do you determine whether the FIFO is actually empty or full when the read and write pointers have the same value? (Look at Figures 8.13a and 8.13g to see that pointer equality is not enough to distinguish empty from full.) The answer lies in recording the type of the previous operation on the FIFO. If the previous operation was a write, then the FIFO cannot be empty because something was just written into it. Conversely, if the previous operation was a read, then the FIFO cannot be full because something was just read from it. So we can state the logic as follows:

+   If the read and write pointers are equal and the last operation was a write, then the FIFO is full.
+   If the read and write pointers are equal and the last operation was a read, then the FIFO is empty.

The logic is simple so all that remains is finding a way to record the type of the previous operation. Obviously, you need a flip-flop, but where does its clock come from? Figure 8.17 shows the circuitry for this. The prevop0 flip-flop can

![](bbox=[0.35, 0.73, 0.88, 0.88])

# Figure 8.17 FIFO control logic.

be immediately set to logic 1 to indicate a write operation if we tie the D input high and clock the flip-flop with the falling edge of the write line. Conversely, we can drive the asynchronous clear with the read line to reset the flip-flop when a read occurs. Otherwise, the flip-flop retains its value.