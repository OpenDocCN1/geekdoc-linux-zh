

# MOV 将右操作数移动到左操作数

影响的标志位：

```
O D I T S Z A P C OF: 溢出标志 TF: 陷阱标志 AF: 进位标志
F F F F F F F DF: 方向标志 SF: 符号标志 PF: 奇偶标志
<none>           IF: 中断标志 ZF: 零标志 CF: 进位标志
```

# 法律格式：

```
MOV r8,r8
MOV m8,r8
MOV r8,m8
MOV r8,i8
MOV m8,i8
MOV r16,r16
MOV m16,r16
MOV r16,m16
MOV m16,i16
MOV r16,i16
MOV r32,r32    386+
MOV m32,r32    386+
MOV r32,m32    386+
MOV r32,i32    386+
MOV m32,i32    386+
MOV sr,r16
MOV sr,m16
MOV r16,sr
MOV m16,sr
```

# 示例：

```
MOV AL, BH
MOV EBX, EDI
MOV BP, ES
MOV ES, AX
MOV AX,0B00H
MOV ES: [BX],0FFFFH
MOV CX, [SI+Offset]
```

# 备注：

这可能是所有指令中最常用的一个。标志位不受影响。

```
r8 = AL AH BH BL CL LD DH  r16 = AX BX CX DX BP SP SI DI
sr = CS DS SS ES FS GS          r32 = EAX EBX ECX EDX EBP ESP EDI
m8 = 8位内存数据        m16 = 16位内存数据
m32 = 32位内存数据      i8 = 8位立即数
i16 = 16位立即数   i32 = 32位立即数
d8 = 8位有符号偏移量  d16 = 16位有符号偏移量
d32 = 32位无符号偏移量
```

# 取反（补码；即乘以 -1）

影响的标志位：

O D I T S Z A P C OF: 溢出标志 TF: 陷阱标志 AF: 进位标志
F F F F F F F DF: 方向标志 SF: 符号标志 PF: 奇偶标志
* * * * * * * * IF: 中断标志 ZF: 零标志 CF: 进位标志

# 法律格式：

```
NEG r8
NEG m8
NEG r16
NEG m16
NEG r32      386+
NEG m32      386+
```

# 示例：

```
NEG AL
NEG DX
NEG ECX
NEG BYTE [BX]    ; 取反 [BX] 处的 BYTE 量
NEG WORD [DI]    ; 取反 [DI] 处的 WORD 量
NEG DWORD [EAX]  ; 取反 [EAX] 处的 DWORD 量
```

# 备注：

这是将值乘以 -1 的汇编语言等效操作。请记住，取反不等同于简单的反转操作数中的每个位。（另一个指令 NOT 才是那样的。）该过程也称为生成值的补码。一个值加上它的补码将得到零。-1 = FF；-2 = FE；-3 = FD；以此类推。

如果操作数为 0，则 CF 清零且 ZF 置位；CF 置位且 ZF 清零。如果操作数包含最大负值（8 位为 -128 或 16 位为 -32,768），则操作数不变，但 OF 和 CF 置位。如果结果为负数，否则 SF 将清零。如果结果的低 8 位包含偶数个置位（1位），则 PF 置位；否则 PF 清零。

在处理内存数据时使用大小指定符（BYTE, WORD, DWORD）：

```
r8 = AL AH BH BH CL DH DI      r16 = AX BX CX DX BP SI DI
sr = CS DS ES SS FS SS          r32 = EAX EBX ECX EDX ESP ESI EDI
m8 = 8位内存数据        m16 = 16位内存数据
m32 = 32位内存数据      i8 = 8位立即数
i16 = 16位立即数   i32 = 32位立即数
d8 = 8位有符号偏移量  d16 = 16位有符号偏移量
d32 = 32位无符号偏移量
```

# NOP 无操作

影响的标志位：

O D I T S Z A P C OF: 溢出标志 TF: 陷阱标志 AF: 进位标志
F F F F F F DF: 方向标志 SF: 符号标志 PF: 奇偶标志
<none> IF: 中断标志 ZF: 零标志 CF: 进位标志

# 法律格式：

NOP <none>

# 示例：

NOP

# 备注：

这是所有 86 系列指令中最容易理解的，它只是什么都不做。它的作用是在指令序列中占据空间。当被 CPU 取到 NOP 时，它被当做 `XCHG AX,AX` 执行。因此，实际上执行了一些工作，但没用，且没有数据被更改。标志位不受影响。NOP 用于调试、为未来的调用留出空间或用于定时循环。

```
r8 = AL AH BH CL DL DH          r16 = AX BX CX DX BP SI DI
sr = CS DS SS ES FS GS             r32 = EAX EBX ECX EDX ESP EDI
m8 = 8位内存数据          i8 = 8位立即数据
m32 = 32位内存数据          i32 = 32位立即数据
i16 = 16位立即数据          d16 = 16位有符号偏移量
d8 = 8位有符号偏移量
d32 = 32位无符号偏移量
```

# NOT 逻辑取反（反码）

