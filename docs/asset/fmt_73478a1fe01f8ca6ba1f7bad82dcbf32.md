
可选地可以使用 `OFFSET` 操作符使关系更清晰。在定义变量时，`TYPEDEF` 操作符让你创建一个具有内置类型状态自定义类型。`TYPEDEF` 是创建指针变量的理想选择。

示例程序：指针。以下程序 (`pointers.asm`) 使用 `TYPEDEF` 创建了三个指针类型（`PBYTE`、`PWORD`），并在运行时它们以从数组检索数据：

```
INCLUDE Irvine32.inc

; 创建自定义类型。

PBYTE TYEDEF PTR BYTE    ; 指向字节的指针

PWORD TYEDEF PTR WORD     ; 指向字的指针

DWORD TYEDEF PTR DWORD   ; 指向双字的指针
```

```
.data

arrayB BYTE 10h,20h,30h,40h

arrayW WORD 1,2,3

arrayD DWORD 4,5,6

; 创建一些指针变量。

ptr1 PBYTE arrayB

ptr2 WORD arrayW

ptr3 DWORD arrayD
```

```assembly
.code

main PROC

    使用指针访问数据。

    mov esi,ptr1

    mov al, [esi]          ; 10h

    mov esi,ptr2

    mov ax, [esi]          ; 1

    mov esi,ptr3

    mov eax, [esi]         ; 4

    exit

main ENDP

END main
```

### 4.4.5 节回顾

1. (对/错)：任何16位通用寄存器都可以作为间接操作数。
2. (对/错)：任何32位通用寄存器都可以作为间接操作数。
3. (对/错)：`BX`寄存器通常保留用于栈。
4. (对/错)：当数组超出范围时，实模式下会发生通用保护。
5. (对/错)：以下指令无效：`[esi]`
6. (对/错)：以下是索引操作数：`array [esi]`

本节剩余问题使用以下数据定义：

```
myBytes BYTE 10h,20h,30h,40h

myWords 8AH,3Bh,72h,44h,66h

myDoubles DWORD 1,2,3,4,5

Pointer DWORD myDoubles
```

7. 在以下指令序列右侧填写要求的寄存器值：

```
mov esi, OFFSET myBytes

mov al, [esi]               ; a. AL =
mov ax, [esi+3]             ; b. AL =
mov esi, OFFSET myWords + 2

mov ax, [esi]               ; c. AX =
mov edi, 8

mov edx, [myDoubles + edi] ; d. EDX =
mov edx, [myDoubles]      ; e. EDX =
mov ebx, myPointer

mov eax, [ebx + 4]         ; f. EAX =
```

8. 挑战：在以下指令序列右侧填写要求的寄存器值：

```
mov esi, OFFSET myBytes

mov ax, WORD PTR [esi]     ; a. AX =
```

## 4.5 JMP 和 LOOP 指令

`CPU`自动加载顺序执行程序。当每条指令被解码和执行时，`CPU`已经将指令指针指向到下一条指令；它还将指令加载到其队列中。但现实中的程序并没有那么简单。`IF`语句、跳转和循环呢？它们显然需要程序转移到不同的位置。

控制转移（或分支）改变语句执行顺序的方法。所有编程语言都包含实现此目的的语句。我们将语句分为两类：

- **无条件转移**：程序在所有情况下都跳转到新位置：新值被加载到指令指针中，导致执行在新地址继续。`JMP`指令是一个很好的例子。
- **条件转移**：如果某个条件为真，程序则分支。`Intel`提供了广泛的条件转移指令，这些可以组合成逻辑结构。`CPU`根据`ECX`和标志寄存器的内容解释真/假条件。`LOOP`是一个很好的例子。

### 4.5.1 JMP 指令

`JMP`指令导致无条件地转移到代码段内部的内存位置。该位置必须通过代码标签来标识，汇编器将其转换为偏移量。语法为：

```
JMP targetLabel
```

