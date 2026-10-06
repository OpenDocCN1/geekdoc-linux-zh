
每次移位操作会将最右侧的位复制到进位标志（Carry flag）。OF 仅由 ROR 的移一位形式修改；在移位 CL 形式之后，OF 变为未定义。

```
r8 = AL AH BL BH CH CL DH  r16 = AX BX CX DX BP SP SI DI
sr = CS DS SS ES FS GS        r32 = EAX EBX ECX EDX EBP ESP EDI
m8 = 8-位内存数据       ml16 = 8-位内存数据
m32 = 32-位内存数据      i8 = 8-位立即数
i16 = 16-位立即数  i32 = 32-位立即数
d8 = 8-位符号位位移 d16 = 16-位符号位移
d32 = 32-位无符号位移
```

582 汇编语言逐步进阶

## SBB 借位减法

### 受影响的标志位：

O D I T S Z A P C OF: 溢出标志 TF: 陷阱标志 AF: 辅助进位
F F F F F F F F DF: 方向标志 SF: 符号标志 PF: 奇偶标志
* * * * * * IF: 中断标志 ZF: 零标志 CF: 进位标志

### 合法形式：

```
SBB r8,r8
SBB m8,r8
SBB r8,m8
SBB r16,r16
SBB m16,r16
SBB r16,m16
SBB r32,r32      386+
SBB m32,r32      386+
SBB r32,m32      386+
SBB r8,i8
SBB m8,i8
SBB r16,i16
SBB m16,i16
SBB r32,i32
SBB m32,i32      386+
SBB r16,i18
SBB m16,i18
SBB r32,i18      386+
SBB m32,i18      386+
SBB AL,i16
SBB AX,i16
SBB EAX,i32      386+
```

### 示例：

```
SBB BX,DI                ;使用单字节操作码
SBB AX,0FFFF               ;使用单字节操作码
SBB AL,42H
SBB BY,17H
SBB WORD [BX+SI],5
SBB WORD [ES:BX],0B00H
```

### 注意事项：

SBB 执行借位减法，用目标操作数减源操作数，然后从结果中减去进位标志（Carry flag）。结果替换目标操作数。如果结果为负，则设置进位标志。若要在不考虑进位标志的情况下进行减法（即不借位），请使用 SUB 指令（注：此处原文可能误为 SBB，根据语境应为 SUB）。

```
r8 = AL AH BL BH CL DL DH      r16 = AX BX CX ECX EDX EBP SI DI
sr = CS DS ES FS GS             r32 = EAX ECX EBP EDI
m8 = 8-位数据                 m16 = 16-位内存数据
m32 = 32-位内存数据       i8 = 8-位立即数
i16 = 16-位立即数    i32 = 32-位立即数
d8 = 8-位符号位位移  d16 = 16-位符号位移
d32 = 32-位无符号位移  
```

## 8086/8088 指令集部分参考 583

## SHL 左移

### 受影响的标志位：

```
O D I T S Z A P C OF: 溢出标志 TF: 陷阱标志 AF: 辅助进位
F F F F F F F DF: 方向标志 SF: 符号标志 PF: 奇偶标志
* * * * * IF: 中断标志 ZF: 零标志 CF: 进位标志
```

### 合法形式：

```
SHL r8,1
SHL m8,1
SHL r16,1
SHL m16,1
SHL r32,1    386+
SHL m32,1    386+
SHL r8,CL
SHL m8,CL
SHL r16,CL
SHL m16,CL
SHL r32,CL    386+
SHL m32,CL    386+
SHL r8,i8    286+
SHL m8,i8    286+
SHL r16,i8   286+
SHL m16,i8   286+
SHL r32,i8   386+
SHL m32,i8   386+
```

### 示例：

```
SHL AL,1
SHL WORD [BX+SI],CL
SHL BP,1
SHL EAX,9
SHL BP,CL
```

### 注意事项：

SHL 将目标操作数内的位向左移动，左侧为最高位（MSB）。移位位数可以是 8-位立即数，可以是 CL 中的值——而不是 CX 或 ECX（8086 和 8088 限制为值 1）。注意 CL 可以接受高达 255 的值，这意味着可以移位大于 16（在 32 位模式下为 32）的值，尽管在 8086 和 8088 上实际上执行这些移位（286 及后续版本将移位操作限制在原生字长，除非运行虚拟 86 模式）。操作数的最左位移入进位标志；最右位清零。辅助进位标志（AF）在该指令后变为未定义。OF 仅由 SHL 的移一位形式修改；在移位 CL 形式之后，OF 变为未定义。

SHL 是 SAL（左移）的同义词。除了移位方向外，SHL 与 SHR 相同。

