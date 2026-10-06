Code and data are two very different kinds of critters, but they interact in ways that make the game interesting. The code includes steps that place data into storage (MOVE instructions) and steps that alter data that is already in storage (INCREMENT and DECREMENT instructions). Most of the time you'll think of code as being the master of data, in that the code writes data values into storage. Data influence code as well, however. Among the tests the code makes examine data in storage, if a given data value exists in storage, the code may do one thing; if that value does not exist in storage, the code will do something else, as as in the JUMP BACK and JUMP AHEAD instructions.

The short block of instructions marked PROCEDURE is a detour off the main stream of instructions. At any point in the program you can duck into the procedure, perform its steps and tests, and return to the very place from which you left. This allows a sequence of steps and tests that is generally useful and used frequently to exist in only place rather than exist as a separate copy everywhere it is needed.

# Addresses

Another critical concept lies in the funny numbers at the left side of the program step locations and data locations. Each number is unique, in that a location tagged with that number appears only once inside the computer. This location is called an address. Data is stored and retrieved by specifying the data's address in the machine. Procedures are called by specifying the address at which they begin.

The little box (which is also a storage location) marked PROGRAM COUNTER keeps the address of the next instruction to be performed. The number inside the program counter is increased by one (we say, "incremented") each time an instruction is performed unless the instruction tells the program counter to do something else. For example: Notice the JUMP BACK 7 instruction at address 0049. When this instruction is performed, the program counter will "back up" by seven counts. This is analogous to the "go back three spaces" concept in board games.

# Metaphor Check!

That's about as much explanation of the Game of Assembly Language as I'm going to offer for now. This is still Chapter 1, and we are still in