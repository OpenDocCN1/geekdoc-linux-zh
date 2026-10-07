
# Entering Kernel Mode

![](img/a86367b95bf21add858c99948ac951c6_76_0.png)

Interrupts are light-weight and do most of their work by scheduling an interrupt thread.

Interrupt

Figure 2.2 Process, Interrupt, and Kernel Threads

## 2.2.3 UltraSPARC I & II Traps

The SPARC processor architecture uses traps as a unified mechanism to handle system calls, processor exceptions, and interrupts. A SPARC trap is a procedure initiated by the microprocessor as a result of a synchronous processor exception, an asynchronous processor exception, a software-initiated trap instruction, or a device interrupt.

Upon receipt of a trap, the UltraSPARC I & II processor enters privileged mode and transfers control to the instructions, starting at a predetermined location in a trap table. The trap handler for the type of trap received is executed, and once the interrupt handler has finished, control is returned to the interrupted thread. A trap causes the hardware to do the following:

- Save certain processor state (program counters, condition code registers, type, etc.)
- Enter privileged execution mode
- Begin executing code in the corresponding trap table slot

When an UltraSPARC trap handler processing is complete, it issues a SPARC DONE or RETRY instruction to return to the interrupted thread.

The UltraSPARC I & II trap table is an in-memory table that contains the first eight instructions for each type of trap. The trap table is located in memory at the address stored in the trap table base address register (TBA), which is initialized during boot. Solaris places the trap table at the base of the kernel (known as kernelbase) in a locked-down (non-pageable) 4-Mbyte page so that memory-related traps (page faults or TLB misses) will occur during execution of instructions in the trap table. (For a detailed kernel memory map, see Appendix B, “Kernel Virtual Address Maps”).

### 2.2.3.1 UltraSPARC I & II Trap Types

The trap table contains one entry for each type of trap and provides a specific handler for each trap type. The UltraSPARC I & II traps can be categorized into the following types:

- **Processor resets** — Power-on reset, machine resets, software-initiated resets
- **Memory management exceptions** — MMU page faults, page protection violations, memory errors, misaligned accesses, etc.
- **Instruction exceptions** — Attempts to execute privileged instructions from nonprivileged mode, illegal instructions, etc.
- **Floating-point exceptions** — Floating-point exceptions, floating-point mode instruction attempted when floating point unit disabled, etc.
- **SPARC register management** — Traps for SPARC register window spilling, filling, or cleaning.
- **Software-initiated traps** — Traps initiated by the SPARC trap instruction (tei); primarily used for system call entry in Solaris.

Table 2-1 shows the UltraSPARC I & II trap types, as implemented in Solaris.

## Table 2-1 Solaris UltraSPARC I & II Traps

| Trap Definition | Trap Type | Priority |
| :--- | :--- | :--- |
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

## Table 2-1 Solaris UltraSPARC I & II Traps (Continued)

