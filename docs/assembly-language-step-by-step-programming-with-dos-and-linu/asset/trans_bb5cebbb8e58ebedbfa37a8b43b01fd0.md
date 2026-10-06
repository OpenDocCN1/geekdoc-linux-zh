

# PUSHF 将 16 位标志位压入栈

## 受影响的标志位：

O D I T S Z A P C OF: 溢出标志 TF: 陷阱标志 AF: 进位标志
F F F F F F F DF: 方向标志 SF: 符号标志 PF: 奇偶性标志
<none> IF: 中断标志 ZF: 零标志 CF: 进位标志

## 合法形式：

PUSHHF <none>

## 示例：

PUSHF

## 注意：

PUSHF 简单地将标志寄存器的当前内容推入栈顶。栈顶定义为 SS:SP 处的字，且无法通过前缀来覆盖它。

在字进入栈之前，SP 会被减小。请记住，SP 始终指向空栈或实际数据。有一对单独指令 PUSH 和 POP，用于推入和弹出其他寄存器数据和内存数据。

当推入标志位时，标志寄存器不会受到影响，只有当使用 POPF 将其弹出回时才会受影响。

PUSHF 和 POPF 最用于编写中断服务例程序，在这些程序中，你必须能够保存和恢复环境（即所有机器寄存器），以避免在处理中断时干扰机器操作。

```
r8 = AH BL BH CL CL DH
r16 = AX CX DX BP SP SI DI
sr = CS DS SS ES FS GS
r32 = EAX EBX ECX EBP ESP E EDI
m8 = 8 位内存数据
m16 = 16 位内存数据
m32 = 32 位内存数据
i8 = 8 位立即数
i16 = 16 位立即数
i32 = 32 位立即数
d8 = 8 位符号位移量
d16 = 16 位符号位移量
d32 = 32 位无符号位移量
```

# PUSHFD 将 32 位 EFlags 标志压入栈 (386+)

## 受影响的标志位：

```
  O D I T S Z A P C  OF: 溢出标志 TF: 陷阱标志 AF: 进位标志
  F F F F F F F DF: 方向标志 SF: 符号标志 PF: 奇偶性标志
  <none>             IF: 中断标志 ZF: 零标志 CF: 进位标志
```

## 合法形式：

```
PUSHFD <none>      386+
```

## 示例：

```
PUSHFD
```

## 注意：

PUSHFD 简单地将 32 位 EFlags 寄存器的当前内容推入栈顶。32 位模式下的栈顶定义为 [SS:ESP] 处的字，且无法通过前缀指定顺序。

在 EFlags 双字进入栈之前，ESP 会被减小。请记住，ESP 始终指向空栈或实际数据。有一对单独指令 PUSH 和 POP 用于推入和弹出其他寄存器数据、内存数据（在 286 及后续处理器中包括立即数）。

当推入标志位时，EFlags 寄存器不会受到影响，只有当使用 POPFD 将其弹出回时才会受影响。

PUSHFD 和 POPFD 最用于编写中断服务程序，在这些程序中，你必须能够保存和恢复环境（即所有机器寄存器），以避免在处理中断时干扰机器操作。

```
r8 = AX AH BH BH CL CL DL DH      r16 = AX BX CX DX BP SP SI DI
sr = CS DS SS ES FS GS                                         r32 = EAX EBX ECX EDX EBP EDI ESI EDI
m8 = 8 位立即数               m16 = 16 位内存数据
m32 = 32 位内存数据               i8 = 8 位立即数
i16 = 16 位立即数             i32 = 32 位立即数
d8 = 8 位符号位移量        d16 = 16 位符号位移量
d32 = 32 位无符号位移量
```

# RET 从过程返回

## 受影响的标志位：

O D I T Z A P C OF: 溢出标志 TF: 陷阱标志 AF: 进位标志
F F F F F F F DF: 方向标志 SF: 符号标志 PF: 奇偶性标志
<none> IF: 中断标志 ZF: 零标志 CF: 进位标志

## 合法形式：

- RET
- RETN
- RETF
- RET i8
- RETN i8
- RET i16
- RETF i16

## 示例：

- RET
- RET 12H
- RETN
- RETF 17H

## 注意：

返回有两种类型：近返回（Near）和远返回（Far），近返回在当前代码段内，远返回跳转到其他段。通常使用 RET 形式，汇编器将其解析为近返回或远返回反对，以匹配过程定义时使用的 NEAR 或 FAR 饰符。在必要时可以指定 RETF 或 RETN。

RET 可以接受一个操作数，指示从过程返回时要释放多少字节的栈空间。该数值从栈指针中减去，以消除在调用之前之前为过程使用而推入栈的项。

