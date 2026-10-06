8088, 8086, and 80286 are often called 16-bit CPUs because their registers are almost all 16 bits in size. The 80386 and its successors are called 32-bit CPUs because most of their internal registers are 32 bits in size. The x86 CPUs have a fair number of registers, and they are an interesting crew indeed.

Registers do many jobs, but one of their more important jobs is holding addresses of important locations in memory. If you'll recall, the 8086 and 8088 have 20 address pins, and their megabyte of memory (which is the real mode segmented memory we're talking about) requires addresses 20 bits in size.

How do you put a 20-bit memory address in a 16-bit register? Easy. You don't.

You put a 20-bit address in two 16-bit registers.

What happens is this: All memory locations in real mode's megabyte of memory have not one address but two. Every byte in memory is assumed to reside in a segment. A byte's complete address, then, consists of the address of its segment, along with the distance of the byte from the start of that segment. The address of the segment is (as we said before) the byte's segment address. The byte's distance from the start of the segment is the byte's offset address. Both addresses must be specified to completely describe any single byte's location within the full megabyte of real memory. When written out, the segment address comes first, followed by the offset address. The two are separated with a colon. Segment:offset addresses are always written in hexadecimal. Make sure that the colon is so that people know you're specifying an address and not just a couple of numbers!

I've drawn Figure 6.5 to help make this a little clearer. A byte of data we'll call MyByte exists in memory at the location marked. Its address is given as 0001:001D. This means MyByte falls within segment 0001H and located 001DH from the start of that segment. Note that when two numbers are used to specify an address with a colon between them, you do not end each of the two numbers with an H for hexadecimal.

You can omit zeros if you like; that, instead of saying 00B2:0004 you could write 0B2:4. The leading zero is retained in front of the B in keeping with assembly language policy of never allowing a hex number to begin with the hex digits A through F.) As a good rule of