
.data

`count` `WORD` 1

.code

`mov` `ecx`,0

`mov` `cx`,`count`

```
对于等于 -16 的符号整数尝试同样的方法会发生什么？
```

.data

`signedVal` `SWORD` -16 ; FFFF0h (-16)

.code

`mov` `ecx`,0

`mov` `cx`,`signedVal`

```
ECX 中的值 (+65520) 与 -16 完全不同。相反，如果我们先填充 ECX 为 FFFFFFFF，然后将 signedVal 拷贝到 CX，最终结果将是正确的：
```

```
mov ecx,0FFFFFFFF

mov cx,signedVal ; ECX = FFFFFFFFh (-16)
```

在处理符号整数时产生了一个问题：在决定如何填充目的操作数之前，我们不想检查它们的值是正还是负。遗憾的是，Intel 的工程师在设计 Intel386 处理器时发现了这个问题，并引入了 `MOVZX` 和 `MOVSX` 指令来处理无符号和符号整数。

![](img/ea8a6a99b0e33c5c1bf5dd603b329094_132_0.png)

## 4.1.5.2 MOVZX 指令

`MOVZX` 指令（零扩展移动）将源操作数的内容复制到目标操作数，并将值零扩展到 16 位或 32 位。此指令仅用于无符号整数。共有三种变体：

```MOVZX r32, r/m8

MOVZX r32, r/m16

MOVZX r16, r/m8
```

（操作数表示法见表 4-1。）在这三种变体中，第一个操作数是目标，第二个是源源。目标操作数必须是一个寄存器。下图显示了一个 8 位源操作数被零扩展到 16 位目标操作数：

| | | |
|---|---|---|
| 0 | 10000111 | 源 |
| 00000000 | 10000111 | 目标 |

以下示例对所有操作数均使用寄存器，展示了所有的尺寸变化：

```
mov bx, 0A69Bh

movzx eax,bx  ; EAX = 0000A69Bh

movzx edx,bl ; EDX = 0000009Bh

movzx cx,bl   ; CX = 009Bh
```

以下示例源操作数使用内存操作数，产生相同的结果：

```
.data

byte BYTE 9Bh

word1 WORD 0A69Bh

.code

movzx eax,word1 ; EAX = 0000A69Bh

movzx edx,byte ; EDX = 0000009Bh

movzx cx,byte ; CX = 009Bh
```

如果你计划在实地址模式（Real-address mode）下运行并测试书籍示例，请忘记包含 `Irvine16.lib` 并在主过程开头插入以下行：

```
mov ax, @data

mov ds,ax
```

## 4.1 数据传输指令

## 4.1.5.3 MOVSX 指令

`MOVSX` 指令（符号扩展移动）将源操作数的内容复制到目标操作数，并将值符号扩展到 16 位或 32 位。此指令仅用于有符号整数。共有三种变体：

```
MOVSX r32,r/m8

MOVSX r32,r/m16

MOVSX r16,r/m8
```

操作数的符号扩展是通过取较小操作数的最高位，并将该位重复（复制）到目标操作数中所有扩展位来实现的。例如，如果将一个值为 10001111b 的 8 位值移动到 16 位目标中，低 8 位将原样复制。接下来，如图所示，最高位被复制到目标的高 8 位中的每一个位置：

![](img/ea8a6a99b0e33c5c1bf5dd603b329094_134_0.png)

以下示例对所有操作数均使用寄存器，涵盖了所有的变化：

```
mov bx,0A69Bh

movsx eax,bx

movsx edx,bl

movsx cx,bl

EAX = FFFA69Bh

EDX = FFFFFF9Bh

CX = FF9Bh
```

## 4.1.6 LAHF 和 SAHF 指令

`LAHF`（将状态标志加载到 AH）指令将 EFLAGS 寄存器的低字节复制到 AH。复制的标志包括：符号（Sign）、零（Zero）、辅助进位（Auxiliary Carry）、奇偶（Parity）和进位（Carry）。使用此指令，你可以轻松地将标志副本保存到变量中备用：

- data
saveflags BYTE ? =
- code
lahf
mov saveflags,ah
load flags 到 AH
保存变量

`SAHF`（将 AH 存储到状态标志）指令将 AH 复制到 EFLAGS 寄存器的低字节。例如，你可以检索之前保存的标志值：

```
mov ah,saveflags = 将保存的标志加载到 AH

sahf = 复制标志寄存器
```

## 4.1.7 XCHG 指令

`XCHG`（交换）指令交换两个操作数的内容。共有三种变体：

```
XCHG reg,reg

XCHG reg,mem

XCHG mem,reg
```

`XCHG` 指令的操作数规则与 `MOV` 指令（第 4.1.4 节）相同，不同之处 `XCHG` 不接受立即数（immediate operands）。

在数组排序中，`XCHG` 提供了一种交换两个数组元素的简单方法。以下是使用 `XCHG` 的示例：

```
xchg ax,bx      ; 交换 16 位寄存器

xchg ah,al      ; 交换 8 位寄存器

xchg varl,bx    ; 交换 16 位内存操作数与 BX

xchg eax,ebx     ; 交换 32 位寄存器
```

