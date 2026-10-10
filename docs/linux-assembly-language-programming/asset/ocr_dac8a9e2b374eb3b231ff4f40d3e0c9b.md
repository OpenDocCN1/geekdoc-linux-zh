![](bbox=[0.17, 0.01, 0.86, 0.25])

# 12.1.2 Segment:Offset Notation

Suppose now that we would like to refer to the memory whose address is 23456H in an assembler command. This address lies in the DS segment. (This is because 2000H was just stored in the DS register.) It is 3456H bytes from the base address. This difference, the address minus the base address, is called the offset. The segment:offset pair is often used in the assembly language as follows:

```
MOV BL, DS:[3456H]
```

In NASM the syntax is

```
MOV BL, [DS:3456H]
```

This command loads the contents of memory location 23456H into BL. 23456H = 20000H + 3456H. Note that the base address itself is a five-digit hex number, even though DS only holds four digits, in this case 2000H.

The address 23456H is a physical address, not a virtual address. The bits which the processor pumps out onto the address bus may be read off the binary number

```
0010 0011 0100 0101 0110
```

The same memory read could be accomplished using a 16-bit address register as follows:

```
MOV BX, 3456H
MOV BL, [DS:BX]
```

BX, BP, SI, and DI may be used for addressing in this way, but SP, AX, CX, and DX may not.

# 12.1.3 Default Segments

Segment designations may be omitted. There is always a default segment. Referring to Table 12.1, we see that the default segment for an immediate address is the DS segment. Hence the command

```
MOV BL, [3456H]
```

also accomplishes the same load as the MOV BL, [DS:BX] instruction. So do the commands

```
MOV BX, 3456H
MOV BL, [BX]
```

Table 12.1. Default Segments
| 32-bit address | 16-bit address |
| --- | --- |
| [imm] | DS |
| (A X) | DS |
| [imm] | DS |
| (A X) | DS |