影响的标志位：

O D I T S Z A P C OF: 溢出标志 TF: 陷阱标志 AF: 进位标志
F F F F F F DF: 方向标志 SF: 符号标志 PF: 奇偶标志
<none> IF: 中断标志 ZF: 零标志 CF: 进位标志

# 逻辑格式：

NOT r8
NOT m8
NOT r16
NOT m16
NOT r32 386+
NOT m32 386+

# 示例：

NOT CL
NOT DX
NOT [SI+Offset]

# 备注：

NOT 分别反转操作数中的每一位。也就是说，每个 1 变成 0，每个 0 变成 1。这是“逻辑 NOT”或“反码”操作。查看 NEG 指令的补码操作。执行 NOT 后，如果操作数之一为 0，则结果为 1；只有当两个操作数均为 0 时，结果为 0。该操作清除辅助标志位，并根据结果设置影响的标志位。注意：处理内存数据时必须使用大小指定符（BYTE, WORD, DWORD）：执行 NOT 后，FFH 会变成 0；AAH 会变成 55H。

```
r8 = AL AH BH CL DL          r16 = AX BX CX DX BP SI DI
SR = CS DS SS FS GS             r32 = EAX EBX ECX EDX ESP EDI
m8 = 8位内存数据             m16 = 16位内存数据
m32 = 32位内存数据          i8 = 8位立即数据
i16 = 16位立即数据          i32 = 32位立即数据
d8 = 8位有符号偏移量  d16 = 16位有符号偏移量
d32
```

# OR 逻辑或

影响的标志位：

O D I T S Z A P C OF: 溢出标志 TF: 陷阱标志 AF: 进位标志
F F F F F F DF: 方向标志 SF: 符号标志 PF: 奇偶标志
* * * * * * * IF: 中断标志 ZF: 零标志 CF: 进位标志

# 逻辑格式：

OR r8,r8
OR m8,r8
OR r8,m8
OR r16,r16
OR m16,r16
OR r16,m16
OR r32,r32 386+
OR m32,r32 386+
OR r32,m32 386+
OR r8,i8
OR m8,i8
OR r16,i16
OR m16,i16
OR r32,i32 386+
OR m32,i32 386+
OR AL,i8
OR AX,i16
OR EAX,i32 386+

# 示例：

OR EBX, EDI ; 使用单字节机器
OR AX, 0FFFF ; 使用单字节机器
OR AL, 42H
OR WORD [ES:BX],0B80H
OR WORD [BP+SI],DX

# 备注：

OR 在操作数之间执行 OR 逻辑操作。操作完成后，结果替换目标操作数。OR 是逐位进行的，源源 1 与目的 0 进行 OR，源操作 1 与目的 1 进行 OR，以此此类推。如果操作数之一为 1，则结果为 1，只有当两个操作数均为 0 时，结果为 0。该操作清除辅助标志，并根据结果设置影响的标志位。注意：处理内存数据时必须使用大小指定符（BYTE, WORD, DWORD）：

```
r8 = AL AH BH BH CL DH DI      r16 = AX BX CX DX BP SI DI
sr = CS DS ES SS FS SS          r32 = EAX EBX ECX EDX ESP ESI EDI
m8 = 8位内存数据        m16 = 16位内存数据
m32 = 32位内存数据      i8 = 8位立即数
i16 = 16位立即数   i32 = 32位立即数
d8 = 8位有符号偏移量  d16 = 16位有符号偏移量
d32 = 32位无符号偏移量
```

# 将栈顶弹出到操作数中

影响的标志位：

O D I T S Z A P C OF: 溢出标志 TF: 陷阱标志 AF: 进位标志
F F F F F F F DF: 方向标志 SF: 符号标志 PF: 奇偶标志
<none> IF: 中断标志 ZF: 零标志 CF: 进位标志

# 法律格式：

+ - POP r16
- POP m16
- POP r32
- POP m32
- POP sr

# 示例：

+ - POP WORD [BX]
- POP EAX
- POP DX
- POP DWORD [EAX+ECX]
- POP ES

# 备注：

从栈弹出 8 位项目是不可能的。此外记住，在 16 位模式下，栈顶定义为 SS:SP 处的字，且无法通过段前缀来覆盖它。在 32 位模式下，栈顶是 [ESP] 处的双。有一对单独的指令 PUSH 和 POPF 用于推弹出标志寄存器。

所有寄存器格式都有单字节操作码。NASM 会识别并自动生成它们，即使 CPU 指令解码逻辑中存在更大的格式。

```
r8 = AL AH BH BH CL DL DH          r16 = AX BX CX DX BP SP DI
sr = CD CD DS SS FS FS GS             r32 = EAX EBX ECX EDX EBP ESP EDI
m8 = 8位内存数据             m16 = 16位内存数据
m32 = 32位内存数据          i8 = 8位立即数据
i16 = 16位立即数据          i32 = 32位立即数据
d8 = 8位有符号偏移量  d16 = 16位有符号偏移量
d32
```

