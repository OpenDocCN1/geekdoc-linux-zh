useful to forget about the transistors and even rows of chips to avoid confusion. (My high school computer science teacher was not entirely wrong ... but he was right for the wrong reasons.)

Over the years, memory systems have been accessed in different ways. Eight-bit computers (now ancient and most extinct) accessed memory eight bits (one byte) at a time. Sixteen-bit computers access memory 16 bits (one word) at a time. And today's 32-bit computers (everything in the PC realm since the 386) access memory 32 bits (one double word) at a time. It can be confusing, so it's better in most cases to envision a very long row of byte-sized containers, each with its own address. Don't assume that in computers which process information a word at a time that only words have addresses; it is a convention with the PC architecture that every byte has its own address regardless of how many bytes are pulled from memory at one time.

Every byte of memory in the computer has its unique address, even in computers that process two bytes or four bytes of information at a time.

If this seems counterintuitive yet another metaphor will help: When you go to the library to take out the three volumes of Tolkien's massive fantasy The Lord of the Rings, you will find that each of the three volumes has its own card catalog number (essentially volume's address in the library) but you take all three at once and process them as a single entity. If you really want to, you can take only one of the books out at a time, but to do so will require another trip to the library to get the next volume, which is wasteful of your time and effort.

So is with 16-bit or 32-bit computers. Every byte has its own address, but when a 16-bit computer accesses a byte, it actually reads two bytes starting at the address of the requested byte. You can use the second byte or ignore it if you don't need it—but if you later decide you need the second byte, you'll have to access memory again to get it. To save time and get it all at one swoop.

# The Honcho Chip

All of this talk about reading things from memory and writing things to memory has thus carefully skirted the question of who is doing the read and writing. The who is almost always a single chip, and a remarkable chip it is, too: the central processing unit, or CPU. If you are the president and CEO of your personal computer, the CPU is your shop