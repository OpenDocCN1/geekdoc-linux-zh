address in memory. This double word, consisting of four bytes row, is read from memory and loaded into the CPU. The CPU exam-ines the pattern of binary bits contained in the double word, and then begins performing the task that the fetched machine instruction directs it to do.

Ancient 8088-based machines such as the original IBM PC only fetched one byte at a time, rather than the four bytes that modern Pentium-class machines fetch. Because most machine instructions are more than a single byte in size, the 8088 CPU had to return to memory to fetch a second (a third or fourth) byte to complete the machine instruction before it could actually begin to obey the instruction and begin performing the task that the instruction specified.

As as it finishes executing an instruction, the CPU goes out to memory and fetches the next instruction pointer in sequence. Inside the CPU is a register called the instruction pointer that quite literally contains the address of the next instruction to be fetched and executed. Each time an instruction is completed, the instruction pointer is updated to point to next instruction in memory. (There is some silicon afoot inside modern CPUs that guesses what's to be fetched next and keeps it on a side shelf so it'll be there when fetched only much more quickly—but the process as I've described is true in terms of the outcome.)

So the process goes: Fetch and execute; fetch and execute. The CPU works its way through memory, with the instruction pointer register leading the way. As it goes, it works: Moving data around in memory, moving values around in registers, passing data to peripherals, crunching data in arithmetic or logical operations.

Computer programs are lists of binary machine instructions stored in memory. They are no different from any other list of data bytes stored in memory except in how they are treated when fetched by the CPU.

# The’s Innards

I made the point earlier that machine instructions are binary instructions. This is something we often gloss over, yet to understand the true nature of the CPU, we have to step away from the persistent image of machine instructions as numbers. They are not numbers. They are binary patterns designed to throw electrical switches.