当`CPU`执行此指令时，`targetLabel`的偏移量被移动到指令指针中，导致立即在新位置继续执行。通常你只能跳转到当前过程中的标签，除非该标签被标记为全局（详情见第5章5.5.2.3节）。

创建循环 `JMP`指令提供了创建循环循环的方法，只需跳转到循环顶部的标签：

```
top:
```

```
jmp top ; 重复无限循环
```

```
mov eax,DWORD PTR myWords      ; b. EAX =
mov esi,myPointer

mov ax,WORD PTR [si+2]      ; c. AX =
mov ax,WORD PTR [si+6]      ; d. AX =
mov ax,WORD PTR [si-4]      ; e. AX =
```

128 第 4 章 · 数据传输、寻址与算术

`JMP` 是无条件跳转的，因此除非找到其他退出循环的方法，否则循环将无限持续（虽然有方法，但我们还没有解释）。

## 4.5.2 LOOP 指令

`LOOP` 指令提供了一种简单的方法来按指定次数重复某块语句。`ECX` 会自动被用作计数器，并在每次循环重复时减 1。它的语法是：

```
LOOP destination
```

`LOOP` 指令的执行涉及两个步骤：首先，它从 `ECX` 中减去 1。接着，它将 `ECX` 与零进行比较。如果 `ECX` 不等于零，则跳转到由 `destination` 标识的标签。否则，如果 `ECX` 等于零，则不跳转，控制权传递到循环后的指令。

在实地址模式（Real-address mode）下，`CX` 被用作默认循环寄存器而不是 `ECX`。在任何模式下，`LOOP` 指令使用 `ECX` 作为循环计数器，而 `LOOPW` 指令使用 `CX` 作为循环计数器。

在下面的示例中，我们每次循环重复时向 `AX` 加 1。当循环结束时，`AX = 5` 且 `ECX = 0`：

```
mov ax,0

mov ecx,5

inc ax

loop l1
```

常见的编程错误是在开始循环之前无意中将 `ECX` 初始化为零。如果发生这种情况，`LOOP` 指令会将 `ECX` 减至 `FFFFFFFF`，循环将重复 4,294,967,296 次！或者，如果 `ECX` 是循环计数器（在实地址模式下），它将重复 65,536 次。

循环目标必须在当前计数器的 -128 到 +127 字节范围内。机器指令的平均大小约为 3 字节，因此一个循环平均最多包含 42 条指令。以下是 `MASM` 生成的错误信息示例，原因是 `LOOP` 指令的目标标签太远了。

```
error A2075: jump destination too far : by 14 bytes(s)
```

如果在循环内部修改了 `ECX`，`LOOP` 指令可能无法正常工作。在下面的示例中，`ECX` 在循环内部被递增。它永远不会到达零，循环就会停止：

```
top:
```

5. 在循环体内，使用间接寻址将单个数组元素加到持有和的寄存器中。
6. 将索引寄存器指向下一个数组元素。
7. 使用 `LOOP` 指令从起始标签重复循环。

（步骤 1–3 可以按任何顺序执行。）

## SumArray 程序示例

下面的 `sumArray` 程序计算一个字数组数组的和：

| 标题 | 累加数组 (SumArray.asm) |
| :--- | :--- |
| INCLUDE | Irvine32.inc |
| .data | |
| intarray | WORD 100h,200h,300h,400h |

```code
main PROC

    mov edi, OFFSET intarray      ; intarray 的地址

    mov ecx, LENGTHHOF intarray  ; 循环计数器

    mov ax,0                     ; 累加器清零

L1:

    add ax,[edi]                 ; 加一个整数

    add edi,TYPE intarray        ; 指向下一个整数

    loop L1                      ; 重复直到 ECX = 0

    exit

main END

END main
```

## 4.5.4 拷贝字符串

