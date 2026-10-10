
used by the kernel when transitioning from user mode to kernel mode. This process is discussed in detail in Chapter 3.

## Translation Lookaside Buffer

The TLB is used in translating virtual addresses to physical addresses. Each entry in the TLB holds a virtual page number, the corresponding physical page number, and the access rights for that particular page. The system may use separate TLBs for instructions (ITLB) and data (DTLB), or it may use a combined TLB.

PA-RISC version 2.0 includes provisions for variable-sized pages. Prior to PA-RISC 2.0 all pages were a fixed 4 KB. PA-RISC 2.0 can use pages ranging from 4 KB to 64 MB. This allows for more efficient use of the TLB when very large data structures are used. A large data structure can be placed in a single large page and will use only one TLB entry rather than requiring several.

When an instruction accesses a particular virtual page, that page is looked up in the TLB to find the corresponding physical address and the access rights. If a matching entry is not present, a *TLB miss* interruption is generated. The system must then look up the correct entry in the Page Directory (PDR), insert the entry into the TLB, then restart the instruction. The details of how this happens are covered in Chapter 6, “Managing Memory.”

## Cache

PA-RISC uses a visible cache architecture. The processor has instructions to explicitly manipulate the cache, flushing or invalidating cache entries where required. Systems can have separate instruction and data caches, or they may have a single combined cache.

In order to have the required data in the cache whenever possible, the cache is capable of prefetching data and instructions. To determine which data should be fetched, the PA-RISC processor uses *branch prediction* to guess which way conditional branches will go. Compilers can code a prediction into branch instructions. For example, if a branch is used in a loop, and the loop will run for 100 iterations, then the end-of-loop branch will be taken 100 times, not taken just one time. The compiler can indicate to the processor that it is more likely that the branch is taken, and the cache prefetch circuitry can then prefetch the correct instructions. PA-RISC 2.0 also adds a *dynamic branch prediction* functionality. The processor keeps track of how many times a branch actually went the way that the compiler predicted. If the branch prediction indicator is wrong more than right, then the system starts prefetching the opposite of the way the branch prediction indicates.

In a multiprocessor system, the cache must also be aware of the memory activity of other processors. This is called *cache coherence*. The cache circuitry continually monitors the system bus for load and store instructions from other processors. In this way, it will know if the data in the cache is no longer valid due to access from a different processor.

## Assist Processors

The PA-RISC architecture provides for extensibility in the form of assist processors. Two kinds of assist processors are defined: special function units (SFUs) and coprocessors. An SFU is a hardware module that has direct access to the CPU's general registers but operates outside of the CPU's execution unit. Although the architecture defines how SFUs are to be implemented, none are currently used. A coprocessor is also an assist processor, but it is less closely coupled to the CPU. It has its own set of registers, and data must be explicitly passed to and from the coprocessor for processing.

An understanding of the assist processors is not required for an understanding of the kernel, so we do not go into detail beyond this brief mention. Suffice it to say that PA-RISC processors do have a floating-point coprocessor, and if you find yourself looking at assembly code, you may occasionally see references to it.

## Registers

The PA-RISC architecture provides for several sets of registers. Of particular interest to us are the general registers, space registers, and some of the control registers.

### General Registers

PA-RISC has 32 general purpose registers. In PA-RISC 2.0, these are 64-bit registers; prior to PA-RISC 2.0, these registers are 32 bits wide. The architecture itself defines specific uses for only a few of these registers:

- GR0—Permanent zero. Reads from this register always return a zero. Writes to this register are discarded.
- GR1—Target of ADDIL. When the ADD IMMEDIATE LONG (ADDIL) instruction is executed, the result is always placed in GR1. This register can also be used for other purposes.
- GR2—Target of B,L. This register is used as the target of the BRANCH AND LINK instruction, which is used for procedure calls. The link, or return, address is placed in GR2. This register can also be used for other purposes.
- GR31—Target of BLE. This register is similar to GR2 but is used for the return address from a BRANCH AND LINK EXTERNAL instruction.

Beyond these requirements there is also a software convention that specifies how registers will be used by HP-UX. These conventions are slightly different for the 64-bit version of HP-UX. Figure 1-2 shows the usage of general registers for the 32-bit kernel, and Figure 1-3 shows the usage for the 64-bit kernel. Most of these requirements for register usage come into play when performing procedure calls and are covered in detail in Chapter 2, "Procedure Calling Conventions." GR27, the data pointer, points to the base of the data segment. Memory references to the data segment are made relative to GR27. These are primarily global values in the kernel. GR30 is the stack pointer.

