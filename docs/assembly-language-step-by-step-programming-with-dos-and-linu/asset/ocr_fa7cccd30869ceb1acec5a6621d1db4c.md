# Lifting the Hood

some time in the next few months as I write, Intel will begin sampling samples of its first 64-bit CPU, code-named Merced. Merced fetches 8 bytes (a quad word) at a time and will run at speeds of 1 GHz (gigahertz: a billion clock cycles per second) or has plenty of internal machinery to make sure that expanding its silicon jaws to swallow 64 bits at a time will not slow anything down.

Is 64 bits an optimal size? No bets taken here. I've been in this business long enough to see the foolishness of making sweeping statements like that.

# Talking to Memory

The assorted Intel CPUs operate at varying speeds with various features, but at the bottom of things they are conceptually identical, and this discussion will apply to all of them.

The CPU chip's most important job is to communicate with the computer's memory system. Like a memory chip, a CPU chip is a small square of silicon onto which a great many transistors have been placed. The fragile silicon chip is encased in a plastic or ceramic housing with a large number of pins protruding from it. Like the pins of memory chips, the CPU's pins transfer information encoded as voltage levels, typically 3 to 5 volts. Five volts indicate a binary 1, and zero volts indicate a binary 0.

Like the memory chips, the CPU chip has a number of pins devoted to memory addresses, and these pins are connected directly to the computer's bands of memory chips. When the CPU desires to read a byte (or a word, or double word) from memory, it places the memory address of the byte to be read on its address pins, encoded as a binary number. Seventy nanoseconds or later, the byte appears (also as a binary number) on the data pins of the memory chips. The CPU chip also has data pins, and it slurps up the byte presented by the memory chips through its own data pins. See Figure 3.4.

The process, of course, also works in reverse: To write a byte into memory, the CPU first places the memory address where it wants to write onto its address pins. Some number of nanoseconds later (which varies from system to system how memory is arranged) the CPU places the byte it wishes to write into memory on its data pins. The memory chips obediently store the byte inside themselves at the requested address.