涉及数组和字符串的一种非常常见的操作是拷贝大块数据。编译器编写者总是尝试产生尽可能快执行操作的代码。让我们看看如何在汇编语言中实现这一点，创建一个拷贝字符串的循环。变址寻址（Indexed addressing）非常适合这类操作，因为同一个索引可以同时引用两个字符串。唯一的要求是目标字符串有足够的可用空间来接收拷贝的字符，包括结尾的空字节：

## 拷贝字符串 (CopyStr.asm)

| | |
| :--- | :--- |
| INCLUDE | Irvine32.inc |
| .data | |
| source | BYTE "This is the source string",0 |
| target | BYTE SIZE source DUP(0) |

```code
main PROC

    mov esi,0                     ; 索引寄存器
```

## 4.5 JMP 和 LOOP 指令

```
mov ecx,SIZEOF source    ; 循环计数器
L1:

mov al,source[esi]      ; 从 source 获取一个字符
mov target[esi],al       ; 存储到 target 中
inc esi                   ; 移动到下一个字符
loop L1                   ; 重复整个字符串
exit

main ENDP

END
```

当然，`MOV` 指令不能有两个内存操作数，因此每个字符先从源移动到 `AL`，然后从 `AL` 移动到目标字符串。

用 `C++` 或 `Java` 编程时，初学者往往没有意识到后台拷贝操作发生有多频繁。例如，在 `Java` 中，如果在添加新元素时超过了 `ArrayList` 的容量，运行时将分配一个存储块并将现有数据拷贝到新位置。当后台拷贝操作发生得频繁时，会对性能产生重大影响。

## 4.5.5 复习

1. 错误/对：`JMP` 指令可以跳转到任何操作数。
2. 错误/对：`JMP` 指令是条件指令。
3. 如果在循环之前初始化 `ECX` 为零，`LOOP` 重复多少次？（假设间接操作）。
4. 错误/对：`LOOP` 指令首先检查 `ECX` 是否大于零，然后跳转到标签。
5. 错误/对：`LOOP` 指令执行以下操作：如果 `ECX` 大于零则跳转。
6. 在实地址模式下，哪个寄存器被 `LOOP` 指令作为计数器？
7. 在实地址模式下，哪个寄存器被 `LOOP` 指令作为计数器？
8. 错误/对：`LOOP` 指令的目标在当前位置 256 字节以内。
9. 挑战：在此示例中 `EAX` 的最终值是多少？

```
mov eax,0               ; 外部循环计数器
mov ecx,10

L1:

mov eax,3               ; 内部循环计数器
mov ecx,5

L2:

add eax, 5
```

10. 修改之前的代码，使得内部循环开始时外部循环计数器不会被擦除。

## 4.6 章总结

`MOV` 是数据传输指令，将源操作数拷贝到目标操作数。`MOVZX` 指令将较小的操作数符号扩展。`MOVSX` 指令将较小的操作数符号扩展。

`XCH` 交换两个操作数的内容。至少一个操作数必须是寄存器。

本章介绍了以下操作数类型：

- 直接操作数是变量名，代表变量的地址。
- 直接偏移操作数将位移与变量名相加，产生一个新的偏移。该偏移用于访问内存。
- 间接操作数是包含地址的寄存器。通过在寄存器周围加上括号（如 `[esi]`），程序可以地址并检索内存数据。
- 索引操作数将常量与间接操作数结合。常量和寄存器值相加，并引用生成的地址。例如，`[array + esi]` 和 `array[esi]` 都是索引操作数。

以下算术指令需要记住：

- `INC` 指令对操作数加 1。
- `DEC` 指令对操作数减 1。
- `ADD` 指令将源操作数加到目标操作数。
- `SUB` 指令从目标操作数中减去源操作数。
- `NEG` 指令反转操作数的符号。

## 4.7 编程练习

- 当有符号算术操作的结果对于目标操作数太大时，溢出位（Overflow flag）会被设置。在一个字节中，`CPU` 通过将第 6 位进位与第 7 位进位进行异或运算来检测溢出。

读完本章后，你应该知道如何使用以下操作符：