要交换两个内存操作数，使用寄存器作为临时容器并结合 `XCHG` 使用：

```
mov ax,val1

xchg ax,val2

mov val1,ax
```

## 4.1.8 直接偏移操作数

你可以在变量名后添加位移（displacement），创建一个直接偏移操作数。这允许你访问可能未被解引的内存位置。在很多情况下，位移是加在变量基地址上的。

以下示例展示了如何使用直接偏移操作数：

```
mov al, array[0]  ; 移动数组的第一个字节

mov ax, array[2]  ; 移动数组的第一个字

mov eax, array[4]  ; 移动数组的第一个双字
```

位移可以是任意常量值。例如：

```
mov al, array[5]  ; 移动数组的第 6 个字节
```

## 4.2 加法与减法

`var3` `SWORD` -16,-42
`var4` `DWORD` 1,2,3,4,5

7. 对于下列每条语句，请说明指令是否有效：
a. `mov` `ax`,`var1`
b. `mov` `ax`,`var2`
c. `mov` `eax`,`var3`
d. `mov` `var2`,`var3`
e. `movzx` `ax`,`var2`
f. `movzx` `var2`,`al`
g. `mov` `ds`,`ax`
h. `mov` `ds`,1000h

8. 在顺序执行下列每个指令后，目标操作数的十六进制值是多少？

```
mov ax,var1      ; a.

mov ah, [var1+3] ; b.
```

9. 在顺序执行下列每个指令后，目标操作数的值是多少？

```
mov ax,var2      ; a.

mov ax, [var2+4]  ; b.

mov ax,var3      ; c.

mov ax, [var3-2]  ; d.
```

10. 在顺序执行下列每个指令后，目标操作数的值是多少？

```
mov edx,var4     ; a.

movzx edx,var2   ; b.

mov edx,[var4+4] ; c.

movsx edx,var1   ; d.
```

## 4.2 加法与减法

整数加法和减法是 CPU 可以执行的最基础的操作之一。在本节中，我们将探索执行二进制加法和减法的指令：`INC`（增）、`DEC`（递减）、`ADD`（加）、`SUB`（减）和 `NEG`（取反）。

### 4.2.1 INC 和 DEC 指令

`INC`（增）和 `DEC`（递减）指令分别对单个操作数加 1 或减 1。其语法如下：

```
INC reg/mem

DEC reg/mem
```

# 第 4 章 · 数据传输、寻址与算术

以下是一些示例：

```
.data

myWord WORD 1000h

.code

inc myWord ; 1001h

mov bx,myWord

dec bx ; 1000h
```

### 4.2.2 ADD 指令

`ADD` 指令将源操作数加到相同大小的目标操作数上。其语法为：

```
ADD dest, source
```

操作后源操作数不变，和存储在目标操作数中。可能的操作数集合与 `MOV` 指令相同（见第 4.1.4 节）。这里有一个加上两个 32 位整数的短代码示例：

```
.data

var1 DWORD 10000h

var2 DWORD 20000h

.code

mov eax,var1

add eax,var2 ; 30000h
```

**标志** 进位、零、符号、溢出、辅助进位和奇偶标志会根据目标操作数的值改变。我们将在 4.2.6 节中详细说明标志值。

### 4.2.3 SUB 指令

`SUB` 指令从目标操作数减去源操作数。可能的操作数集合与 `ADD` 和 `MOV` 指令相同（见第 4.1.4 节）。其语法为：

```
SUB dest, source
```

这是一个减去两个 32 位整数的短代码示例：

```
.data

var1 DWORD 30000h

var2 DWORD 10000h

.code

mov eax,var1

sub eax,var2 ; 20000h
```

CPU 通过先取反后相来执行减法。例如，4 - -1 实际上是 4 + (-1)。记住，负数使用补码表示，因此 -1 表示为 11111111，如下所示：

## 4.2 加法与减法

| 进位: | 1 1 1 1 1 1 |
|---|---|
| | 0 0 0 0 0 1 0 0 | (4) |
| + | 1 1 1 1 1 1 1 | (-1) |
| | 0 0 0 0 0 1 1 | (3) |

这次加法在最高位处产生了一个进位，但对于所有符号算术运算，进位都会被忽略。

**标志** 进位、零、符号、溢出、辅助进位和奇偶标志会根据目标操作数的值改变。我们将在 4.2.6 节中详细说明此。

### 4.2.4 NEG 指令

`NEG`（取反）指令通过将数字转换为其补码来改变数字的符号。允许以下操作数：

```
NEG reg

NEG mem
```

记住，数字的补码可以通过反转目标操作中的所有位并加 1 来得到。

**标志** 进位、零、符号、溢出、辅助进位和奇偶标志会根据目标操作数的值改变。我们将在 4.2.6 节中详细说明此。

### 4.2.5 实现算术表达式

掌握了 `ADD`、`SUB` 和 `NEG` 指令后，你现在有了可以在汇编语言中实现涉及加法、减法和取反算术表达式。换句话说，我们可以模拟 C++ 在读取如下表达式时可能执行的操作：

