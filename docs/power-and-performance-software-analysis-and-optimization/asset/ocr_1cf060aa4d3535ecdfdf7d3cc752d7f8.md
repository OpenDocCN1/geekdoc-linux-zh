# Table 1.4 Values for the MOD Field in the Mod R/M Byte (Intel Corporation, 2013)

| Value | Memory Operand | Offset Size |
|---|---|--|
| 00 | Yes | 0 |
| 01 | Yes | 1 Byte |
| 10 | Yes | 2 Bytes |
| 11 | No | 0 |

# Table 1.5 Register Encodings in Mod R/M Byte (Intel Corporation, 2013)

| Value | Register (16/8) |
|---|--|
| 000 | AX/AL |
| 001 | CX/CL |
| 010 | DX/DL |
| 011 | BX/BL |
| 100 | SP/AH |
| 101 | BP/CH |
| 110 | SI/DH |
| 111 | DI/BH |

Otherwise, the R/M field specifies how the memory operand’s address should be calculated.

The 8086, and its 16-bit successors, had some limitations on which registers and forms could be used for addressing. These restrictions were removed once the architecture expanded to 32-bits, so it doesn’t take too much to document them here.

For an example the REG field extending the opcode, consider the CMP instruction in the form that contains a 16-bit immediate against a 16-bit register. In the SDM, `CMP r16,im16` is described as `81 iw` (Intel Corporation, 2013), which means an opcode of 0x81, a Mod R/M byte with MOD = 11₂, REG = 7 = 111₂, and the R/M field encoding the 16-bit register to test. The `iw` entry specifies that a 16-bit immediate value will follow the Mod R/M byte, providing the immediate to test the register against. Therefore, `CMP DX, 0ABCD` will be encoded as: `0x81, 0xFA, 0xCD`. Notice that 0ABCD is stored byte-reversed because x86 is little-endian.

Consider another example, this performing a CMP of a 16-bit immediate against a memory operand. For this example, the memory operand is encoded as an offset from the base pointer, `BP + 8`. The CMP encoding format is the same as before,