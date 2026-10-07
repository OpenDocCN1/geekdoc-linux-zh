# The Hardware Address Translation Layer

# 197

![](bbox=[0.115, 0.083, 0.923, 0.439])

Figure 5.30 Relationship of TLBs, TSBs, and TTEs

The TLB on UltraSPARC-I and -II has 64 entries, and the TSB has between 2,048 and 262,144 entries, depending on the amount of memory in the system. Unlike the previous generation SPARC MMU, the UltraSPARC-I and -II MMU does not use a hardware page tablewalk to access the TSB entries, but it still provides a form of hardware assistance to speed up TSB access: Hardware precomputes TSB table offsets to help the software handler finds TTEs in the TSB. When the CPU needs to access a virtual address, the system takes the following steps:

+   1. The MMU first looks in the TLB for a valid TTE for the requested virtual address.
2. If a valid TTE is not found, then the MMU automatically generates a pointer for the location of the TSB TTE entry and generates a TLB miss trap.
3. The trap handler reads the hardware-constructed pointer, retrieves the entry from the TSB, and places it in the appropriate TLB slot with an atomic write into the TLB.
4. If the TTE is not found in the TSB, then the TLB miss handler jumps to a more complex, but slower, TSB miss handler, which retrieves the TTE from the page structure by using a software hashed index structure.

UltraSPARC-I and -II also provide a separate set of global registers to processU traps. This approach dramatically reduces the time taken for the TLB miss handler to locate TSB entries since the CPU does not need to save process state during the trap—it simply locates the entry, atomically stores the entry, and returns to execution of the running process.