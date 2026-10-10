# ## Assist Processors

The PA-RISC architecture provides for extensibility in the form of assist processors. Two kinds of assist processors are defined: special function units (SFUs) and coprocessors. An SFU is a hardware module that has direct access to the CPU's general registers but operates outside of the CPU's execution unit. Although the architecture defines how SFUs are to be implemented, none are currently used. A coprocessor is also an assist processor, but it is less closely coupled to the CPU. It has its own set of registers, and data must be explicitly passed to and from the coprocessor for processing.

An understanding of the assist processors is not required for an understanding of the kernel, so we do not go into detail beyond this brief mention. Suffice it to say that PA-RISC processors do have a floating-point coprocessor, and if you find yourself looking at assembly code, you may occasionally see references to it.

# # Registers

The PA-RISC architecture provides for several sets of registers. Of particular interest to us are the general registers, space registers, and some of the control registers.

# ## General Registers

PA-RISC has 32 general purpose registers. In PA-RISC 2.0, these are 64-bit registers; prior to PA-RISC 2.0, these registers are 32 bits wide. The architecture itself defines specific uses for only a few of these registers:

+   - GR0—Permanent zero. Reads from this register always return a zero. Writes to this register are discarded.

+   - GR1—Target of ADDIL. When the ADD IMMEDIATE LONG (ADDIL) instruction is executed, the result is always placed in GR1. This register can also be used for other purposes.

+   - GR2—Target of B , L. This register is used as the target of the BRANCH AND LINK instruction, which is used for procedure calls. The link, or return, address is placed in GR2. This register can also be used for other purposes.

+   - GR31—Target of BLE. This register is similar to GR2 but is used for the return address from a BRANCH AND LINK EXTERNAL instruction.

Beyond these requirements there is also a software convention that specifies how registers will be used by HP-UX. These conventions are slightly different for the 64-bit version of HP-UX. Figure 1-2 shows the usage of general registers for the 32-bit kernel, and Figure 1-3 shows the usage for the 64-bit kernel. Most of these requirements for register usage come into play when performing procedure calls and are covered in detail in Chapter 2, "Procedure Calling Conventions." GR27, the data pointer, points to the base of the data segment. Memory references