- `OFFSET` 运算符返回变量距离其所在段起始位置的距离。
- `PTR` 运算符允许你覆盖变量的默认大小。
- `TYPE` 运算符返回单个变量或数组中单个元素的大小（以字节为单位）。
- `LENGTH` 运算符返回数组中的元素个数。
- `SIZEOF` 运算符返回数组初始化器所占用的字节数。
- `TYDEF` 运算符创建一个用户定义类型。

`JMP` 和 `LOOP` 指令在创建计数循环时非常有用。在 32 位模式下，`LOOP` 指令使用 `ECX` 作为循环计数器。在 16 位模式下，使用 `CX` 而不是 `ECX`。在 16 位和 32 位模式下，`LOOPD`（双字循环）指令都使用 `ECX` 作为计数器。

## 4.7 编程练习

以下练习可以在保护模式或实地址模式下完成：

### 1. 进位位（Carry Flag）

编写一个程序，使用加减法来设置和清除进位位。在每条指令之后，插入 `call DumpRegs` 语句以显示寄存器和标志位。使用注释解释每条指令如何（以及为什么）影响了进位位。

### 2. INC 和 DEC

编写一个短程序证明 `INC` 和 `DEC` 指令不影响进位位。

### 3. 零标志和符号标志（Zero and Sign Flags）

编写一个程序，使用加减法来设置和清除零标志和符号标志。在每次加或减法指令之后，插入 `call DumpRegs` 语句以显示寄存器和标志位。使用注释解释每条指令如何（以及为什么）影响了零标志和符号标志。

### 4. 溢出位（Overflow Flag）

编写一个程序，使用加减法来设置和清除溢出位。在每次加减法指令之后，插入 `call DumpRegs` 语句以显示寄存器和标志位。使用注释解释每条指令如何（以及为什么）影响了溢出位。可选：包含一条同时设置进位位和溢出位的 `ADD` 指令。

### 5. 直接偏移寻址（Direct-Offset Addressing）

在你的程序中插入以下变量：

```
.data

Uarray WORD 1000h, 2000h, 3000h, 4000h

Array SWORD -1, -2, -3, -4
```

编写指令，使用直接偏移寻址将 `Uarray` 中的四个值移动到 `EAX`、`EBX`、`ECX` 和 `EDX` 寄存器。当你紧跟一个 `call Dumpregs` 语句时，应该显示以下寄存器值：

```
EAX=00001000 EBX=00002000 ECX=00003000 EDX=00004000
```

接下来，编写指令使用直接偏移寻址将 `Sarray` 中的四个值移动到 `EAX`、`EBX`、`ECX` 和 `EDX` 寄存器。当你紧跟一个 `call Dumpregs` 语句时，应该显示以下寄存器值：

```
EAX=FFFFFFFF EBX=FFFFFE ECX=FFFFFFFD EDX=FFFFFC
```

### 6. 斐波那契数字

编写一个程序，使用循环计算斐波那契数列 `{1,1,2,3,5,8,13 }` 的前七个值。将每个值放在 `EAX` 寄存器中，并在循环内部通过 `call Dumpregs` 语句显示它。

### 7. 算术表达式

编写一个程序实现以下算术表达式：

```
EAX = -val2 + 7 - val3 + val1
```

使用以下数据定义：

```
val1 SDWORD 8

val2 SDWORD -15

val3 SDWORD 20
```

在每条指令后的注释中，写出 `EAX` 的十六进制值。在程序末尾插入 `call Dumpregs` 语句。

### 8. 反向复制字符串

编写一个使用间接寻址 `LOOP` 指令的程序，将字符串从源复制到目标，在此过程中反转字符顺序。使用以下变量：

```
source BYTE "This is the source string",0

target BYTE SIZEOF source DUP(0)
```

在循环之后立即插入以下语句。它们将显示目标字符串的十六进制内容：

```
mov esi,OFFSET target    ; 变量的偏移
mov ebx,1                ; 字节格式
```

```
mov ecx,SIZEOF target-1    ; 计数器
call DumpMem
```