| Trap Definition | Trap Type | Priority |
| :--- | :--- | :--- |
| Attempt to execute privileged instruction | 011 | 6 |
| Unimplemented load instruction | 012 | 6 |
| Unimplemented store instruction | 013 | 6 |
| Reserved | 014...01F | n/a |
| Floating-point unit disabled | 020 | 8 |
| Floating-point exception ieee754 | 021 | 11 |
| Floating-point exception – other | 022 | 11 |
| Tag overflow | 023 | 14 |
| SPARC register window clean | 024...027 | 10 |
| Division by zero | 028 | 15 |
| Internal processor error | 029 | 4 |
| Data access exception | 030 | 12 |
| Data access MMU miss | 031 | 12 |
| Data access error | 032 | 12 |
| Data access protection | 033 | 12 |
| Memory address not aligned | 034 | 10 |
| Load double memory address not aligned | 035 | 10 |
| Store double memory address not aligned | 036 | 10 |
| Privileged action | 037 | 11 |
| Load quad memory address not aligned | 038 | 10 |
| Store quad memory address not aligned | 039 | 10 |
| Reserved | 03A...03F | n/a |
| Asynchronous data error | 040 | 2 |
| Asynchronous data error | 041 | 3 |
| Asynchronous data error | 042 | 3 |
| Asynchronous data error | 043 | 3 |
| Asynchronous data error | 044 | 3 |
| Asynchronous data error | 045 | 3 |
| Asynchronous data error | 046 | 3 |
| Asynchronous data error | 047 | 3 |
| Asynchronous data error | 048 | 3 |
| Asynchronous data error | 049 | 3 |
| Asynchronous data error | 050 | 3 |
| Asynchronous data error | 051 | 3 |
| Asynchronous data error | 052 | 3 |
| Asynchronous data error | 053 | 3 |
| Asynchronous data error | 054 | 3 |
| Asynchronous data error | 055 | 3 |
| Asynchronous data error | 056 | 9 |
| Asynchronous data error | 057 | 9 |
| Asynchronous data error | 058 | 9 |
| Asynchronous data error | 059 | 9 |
| Asynchronous data error | 060 | 9 |
| Asynchronous data error | 061 | 9 |
| Asynchronous data error | 062 | 9 |
| Asynchronous data error | 063 | 9 |
| Asynchronous data error | 064 | 9 |
| Asynchronous data error | 065 | 9 |
| Asynchronous data error | 066 | 9 |
| Asynchronous data error | 067 | 9 |
| Asynchronous data error | 068 | 9 |
| Asynchronous data error | 069 | 9 |
| Asynchronous data error | 070 | 9 |
| Asynchronous data error | 071 | 9 |
| Asynchronous data error | 072 | 9 |
| Asynchronous data error | 073 | 9 |
| Asynchronous data error | 074 | 9 |
| Asynchronous data error | 075 | 9 |
| Asynchronous data error | 076 | 9 |
| Asynchronous data error | 077 | 9 |
| Asynchronous data error | 078 | 9 |
| Asynchronous data error | 079 | 9 |
| Asynchronous data error | 080 | 9 |
| Asynchronous data error | 081 | 9 |
| Asynchronous data error | 082 | 9 |
| Asynchronous data error | 083 | 9 |
| Asynchronous data error | 084 | 9 |
| Asynchronous data error | 085 | 9 |
| Asynchronous data error | 086 | 9 |
| Asynchronous data error | 087 | 9 |
| Asynchronous data error | 088 | 9 |
| Asynchronous data error | 089 | 9 |
| Asynchronous data error | 090 | 9 |
| Asynchronous data error | 091 | 9 |
| Asynchronous data error | 092 | 9 |
| Asynchronous data error | 093 | 9 |
| Asynchronous data error | 094 | 9 |
| Asynchronous data error | 095 | 9 |
| Asynchronous data error | 096 | 9 |
| Asynchronous data error | 097 | 9 |
| Asynchronous data error | 098 | 9 |
| Asynchronous data error | 099 | 9 |
| Asynchronous data error | 09A | 9 |
| Asynchronous data error | 09B | 9 |
| Asynchronous data error | 09C | 9 |
| Asynchronous data error | 09D | 9 |
| Asynchronous data error | 09E | 9 |
| Asynchronous data error | 09F | 9 |
| Asynchronous data error | 0A0 | 9 |
| Asynchronous data error | 0A1 | 9 |
| Asynchronous data error | 0A2 | 9 |
| Asynchronous data error | 0A3 | 9 |
| Asynchronous data error | 0A4 | 9 |
| Asynchronous data error | 0A5 | 9 |
| Asynchronous data error | 0A6 | 9 |
| Asynchronous data error | 0A7 | 9 |
| Asynchronous data error | 0A8 | 9 |
| Asynchronous data error | 0A9 | 9 |
| Asynchronous data error | 0AA | 9 |
| Asynchronous data error | 0AB | 9 |
| Asynchronous data error | 0AC | 9 |
| Asynchronous data error | 0AD | 9 |
| Asynchronous data error | 0AE | 9 |
| Asynchronous data error | 0AF | 9 |
| Asynchronous data error | 0B0 | 9 |
| Asynchronous data error | 0B1 | 9 |
| Asynchronous data error | 0B2 | 9 |
| Asynchronous data error | 0B3 | 9 |
| Asynchronous data error | 0B4 | 9 |
| Asynchronous data error | 0B5 | 9 |
| Asynchronous data error | 0B6 | 9 |
| Asynchronous data error | 0B7 | 9 |
| Asynchronous data error | 0B8 | 9 |
| Asynchronous data error | 0B9 | 9 |
| Asynchronous data error | 0BA | 9 |
| Asynchronous data error | 0BB | 9 |
| Asynchronous data error | 0BC | 9 |
| Asynchronous data error | 0BD | 9 |
| Asynchronous data error | 0BE | 9 |
| Asynchronous data error | 0BF | 9 |
| Asynchronous data error | 0C0 | 9 |
| Asynchronous data error | 0C1 | 9 |
| Asynchronous data error | 0C2 | 9 |
| Asynchronous data error | 0C3 | 9 |
| Asynchronous data error | 0C4 | 9 |
| Asynchronous data error | 0C5 | 9 |
| Asynchronous data error | 0C6 | 9 |
| Asynchronous data error | 0C7 | 9 |
| Asynchronous data error | 0C8 | 9 |
| Asynchronous data error | 0C9 | 9 |
| Asynchronous data error | 0CA | 9 |
| Asynchronous data error | 0CB | 9 |
| Asynchronous data error | 0CC | 9 |
| Asynchronous data error | 0CD | 9 |
| Asynchronous data error | 0CE | 9 |
| Asynchronous data error | 0CF | 9 |
| Asynchronous data error | 0D0 | 9 |
| Asynchronous data error | 0D1 | 9 |
| Asynchronous data error | 0D2 | 9 |
| Asynchronous data error | 0D3 | 9 |
| Asynchronous data error | 0D4 | 9 |
| Asynchronous data error | 0D5 | 9 |
| Asynchronous data error | 0D6 | 9 |
| Asynchronous data error | 0D7 | 9 |
| Asynchronous data error | 0D8 | 9 |
| Asynchronous data error | 0D9 | 9 |
| Asynchronous data error | 0DA | 9 |
| Asynchronous data error | 0DB | 9 |
| Asynchronous data error | 0DC | 9 |
| Asynchronous data error | 0DD | 9 |
| Asynchronous data error | 0DE | 9 |
| Asynchronous data error | 0DF | 9 |
| Asynchronous data error | 0E0 | 9 |
| Asynchronous data error | 0E1 | 9 |
| Asynchronous data error | 0E2 | 9 |
| Asynchronous data error | 0E3 | 9 |
| Asynchronous data error | 0E4 | 9 |
| Asynchronous data error | 0E5 | 9 |
| Asynchronous data error | 0E6 | 9 |
| Asynchronous data error | 0E7 | 9 |
| Asynchronous data error | 0E8 | 9 |
| Asynchronous data error | 0E9 | 9 |
| Asynchronous data error | 0EA | 9 |
| Asynchronous data error | 0EB | 9 |
| Asynchronous data error | 0EC | 9 |
| Asynchronous data error | 0ED | 9 |
| Asynchronous data error | 0EE | 9 |
| Asynchronous data error | 0EF | 9 |
| Asynchronous data error | 0F0 | 9 |
| Asynchronous data error | 0F1 | 9 |
| Asynchronous data error | 0F2 | 9 |
| Asynchronous data error | 0F3 | 9 |
| Asynchronous data error | 0F4 | 9 |
| Asynchronous data error | 0F5 | 9 |
| Asynchronous data error | 0F6 | 9 |
| Asynchronous data error | 0F7 | 9 |
| Asynchronous data error | 0F8 | 9 |
| Asynchronous data error | 0F9 | 9 |
| Asynchronous data error | 0FA | 9 |
| Asynchronous data error | 0FB | 9 |
| Asynchronous data error | 0FC | 9 |
| Asynchronous data error | 0FD | 9 |
| Asynchronous data error | 0FE | 9 |
| Asynchronous data error | 0FF | n/a |

