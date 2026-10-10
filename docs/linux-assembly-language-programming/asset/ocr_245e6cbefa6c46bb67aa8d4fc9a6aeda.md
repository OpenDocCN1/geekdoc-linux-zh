``MOV EAX, EBX``
does not change the EBX register. It means

let EAX = EBX

*not* move EAX to EBX.

There are assemblers which use the opposite syntax, such as the AT&T-style assembler used by gcc. In its syntax, the exact same command is written

```
movl %ebx, %eax
```

The two registers used in a `MOV` command must be the same size. The following command, for example, is not valid.

```
MOV EBX, DX
```

# 3.11.3 Ambiguity Problem

According to the append H hex convention discussed in *chapter 2, section 2.7*, the register names `AH`, `BH`, `CH`, and `DH` are also valid hexadecimal names for the numbers ten, eleven, twelve, and thirteen. This would make commands such as

```
MOV BL, AH
```

ambiguous. This command would be a valid example of both the **reg,reg** form and the **reg,imm** form of the `MOV` command. The customary resolution of this ambiguity is to require all hexadecimal numbers used in assembly language commands to begin with one of the digits 0, 1, . . . 9. This modification of the append H convention will be observed in this text and is required by both `NASM` and `Edlinas`. Hence `MOV BL, AH` is actually not a valid example the **reg,imm** form. It is an example of the **reg,reg** form. To store the immediate value ten into `BL` we must use either

```
MOV BL, 0AH

or

MOV BL, 10
```

# 3.12 Addition and Subtraction Commands

This section describes the **reg,imm** and **reg,reg** forms of the `ADD` and `SUB` commands. These are very fundamental arithmetic instructions.

# 3.12.1 ADD reg,imm

```
ADD reg,imm
```

means to add the immediate value to the register. For example

```
ADD BL, 10
```

can be thought of as

```
let BL = BL + 10
```

# 3.12.2 ADD reg,reg