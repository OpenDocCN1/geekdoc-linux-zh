command name. There is also a “.l” suffix to explicitly specify 32 bits. Example: `cmp w 1000 2000 20` compares 32 (20 hex) words at addresses 0x1000 and 0x2000.

`base [offset>] {ba}` — Get or set a base address to be used as an offset for all other memory commands. With no argument it displays the current base, default is 0. A numeric argument becomes the new base. This is useful for repeated accesses to a specific section of memory.

`crc32 <start addr> <length> [<store addr>] [crc]` — Computes and displays a 32-bit checksum over `<length>` bytes, starting at `<start addr>`. The optional third argument specifies a location to store the checksum.

`cmp <addr1> <addr2> <count>` — Compares two regions of memory. `<count>` is the number of *data items* independent of the specified size, byte, word, or long.

`cp <source> <dest> <count>` — Copies a range of memory to another location. `<count>` is the number of items copied.

`md <addr> [<count>]` — Memory display. Displays a range of memory in both hex and ASCII. The optional `<count>` argument defaults to 64 items. `md` remembers the most recent `<addr>` and `<count>`, so that if it is entered without an address argument, it continues from where it left off.

`mm <start addr>` — Modify memory with autoincrement. Displays the address and current contents of an item, and prompts for user input. A valid hexadecimal value replaces the current value and the command displays the next item. This continues as long as you enter valid hex values. To terminate the command, enter a non-hex value.

`mtest <start addr> <end addr> [<pattern>]` — Simple read/write RAM test. This test modifies RAM and may crash the system if it touches areas used by u-boot, such as the stack or heap.

`mw <addr> <value> [<count>]` — Writes `<value>` to a range of memory starting at `<addr>`. The optional `<count>` defaults to 1.

`nm <addr>` — Modify memory at a constant address (no autoincrement). Interactively writes valid hex data to the same address. This is useful for accessing I/O device registers. Terminate the command with a non-hex input.

`loop <addr> <count>` — Reads memory in a tight loop. This can be useful for scoping. This command **never terminates**! The only way out is to reset the board.

# NAND Flash Memory Commands

NAND flash is organized into arbitrary sized named *partitions*. All NAND commands are prefixed by the keyword `nand`. The BeagleBone Black u-boot implements the NAND commands, even though there is no NAND device installed.