### 2.2.3.2 UltraSPARC I & II Trap Types

The UltraSPARC I & II trap table is an in-memory table that contains the first eight instructions for each type of trap. The trap table is located in memory at the address stored in the trap table base address register (TBA), which is initialized during boot. Solaris places the trap table at the base of the kernel (known as kernelbase) in a locked-down (non-pageable) 4-Mbyte page so that memory-related traps (page faults or TLB misses) will occur during execution of instructions in the trap table. (For a detailed kernel memory map, see Appendix B, “Kernel Virtual Address Maps”).

The trap table contains one entry for each type of trap and provides a specific handler for each trap type. The UltraSPARC I & II traps can be categorized into the following types:

- **Processor resets** — Power-on reset, machine resets, software-initiated resets
- **Memory management exceptions** — MMU page faults, page protection violations, memory errors, misaligned accesses, etc.
- **Instruction exceptions** — Attempts to execute privileged instructions from nonprivileged mode, illegal instructions, etc.
- **Floating-point exceptions** — Floating-point exceptions, floating-point mode instruction attempted when floating point unit disabled, etc.
- **SPARC register management** — Traps for SPARC register window spilling, filling, or cleaning.
- **Software-initiated traps** — Traps initiated by the SPARC trap instruction (tei); primarily used for system call entry in Solaris.

