registers at the other end (with addresses in the range [32752..32767]). The remainder of the RAM cannot be accessed at all.

Once the address is sent to the RAM, GNOME must have a way to accept data from the RAM and send data to the RAM. The buses for this are shown in Figure 9.9. The accumulator is the only source for data written to the RAM, so we can build a 4-bit path from the ACC through the output drivers to the 8-bit RAM data bus. In the opposite direction, the only destination for data read from the RAM is the instruction register, so we place an 8-bit data bus from the input buffers to the IR. The read/write control logic in GNOME will control the output buffers of the RAM and the GNOME data bus so that they do not try to drive the data bus at the same time.

![](bbox=[0.28, 0.31, 0.85, 0.62])

# Figure 9.9 Input and output data buses for the external RAM.

At this point, the datapath is complete. The datapath contains the circuitry needed to read, manipulate, and store data. What is lacking is the controller that fetches instructions, interprets them, and then directs the operations of the datapath.

Fetching an instruction is handled by outputting the program counter through the memory address multiplexer and latching the output data from the RAM into the IR. After fetching an instruction, the simple incrementer in Figure 9.10 can advance the PC to the next instruction in memory. The incrementer can also be used when skipping an instruction.

But a program can also jump to a new address instead of proceeding sequentially through memory. Therefore, a multiplexer is added in Figure 9.11 to select whether the PC is loaded with (1) the address of the next instruction in memory, as calculated by the incrementer; or (2) with the address stored in the