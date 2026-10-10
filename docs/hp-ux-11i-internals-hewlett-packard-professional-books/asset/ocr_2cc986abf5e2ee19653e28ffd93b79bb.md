Table 1-1 Processor Status Word Bits (Continued)

| Field | Description |
| :--- | :--- |
| R | Recovery Counter enable. When 1, recovery counter traps occur if bit 0 of the recovery counter is a 1. This bit also enables decrementing of the recovery counter. |
| Q | Interruption state collection enable. When 1, interruption state is collected. Used in processing the interruption and returning to the interrupted code, this state is recorded in the Interruption Instruction Address Queue (IIAQ), the Interruption Instruction Register (IIR), the Interruption Space Register (ISR), and the Interruption Offset Register (IOR). |
| P | Protection identifier validation enable. When this bit and the C-bit are both equal to 1, instruction references check for valid protection identifiers (PIDs). When this bit and the Dbit are both equal to 1, data references check for valid PIDs. When this bit is 1, probe instructions check for valid PIDs. |
| D | Data address translation enable. When 1, data addresses are translated and access rights checked. |
| I | External interrupt, power failure interrupt, and low-priority machine check interruption unmask. When 1, these interruptions are unmasked and can cause an interruption. When 0, the interruptions are held pending. |

# Virtual Memory Support

In a virtual memory system, pages are mapped from one set of addresses, virtual addresses, to another set, physical addresses. Each time the processor accesses memory, it does so using a virtual address. This address then gets translated to a physical address. This mapping takes place in units of pages. When a program addresses a virtual address, that address is first broken up into a virtual page number and an offset into that virtual page. The virtual page is then translated into a physical page. It's possible that the virtual page might be on disk rather than in physical memory. In this case, a page fault is generated and the page must then be brought in from disk to memory. In this section we look at how addresses get translated. The case where data is resident on disk rather than in physical memory is covered in Chapter 6.

PA-RISC processors operate in one of two modes: narrow or wide. PA-RISC 1.1 processors are always narrow, and they operate on 32-bit addresses. PA-RISC 2.0 processors can be narrow or wide at any time depending on the setting of the W-bit in the PSW. Because the addresses are handled differently in these two cases, we look at both possibilities. We also look at the memory layout for both kernel mode and user mode. Recall that on a PA-RISC 1.1 system, the kernel and user applications are always narrow (32-bit). On a PA-RISC 2.0 system, the kernel can be narrow or wide (64-bit); on a wide kernel, applications can be either narrow or wide.