RET 和 RETN 形式在 MASM V5.0 之后不可用！

```
r8 = AL AH BH CH CL DH r16 = AX BX CX DX BP SI DI
sr = CS CS SI SI ES FS GS r32 = EAX EBX ECX EDX EBP ESP ESI EDI
m8 = 8 位内存数据 m16 = 16 位内存数据
m32 = 32 位内存数据 i8 = 8 位立即数据
i16 = 16 位立即数据 i32 = 32 位立即数据
d8 = 8 位符号位移量 d16 = 16 位符号位移量
d32 = 32 位无符号位移量
```

# ROL 左循环

## 受影响的标志位：

O D I T S A P C OF: 溢出标志 TF: 陷阱标志 AF: 进位标志
F F F F F F DF: 方向标志 SF: 符号标志 PF: 奇偶性标志
IF: 中断标志 ZF: 零标志 CF: 进位标志

## 合法形式：

- ROL r8,1
- ROL m8,1
- ROL r16,1
- ROL m16,1
- ROL r32,1 386+
- ROL m32,1 386+
- ROL r8,CL
- ROL m8,CL
- ROL r16,CL
- ROL m16,CL
- ROL r32,CL 386+
- ROL m32,CL 386+
- ROL r8,i8 286+
- ROL m8,i8 286+
- ROL r16,i8 286+
- ROL m16,i8 286+
- ROL r32,i8 386+
- ROL m32,i8 386+

## 示例：

- ROL AL,1
- ROL WORD [BX+SI], CL
- ROL BP,1
- ROL DWORD [EBX+ESI], 9
- ROL BP, CL

## 注意：

ROL 将目标操作数内的位左循环，左侧指向最高位（MSB）。循环是一种循环移位（参见 SHL 和 SHR）；操作数的最左位移到最右位，所有中间位向左移动一位。除了移动一位的情况外，ROL 与 ROR 相同。

移动的位数可以是 8 位立即值，也可以是 CL 中的值——而不是 CX 或 ECX（8086 和 8088 限制为立即值 1）。注意 CL 可以接受高达 255 的值，但移动大于 16 或 32 的值没有意义，尽管在 8086 和 8088 上实际上执行了移位。（286 及后续版本在运行虚拟 80 模式时将移位操作限制为原生字长。）

每次移位会将最左位复制到进位标志。只有 ROL 移动一位的形式会修改 OF；移动 CL 的形式后，OF 未定义。

```
r8 = AL AH BH CH DL DH    r16 = AX BX CX DX BP SI DI
sr = CS DS SS ES FS GS                r32 = EAX EBX ECX EDX EBP ESI EDI
m8 = 8 位内存数据                  m16 = 16 位内存数据
m32 = 32 位内存数据               i8 = 8 位立即数据
i16 = 16 位立即数据             i32 = 32 位立即数据
d8 = 8 位符号位移量        d16 = 16 位符号位移量
d32 = 32 位无符号位移量
```

# ROR 右循环

## 受影响的标志位：

O D I T Z A P C OF: 溢出标志 TF: 陷阱标志 AF: 进位标志
F F F F F F F DF: 方向标志 SF: 符号标志 PF: 奇偶性标志
IF: 中断标志 ZF: 零标志 CF: 进位标志

## 合法形式：

- ROR r8,1
- ROR m8,1
- ROR r16,1
- ROR m16,1
- ROR r32,1 386+
- ROR m32,1 386+
- ROR r8,CL
- ROR m8,CL
- ROR r16,CL
- ROR m16,CL
- ROR r32,CL 386+
- ROR m32,CL 386+
- ROR r8,i8 286+
- ROR m8,i8 286+
- ROR r16,i8 286+
- ROR m16,i8 286+
- ROR r32,i8 386+
- ROR m32,i8 386+

## 示例：

- ROR AL,1
- ROR WORD [BX+SI], CL
- ROR BP,1
- ROR DWORD [EBX+ESI], 9
- ROR BP,CL

## 注意：

ROR 将目标操作数内的位右循环，右侧指向最低位（LSB）。循环是一种循环移位（参见 SHL 和 SHR）；操作数的最右位移到最左位，所有中间位向右移动一位。对于移位操作采取的方向，ROR 与 R 相同。

移动的位数可以指定为 8 位立即值，也可以是 CL 中的值——而不是 CX 或 ECX（8086 和 8088 限制为立即值 1）。注意 CL 可以接受高达 255 的值，但在 32 位模式下，移动大于 16 或 32 的值没有意义，尽管在 8086 和 8088 上实际上执行了移位。（286 及后续版本在运行虚拟 80 模式时将执行的移位操作限制为原生字长。）

