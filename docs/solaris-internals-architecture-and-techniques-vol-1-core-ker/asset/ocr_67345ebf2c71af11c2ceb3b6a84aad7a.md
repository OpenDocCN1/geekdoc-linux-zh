# Hardware Address Translation Layer

# HAT Layer

![](bbox=[0.105, 0.125, 0.915, 0.497])

Process's Linear Address Space  Virtual Memory Segments  Page size Pieces of Virtual Memory  Virtual-to-Physical Translation Tables  Physical Memory Pages  Physical Memory

Figure 5.26 Role of the HAT Layer in Virtual-to-Physical Translation

The HAT implementation is different for each type of hardware MMU, and hence there are several different HAT implementations. The HAT layer hides the platform-specific implementation and is used by the segment drivers to implement the segment drivers' view of virtual-to-physical translation. The HAT uses the struct data structure to hold the top-level translation information for an address space. The HAT structure is platform specific and is referenced by the address space structure (see Figure 5.7 on page 137). HAT-specific data structures existing in every page represent the translation information at a page level.

The HAT layer is called when the segment drivers want to manipulate the hardware-MMU. For example, when a segment driver wants to create or destroy an address space, it calls the HAT functions specifying the address range and the action to be taken. We can call the HAT functions without knowing anything about the underlying MMU implementation; the arguments to the HAT functions are machine independent and usually consist of virtual addresses, lengths, page pointers, and protection modes.

Table 5-16 summarizes HAT functions.