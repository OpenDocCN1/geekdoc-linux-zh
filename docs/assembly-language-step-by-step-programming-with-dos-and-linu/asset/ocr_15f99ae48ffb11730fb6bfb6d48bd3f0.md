How is this done? Recall that the CPU contains a register that always contains the address of the next instruction to be executed. This register, the instruction pointer, is not essentially different from any of the other registers in the CPU. Just as a machine instruction can add to register AX, another machine instruction can add—or subtract—some number to or from the address stored in the instruction pointer. And the CPU will instantly skip 100 bytes down the list of machine instructions before it continues. Subtract 100 from the address stored in the instruction pointer, and the CPU will instantly jump back 100 bytes up the machine instruction list.

And finally, the Third Whammy: The CPU can change its execution based on the work it has been doing. The CPU can decide whether to execute a given instruction or group of instructions, based on values stored in memory, or based on the state of special one-bit registers called flags. The CPU can count up how many times it needs to do something, and then do that something that number of times.

So, not only can you tell the CPU what to do, but you can tell it where to go. Better, you can sometimes let the CPU, like a faithful bloodhound, sniff out the best course forward in the interest of getting the work done the quickest possible way.

In Chapter 1, I spoke of a computer program being a sequence of steps and tests. Most of the machine instructions understood by the CPU are steps, but others are tests. The tests are always two-way tests, and in the choice of what to do is always the same: Jump or don't jump. That's all. You can test for any of numerous different conditions, but the choice is always one of jumping to another place in the program, or just keep truckin' along.

# The Plan

I sum it all up by borrowing one of the most potent metaphors for computing ever uttered: The computer is a box that follows a plan. These are the words of Ted Nelson, author of the uncanny book Lib/Dream Machines, and one of those very rare people who have the infuriating habit of being right most of the time.

You write the plan. The computer follows it by passing the instructions, byte by byte, to the CPU. At the bottom of it, the process is a hellishly