| Register | Description |
| :--- | :--- |
| GR-0 | Parametric Zero |
| GR-1 | ADDIL Target |
| GR-2 | Return Pointer |
| GR-4 | General Usage |
| GR-5 | ... |
| GR-6 | ... |
| GR-7 | ... |
| GR-8 | ... |
| GR-9 | ... |
| GR-10 | ... |
| GR-11 | ... |
| GR-12 | ... |
| GR-13 | ... |
| GR-14 | ... |
| GR-15 | ... |
| GR-16 | ... |
| GR-17 | ... |
| GR-18 | General Usage |
| GR-19 | General Usage |
| GR-20 | ... |
| GR-21 | ... |
| GR-22 | General Usage |
| GR-23 | Argument 3 (arg3) |
| GR-24 | Argument 2 (arg2) |
| GR-25 | Argument 1 (arg1) |
| GR-26 | Argument 0 (arg0) |
| GR-27 | Data Pointer (dp/qp) |
| GR-28 | Return Value/Frame Ptr |
| GR-29 | Return Value (double) |
| GR-30 | Stack Pointer |
| GR-31 | Link for BLE |

**Figure 1-2 32-Bit General Registers**

### Space Registers

PA-RISC provides eight space registers. As with the general registers, the architecture provides for 64-bit wide registers on PA-RISC 2.0 and 32-bit wide registers on PA-RISC 1.1. However, on all current implementations of PA-RISC 2.0, the space registers are actually only 32 bits wide. The space registers are used in combination with the general registers to construct a virtual address. The space register can be either explicitly supplied in the instruction or implied by the value in the general register. The use of the space registers is covered in detail in the section "Virtual Memory Support."

### Control Registers

PA-RISC provides 32 control registers (see Figure 1-4). Again, in PA-RISC 1.1 these are 32-bit registers, but in PA-RISC 2.0 they are 64-bit registers. Most of these are used when handling interruptions and are discussed in detail in the section "Interruption Handling."

**Callee Saves**

| Register | Description |
| :--- | :--- |
| CR-0 | Recovery Counter |
| CR-1 | ADDIL Target |
| CR-2 | Return Pointer |
| CR-3 | General Usage |
| CR-4 | --- |
| CR-5 | ... |
| CR-6 | --- |
| CR-7 | ... |
| CR-8 | --- |
| CR-9 | --- |
| CR-10 | ... |
| CR-11 | --- |
| CR-12 | ... |
| CR-13 | --- |
| CR-14 | ... |
| CR-15 | --- |
| CR-16 | ... |
| CR-17 | --- |
| CR-18 | General Usage |
| CR-19 | Argument 7 (arg7) |

**Caller Saves**

| Register | Description |
| :--- | :--- |
| CR-20 | Argument 6 (arg6) |
| CR-21 | Argument 5 (arg5) |
| CR-22 | Argument 4 (arg4) |
| CR-23 | Argument 3 (arg3) |
| CR-24 | Argument 2 (arg2) |
| CR-25 | Argument 1 (arg1) |
| CR-26 | Argument 0 (arg0) |
| CR-27 | Data Pointer (dp/dp) |
| CR-28 | Return Value/Frame Ptr |
| CR-29 | Argument Pointer (ap) |
| CR-30 | Stack Pointer |
| CR-31 | Link for BLE |

**Figure 1-3 64-Bit General Registers**

| Register | Description |
| :--- | :--- |
| CR-0 | Recovery Counter |
| CR-1-CR-7 | Reserved |
| CR-8-CR-9 | Protection IDs |
| CR-10 | Coprocessor Configuration Record (CCR) |
| CR-11 | Shift Amount Register (SAR) |
| CR-12-CR-13 | Protection IDs |
| CR-14 | Interrupt Vector Address |
| CR-15 | External Interrupt Enable Mask (EIEM) |
| CR-16 | Interrupt Timer |
| CR-17 | Interrupt Instruction Address Space Queue (IIASQ) |
| CR-18 | Interrupt Instruction Address Offset Queue (ILAOQ) |
| CR-19 | Interrupt Instruction Register |
| CR-20 | Interrupt Space Register |
| CR-21 | Interrupt Offset Register |
| CR-22 | Interrupt Processor Status Word |
| CR-23 | External Interrupt Request Register |
| CR-24-CR-31 | Temporary Registers |

**Figure 1-4 Control Registers**

## Processor Status Word

One more register of interest is the Processor Status Word (PSW). This is a 64-bit register (32-bits on PA-RISC 1.1) whose bits indicate the state of the system. Some of these bits are con-