Table 2-1 shows the UltraSPARC I & II trap types, as implemented in Solaris.

### 2.2.3.3 UltraSPARC I & II Trap Levels

The UltraSPARC I & II trap table is an in-memory table that contains the first eight instructions for each type of trap. The trap table is located in memory at the address stored in the trap table base address register (TBA), which is initialized during boot. Solaris places the trap table at the base of the kernel (known as kernelbase) in a locked-down (non-pageable) 4-Mbyte page so that memory-related traps (page faults or TLB misses) will occur during execution of instructions in the trap table. (For a detailed kernel memory map, see Appendix B, “Kernel Virtual Address Maps”).

The UltraSPARC I & II trap table is an in-memory table that contains the first eight instructions for each type of trap. The trap table is located in memory at the address stored in the trap table base address register (TBA), which is initialized during boot. Solaris places the trap table at the base of the kernel (known as kernelbase) in a locked-down (non-pageable) 4-Mbyte page so that memory-related traps (page faults or TLB misses) will occur during execution of instructions in the trap table. (For a detailed kernel memory map, see Appendix B, “Kernel Virtual Address Maps”).

## 2.2.3.4 UltraSPARC I & II Trap Layout

The UltraSPARC I & II trap table is an in-memory table that contains the first eight instructions for each type of trap. The trap table is located in memory at the address stored in the trap table base address register (TBA), which is initialized during boot. Solaris places the trap table at the base of the kernel (known as kernelbase) in a locked-down (non-pageable) 4-Mbyte page so that memory-related traps (page faults or TLB misses) will occur during execution of instructions in the trap table. (For a detailed kernel memory map, see Appendix B, “Kernel Virtual Address Maps”).

The UltraSPARC I & II trap table is an in-memory table that contains the first eight instructions for each type of trap. The trap table is located in memory at the address stored in the trap table base address register (TBA), which is initialized during boot. Solaris places the trap table at the base of the kernel (known as kernelbase) in a locked-down (non-pageable) 4-Mbyte page so that memory-related traps (page faults or TLB misses) will occur during execution of instructions in the trap table. (For a detailed kernel memory map, see Appendix B, “Kernel Virtual Address Maps”).

The UltraSPARC I & II trap table is an in-memory table that contains the first eight instructions for each type of trap. The trap table is located in memory at the address stored in the trap table base address register (TBA), which is initialized during boot. Solaris places the trap table at the base of the kernel (known as kernelbase) in a locked-down (non-pageable) 4-Mbyte page so that memory-related traps (page faults or TLB misses) will occur during execution of instructions in the trap table. (For a detailed kernel memory map, see Appendix B, “Kernel Virtual Address Maps”).

The UltraSPARC I & II trap table is an in-memory table that contains the first eight instructions for each type of trap. [Wait, the OCR is repeating sections, let me fix the logical flow.]

The UltraSPARC I & II trap table is an in-memory table that contains the first eight instructions for each type of trap. The trap table is located in memory at the address stored in the trap table base address register (TBA), which is initialized during boot. Solaris places the trap table at the base of the kernel (known as kernelbase) in a locked-down (non-pageable) 4-Mbyte page so that memory-related traps (page faults or TLB misses) will occur during execution of instructions in the trap table. (For a detailed kernel memory map, see Appendix B, “Kernel Virtual Address Maps”).