```
r8 = AL AH BL BH CH DL DH      r16 = AX BX CX DX BP SI DI
sr = CS DS SS FS GS               r32 = EAX EBX ECX EDX EBP ESP EDI
m8 = 8-位内存数据               ml16 = 16-位内存数据
m32 = 32-位内存数据            i8 = 8-位立即数据
i16 = 16-位立即数据         i32 = 32-位立即数据
d8 = 8-位符号位位移      d16 = 16-位符号位移
d32 = 32-位无符号位移
```

## SHR 右移

### 受影响的标志位：

O D I T S Z A P C OF: 溢出标志 TF: 陷阱标志 AF: 辅助进位
F F F F F F F DF: 方向标志 SF: 符号标志 PF: 奇偶标志
* * * * * IF: 中断标志 ZF: 零标志 CF: 进位标志

### 合法形式：

```
SHR r8,1
SHR m8,1
SHR r16,1
SHR m16,1
SHR r32,1    386+
SHR m32,1    386+
SHR r8,CL
SHR m8,CL
SHR r16,CL
SHR m16,CL
SHR r32,CL    386+
SHR m32,CL    386+
SHR r8,i8    286+
SHR m8,i8    286+
SHR r16,i8   286+
SHR m16,i8   286+
SHR r32,i8   386+
SHR m32,i8   286+
```

### 示例：

```
SHR AL,1
SHR WORD [BX+SI],CL
SHR BP,1
SHR EAX,9
SHR BP,CL
```

### 注意事项：

SHR 将目标操作数内的位向右移动，右侧为最低位（LSB）。移位位数可以是 8-位立即数，也可以是 CL 中的值——而不是 CX 或 ECX（8086 和 8088 限制为恒等值 1）。注意 CL 可以接受高达 255 的值，移位任何大于 16（在 32 位模式下为 32）的值是没有意义的，尽管在 8086 和 8088 上实际上执行这些移位（286 及后续版本将移位操作限制在原生字长，除非运行虚拟 86 模式）。操作数的最右侧位移入进位标志；最低位清零。辅助进位标志（AF）在该指令后变为未定义。OF 仅由 SHL 的移一位形式修改；在移位 CL 形式之后，OF 变为未定义。

586 汇编语言逐步进阶

SHR 是 SAR（右移）的同义词。除了移位方向外，SAR 与 SHL 相同。

```
r8 = AL AH BL BH CH DL DH      r16 = AX BX CX DX BP SI DI
sr = CS DS SS FS GS                r32 = EAX EBX ECX EDX EBP ESP EDI
m8 = 8-位内存数据               ml16 = 16-位内存数据
m32 = 32-位内存数据              i8 = 8-位立即数据
i16 = 16-位立即数据             i32 = 32-位立即数据
d8 = 8-位符号位位移      d16 = 16-位符号位移
d32 = 32-位无符号位移
```

## STC 设置进位标志 (CF)

### 受影响的标志位：

O D I T S Z A P C OF: 溢出标志 TF: 陷阱标志 AF: 辅助进位
F F F F F F F DF: 方向标志 SF: 符号标志 PF: 奇偶标志
IF: 中断标志 ZF: 零标志 CF: 进位标志

### 合法形式：

STC <none>

### 示例：

STC

### 注意事项：

STC 将进位标志（CF）置为已知状态（1）。在需要进位标志的任务之前使用它。它也可以在从过程返回之前将 CF 置于已知状态，以根据需要指示过程成功或失败。

```
r8 = AL AH BL BH CH DL DH          r16 = AX BX CX DX BP SI DI
sr = CS DS SS FS GS                r32 = EAX EBX ECX EDX EBP ESP ESI EDI
m8 = 8-位内存数据               m16 = 16-位内存数据
m32 = 32-位内存数据              i8 = 8-位立即数据
i16 = 16-位立即数据             i32 = 32-位立即数据
d8 = 8-位符号位位移      d16 = 16-位符号位移
d32 = 32-位无符号位移
```

## STD 设置方向标志 (DF)

### 受影响的标志位：

O D I T S Z A P C OF: 溢出标志 TF: 陷阱标志 AF: 辅助进位
F F F F F F F DF: 方向标志 SF: 符号标志 PF: 奇偶标志
IF: 中断标志 ZF: 零标志 CF: 进位标志

### 合法形式：

STD <none>

### 示例：

STD

### 注意事项：

STD 仅仅将方向标志（DF）置为设置（1）状态。这会影响重复字符串指令（如 STOS、SCAS 和 MOVS）执行的调整。通常，当 DF = 0 时，目标指针增加；当 DF = 1 被通过 CLD 指令设置为 0 时，指针减少。
```