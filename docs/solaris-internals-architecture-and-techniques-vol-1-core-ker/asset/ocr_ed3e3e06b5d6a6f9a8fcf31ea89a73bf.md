The UltraSPARC I & II trap table is an in-memory table that contains the first eight instructions for each type of trap. The trap table is located in memory at the address stored in the trap table base address register (TBA), which is initialized during boot. Solaris places the trap table at the base of the kernel (known as kernelbase) in a locked-down (non-pageable) 4-Mbyte page so that memory-related traps (page faults or TLB misses) will occur during execution of instructions in the trap table. (For a detailed kernel memory map, see Appendix B, “Kernel Virtual Address Maps”).

#  2.2.3.1 UltraSPARC I & II Trap Types

The trap table contains one entry for each type of trap and provides a specific handler for each trap type. The UltraSPARC I & II traps can be categorized into the following types:

+   **Processor resets** — Power-on reset, machine resets, software-initiated resets
**Memory management exceptions** — MMU page faults, page protection violations, memory errors, misaligned accesses, etc.
**Instruction exceptions** — Attempts to execute privileged instructions from nonprivileged mode, illegal instructions, etc.\n**Floating-point exceptions** — Floating-point exceptions, floating-point mode instruction attempted when floating point unit disabled, etc.
**SPARC register management** — Traps for SPARC register window spilling, filling, or cleaning.
**Software-initiated traps** — Traps initiated by the SPARC trap instruction (Tec); primarily used for system call entry in Solaris.

Table 2-1 shows the UltraSPARC I & II trap types, as implemented in Solaris.

# Table 2-1 Solaris UltraSPARC I & II Traps

| Trap Definition | Trap Type | Priority |
| Power-on reset | 001 | 0 |
| Watchdog reset | 002 | 1 |
| Externally initiated reset | 003 | 1 |
| Software-initiated reset | 004 | 1 |
| RED state exception | 005 | 1 |
| Reserved | 006...007 | n/a |
| Instruction access exception | 008 | 5 |
| Instruction access MMU miss | 009 | 2 |
| Instruction access error | 00A | 3 |
| Reserved | 00B...00F | n/a |
| Illegal instruction | 010 | 7 |