```
Rval = -Xval + (Yval - Zval);
```

将使用以下 32 位变量：

```
Rval SDWORD ?

Xval SDWORD 26

Yval SDWORD 30

Zval SDWORD 40
```

在翻译表达式时，最好单独评估每个项并在最后组合它们。首先，我们对 Xval 取反：

```
; 首先: -Xval

mov eax, Xval

neg eax      ; EAX = -26
```

将 Yval 复制到寄存器并从中减去 Zval：

```
; 第二项: (Yval - Zval)

mov ebx, Yval

sub ebx, Zval          ; EBX = -10
```

最后，将这两个项（在 EAX 和 EBX 中）相加：

```
; 相加并存储：

add eax, ebx

mov rval, eax         
```

## 4.2.6 受算术影响的标志

当程序执行算术运算时，可能会发生溢出（值太大或太小）。高阶语言通常不检测整数溢出。而在汇编语言中，你对溢出错误有很好的控制，因为你可以在每次操作后检查标志位。

本节对标志的讨论适用于 `ADD`、`SUB`、`INC` 和 `DEC` 指令。其他标志（辅助进位和奇偶标志）不那么重要，将在稍后讨论。

> 你可以通过调用第 3 章所示的 Dumps 过程在程序中显示 CPU 标志。

### 4.2.6.1 零标志和符号标志

当算术指令的目标操作数赋值为零时，零标志被置。例如：

```
mov cx, 1

sub cx, 1            ; CX = 0, ZF = 1

mov ax, 0FFFFFFh      ; AX = 0, ZF = 1

inc ax               ; AX = 1, ZF = 0
```

当算术运算的结果为负数时，符号标志被置。例如：

```
mov cx, 1

sub cx, 1            ; CX = 0, SF = 0
```

### 4.2.6.2 进位标志（无符号）

当无符号运算的结果对于目标操作数来说太大或太小时，进位标志被置。如果我们从较小的整数中减去较大的整数，进位标志会被置。

### 4.2.6.3 溢出标志（符号算术）

溢出标志仅在执行符号算术运算时有效。具体来说，当算术运算产生一个无法放入目标操作数的符号时，溢出标志被置。

## 4.2 加法与减法

学生经常问，CPU 是如何知道一个数字是有符号的还是无符号的。人们只能给出一个似乎很愚蠢的答案：CPU 并不知道——只有程序员才知道。CPU 在执行操作后会设置所有的状态标志位，而不知道这些标志位中哪些对程序员是重要的。程序员决定解释哪些标志，忽略哪些标志。

## 4.2.7 示例程序 (AddSub3)

让我们来看简单的示例程序，该程序演示了 `ADD`、`SUB`、`INC`、`DEC` 和 `NEG` 指令，并展示了 CPU 状态标志位是如何变化的：

```
TITLE Addition and Subtraction                (AddSub3.asm)

INCLUDE Irvine32.inc

.data

Rval SDWORD ?

nXval SDWORD 26

Yval SDWORD 30

Zval SDWORD 40

.code

main PROC

    ; INC and DEC

    mov ax, 1000h

    inc ax                          ; 1001h

    dec ax                          ; 1000h

    ; 表达式: Rval = -Xval + (Yval - Zval)

    mov eax, Xval

    neg eax                         ; -26

    mov ebx, Yval

    sub ebx, Zval                   ; -10

    add eax,ebx

    mov Rval,eax                   ; -36

    ; 零标志示例:

    mov cx,1

    sub cx,1                        ; ZF = 1

    mov ax,0FFFF

    inc ax                          ; ZF = 1

    ; 符号标志示例:

    mov cx,0

    sub cx,1                        ; SF = 1

    mov ax,7FFFF

    add ax,2                        ; SF = 1

    ; 进位标志示例:

    mov al,0FFh

    add al,1                        ; CF = 1,  AL = 00

    ; 溢标志示例:

    mov al,+127

    add al,1          ; OF = 1

    mov al,-128

    sub al,1          ; OF = 1

main

exit

ENDP

END main
```

## 4.2.8 节复习

使用以下数据回答接几个问题：

```
.data

val1 BYTE 10h

val2 WORD 8000h

val3 DWORD 0FFFFh

val4 WORD 7FFFh
```

- 1. 编写一条减去 val2 的指令。
2. 编写一条从 EAX 中减去 val3 的指令。
3. 编写一条或多条指令从 val2 中减去 val4。
4. 如果使用 ADD 指令将 val2 加 1，进位标志（Carry flag）和符号标志（Sign flag）的值是多少？
5. 如果使用 ADD 指令将 val4 加 1，溢出标志（Overflow flag）和符号标志（Sign flag）的值是多少？
6. 在指示处，写下每条指令执行后进位标志（Carry）、符号标志（Sign）、零标志（Zero）和溢出标志（Overflow）的值：

```
mov ax,7FF0h

add al,10h      ; a. CF = SF = ZF = OF =

add ah,1         ; b. CF = SF = ZF = OF =

add ax,2         ; c. CF = SF = ZF = OF =
```
