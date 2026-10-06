

# STOS 存储字符串

影响的标志位：

O D I T S Z A P C OF: 溢出标志 TF: 陷阱标志 AF: 辅助位
F F F F F F F DF: 方向标志 SF: 符号标志 PF: 奇偶标志
<none> IF: 中断标志 ZF: 零标志 CF: 进位标志

# 合法形式：

- STOS ES:m8
- STOS ES:m16
- STOSB
- STOSW
- STOSD 38+

# 示例：

- STOS ES:WordVar ; 将 AX 存储到 [ES:DI]
- STOS ES:ByteVar ; 将 AL 存储到 [ES:DI]
- STOSB ; 将 AL 存储到 [ES:DI]
- STOSW ; 将 AX 存储到 [ES:DI]
- STOSD ; 将 EAX 存储到 [EDI]
- REP STOS ; 将 AX 存储到 [ES:DI]后续位置，重复 CX 次

# 注意事项：

在 [ES:DI] 或 [EDI] 处存储 AL（用于8位操作）、AX（用于16位操作）或 EAX（用于32位操作）。ES 必须是目标段且不能被重写。（对于位保护模式的平坦模型，所有段都是同价的，不需要显式指定 ES）。同样，DI 或 EDI 必须始终是目标偏移量。

通过在 CX/ECX 中放入重复计数（不是字节、字或双字！）并在助记前加上 REP 前缀，STOS 可以自动向从 [ES:DI] 或 [EDI] 开始的连续内存位置进行“机枪式”AL/AX/EAX 存储。在每次存储后，DI/EDI 会调整 1（用于8位存储操作）、2（用于16位存储操作）或 4（用于32位存储操作），CX 减 1。不要忘记 CX/ECX 操作的是存储到内存的数据个数，而不是字节！

调整意味着如果方向标志被清除（通过 CLD）则进行递增，如果方向标志已设置则进行递减。

```
r8 = AL AH BH CL CH DL DH r16 = AX CX DX BP SP SI DI
sr = CD DS SS ES FS GS EAX EBX ECX EDX EBP ESI EDI
m8 = 8-bit memory data m16 = 16-bit memory data
m32 = 32-bit memory data i8 = 8-bit immediate data
i16 = 16-bit immediate data i32 = 32-bit immediate data
d8 = 8-bit signed displacement d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```

# SUB 算术减法

影响的标志位：

O D I T Z A P C OF: 溢出标志 TF: 陷阱标志 AF: 辅助位
F F F F F F F DF: 方向标志 SF: 符号标志 PF: 奇偶标志
* * * * * * * IF: 中断标志 ZF: 零标志 CF: 进位标志

# 合法形式：

```
SUB r8,r8
SUB m8,r8
SUB r8,m8
SUB r16,r16
SUB m16,r16
SUB r16,m16
SUB r32,r32 38+
SUB m32,r32 38+
SUB r32,m32 38+
SUB r8,i8
SUB m8,i8
SUB r16,i16
SUB m16,i16
SUB r32,i32 38+
SUB m32,i32 38+
SUB AL,i8
SUB AX,i16
SUB EAX,i32 38+
```

# 示例：

- SUB BX,DI ; 使用单字节操作码
- SUB AX,0FFFF ; 使用单字节操作码（注意：可能是 0FFFFH 或类似）
- SUB AL,42H ; 使用单字节操作码
- SUB EBX, DWORD [EDI]
- SUB WORD [ES:BX],0B0H
- SUB WORD [BX+SI],DX

# 注意事项：

SUB 执行不借位的减法，源操作减去目标操作，结果替换目标。如果结果为负数，则设置进位标志。通过在 SUB 后跟随 SBB（带借位减法）可以执行多精度减法，SBB 会考虑进位标志。

```
r8 = AL AH BH CL CH DL DH r16 = AX CX DX BP SP SI DI
sr = CD DS SS ES FS GS EAX EBX ECX EDX EBP ESI EDI
m8 = 8-bit memory data m16 = 16-bit memory data
m32 = 32-bit memory data i8 = 8-bit immediate data
i16 = 16-bit immediate data i32 = 32-bit immediate data
d8 = 8-bit signed displacement d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```

# XOR 异或或

影响的标志位：

O D I T S Z A P C OF: 溢出标志 TF: 陷阱标志 AF: 辅助位
F F F F F F F DF: 方向标志 SF: 符号标志 PF: 奇偶标志
* * * * * * * IF: 中断标志 ZF: 零标志 CF: 进位标志

# 合法形式：

```
XOR r8,r8
XOR m8,r8
XOR r8,m8
XOR r16,r16
XOR m16,r16
XOR r16,m16
XOR r32,r32 38+
XOR m32,r32 38+
XOR r32,m32 38+
XOR r8,i8
XOR m8,i8
XOR r16,i16
XOR m16,i16
XOR r32,i32 38+
XOR m32,i32 38+
XOR AL,i8
XOR AX,i16
XOR EAX,i32 38+
```

# 示例：

- XOR BX,DI ; 使用单字节操作码
- XOR AX,0FFFF ; 使用单字节操作码（注意：可能是 0FFFFH 或类似）
- XOR AL,42H ; 使用单字节操作码
- XOR EBX, DWORD [EDI]
- XOR WORD [ES:BX],0B0H
- XOR WORD [BX+SI],DX

# 注意事项：

XOR 在两个操作数之间执行异或操作，源操作数与目标操作异或，结果替换目标。如果操作数相同，则设置零标志为 0。

```
r8 = AL AH BH CL CH DL DH r16 = AX CX DX BP SP SI DI
sr = CD DS SS ES FS GS EAX EBX ECX EDX EBP ESI EDI
m8 = 8-bit memory data m16 = 16-bit memory data
m32 = 32-bit memory data i8 = 8-bit immediate data
i16 = 16-bit immediate data i32 = 32-bit immediate data
d8 = 8-bit signed displacement d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```

# 段寄存器的段假设

在实模式下，关于如何使用段有许多假设。在 32 位模式下（如 Linux），所有段都指向相同的空间，因此不需要“弄”段。在允许的情况下，可以使用段前缀。这些是 DS；SS；CS 和 ES。在 NASM 中，它们必须放在括号内（MASM 和 TASM 则相反）。

```
mov [ES:BX], AX
```

假设：

- 1. 当偏移量指定 BX、SI 或 DI 时，假设段为 DS。
- 2. 当偏移量指定 SP 时，假设段为 SS。
- 3. 当偏移量指定 BP 时，假设段为 SS。
- 4. 对于字符串指令 LODS，段为 DS，偏移为 SI。不可不可覆盖！
- 5. 对于字符串指令 STOS 和 SCAS，段为 ES，偏移为 DI。不可覆盖！
- 6. 对于字符串指令 MOVS，源必须指向 DS:SI，目标必须指向 ES:DI。不可覆盖！

# 汇编程序员的 Web URL

汇编语言书籍已绝版，但大量的汇编信息可以在 Web 上找到。我在下面的列表中列了一些 2000 年初有效的网站。Web 地址以令人恼火的频率更改或失效，因此如果找不到这些网站，请首先假设它们已经移动，只有在搜索引擎搜索无果后，才假设网站已永久消失。（对于某些像 NASM 这样的东西，你几乎可以假设它已经移动了！）

- NASM 主页：www.web-sites.co.uk/nasm/
- ALINK 主页：http://alink.home.dhs.org/
- NASM-IDE 主页：www://inglenook.co.uk/naside/
- Linux 汇编语言页：http://lightning.voshod.com/asm/
- Jan 的 Linux 汇编语言页：http://bewoner.dma.be/JanW/eng.html