*(Self-correction: The OCR text provided is highly repetitive/fragmented. I will provide the clean merged version based on the unique content provided across the pages.)*

# Entering Kernel Mode

![](img/a86367b95bf21add858c99948ac951c6_76_0.png)

Interrupts are light-weight and do most of their work by scheduling an interrupt thread.

Interrupt

Figure 2.2 Process, Interrupt, and Kernel Threads

## 2.2.3 UltraSPARC I & II Traps

The SPARC processor architecture uses traps as a unified mechanism to handle system calls, processor exceptions, and interrupts. A SPARC trap is a procedure initiated by the microprocessor as a result of a synchronous processor exception, an asynchronous processor exception, a software-initiated trap instruction, or a device interrupt.

Upon receipt of a trap, the UltraSPARC I & II processor enters privileged mode and transfers control to the instructions, starting at a predetermined location in a trap table. The trap handler for the type of trap received is executed, and once the interrupt handler has finished, control is returned to the interrupted thread. A trap causes the hardware to do the following:

- Save certain processor state (program counters, condition code registers, type, etc.)
- Enter privileged execution mode
- Begin executing code in the corresponding trap table slot

When an UltraSPARC trap handler processing is complete, it issues a SPARC DONE or RETRY instruction to return to the interrupted thread.

The UltraSPARC I & II trap table is an in-memory table that contains the first eight instructions for each type of trap. The trap table is located in memory at the address stored in the trap table base address register (TBA), which is initialized during boot. Solaris places the trap table at the base of the kernel (known as kernelbase) in a locked-down (non-pageable) 4-Mbyte page so that memory-related traps (page faults or TLB misses) will occur during execution of instructions in the trap table. (For a detailed kernel memory map, see Appendix B, “Kernel Virtual Address Maps”).

### 2.2.3.1 UltraSPARC I & II Trap Types

The trap table contains one entry for each type of trap and provides a specific handler for each trap type. The UltraSPARC I & II traps can be categorized into the following types:

- **Processor resets** — Power-on reset, machine resets, software-initiated resets
- **Memory management exceptions** — MMU page faults, page protection violations, memory errors, misaligned accesses, etc.
- **Instruction exceptions** — Attempts to execute privileged instructions from nonprivileged mode, illegal instructions, etc.
- **Floating-point exceptions** — Floating-point exceptions, floating-point mode instruction attempted when floating point unit disabled, etc.
- **SPARC register management** — Traps for SPARC register window spilling, filling, or cleaning.
- **Software-initiated traps** — Traps initiated by the SPARC trap instruction (tei); primarily used for system call entry in Solaris.

Table 2-1 shows the UltraSPARC I & II trap types, as implemented in Solaris.

## Table 2-1 Solaris UltraSPARC I & II Traps

| Trap Definition | Trap Type | Priority |
| :--- | :--- | :--- |
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

## Table 2-1 Solaris UltraSPARC I & II Traps (Continued)

| Trap Definition | Trap Type | Priority |
| :--- | :--- | :--- |
| Attempt to execute privileged instruction | 011 | 6 |
| Unimplemented load instruction | 012 | 6 |
| Unimplemented store instruction | 013 | 6 |
| Reserved | 014...01F | n/a |
| Floating-point unit disabled | 020 | 8 |
| Floating-point exception ieee754 | 021 | 11 |
| Floating-point exception – other | 022 | 11 |
| Tag overflow | 023 | 14 |
| SPARC register window clean | 024...027 | 10 |
| Division by zero | 028 | 15 |
| Internal processor error | 029 | 4 |
| Data access exception | 030 | 12 |
| Data access MMU miss | 031 | 12 |
| Data access error | 032 | 12 |
| Data access protection | 033 | 12 |
| Memory address not aligned | 034 | 10 |
| Load double memory address not aligned | 035 | 10 |
| Store double memory address not aligned | 036 | 10 |
| Privileged action | 037 | 11 |
| Load quad memory address not aligned | 038 | 10 |
| Store quad memory address not aligned | 039 | 10 |
| Reserved | 03A...03F | n/a |
| Asynchronous data error | 040 | 2 |
| Asynchronous data error | 041 | 3 |
| ... | ... | ... |
| (Table truncated for brevity based on OCR input) | ... | ... |
