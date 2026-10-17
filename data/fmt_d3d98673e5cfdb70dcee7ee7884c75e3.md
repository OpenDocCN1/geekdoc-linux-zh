
> 在实模式（Real-address mode）下运行的程序使用 `CX` 作为 `LOOPZ` 指令的默认循环计数器。如果你想强制 `ECX` 作为循环计数器，请使用 `LOOPZD` 指令。

### 6.4.2 LOOPNZ 和 LOOPNE 指令

`LOOPNZ`（非零则循环）是 `LOOPZ` 的对应指令。当 `ECX` 的无符号值大于 0 且零标志清位时，循环继续。其语法为：

```
LOOPNZ destination
```

`LOOPNE`（不等则循环）等同于 `LOOPNZ`，因为它们共享相同的电路。这是 `LOOPNZ` 和 `LOOPNE` 的执行逻辑：

```
ECX = ECX - 1
if ECX > 0 and ZF = 0, jump to destination
```

否则，不发生跳转，控制传递到下一条指令。

示例 以下代码片段（来自 `Loopnz.asm`）扫描数组直到找到正数：

```
.data
  array 10001000b
  sentinel WORD 0
.code
  mov esi, OFFSET array
  mov ecx, 10
next:
  test word [esi], sentinel ; bit
  jnz quit                  ; none
  loop next                 ; continue loop
quit:
```

## 6.4.3 节复习

- 1. （是/否）：`LOOP` 指令在零标志清位时跳转到标签。
- 2. （是/否）：`LOOPNZ` 指令在 `ECX` 大于 0 时跳转到标签。
- 3. （是/否）：`LOOPZ` 的目标标签不能超过 -128 或 +127 字节。
- 4. 修改 6.4.2 中的 `LOOPNZ` 示例。
- 5. 挑战：`LOOPNZ` 示例依赖于哨兵值。如果移除它会发生什么？

## 6.5 条件结构

在本节中，我们将检查高级语言中常用的几种条件结构。你将看到每个结构如何转换为汇编。让我们把条件结构视为触发分支选择的一个或多个条件表达式。

> 计算机科学中的一个重要领域是编译器构造。大多数训练过的计算机科学家都能设计简单的编程语言并编写翻译它的程序。在本节中学习的方法对你以后学习编译技术会有帮助。

### 6.5.1 块结构 IF 语句

在大多数高级语言中，`IF` 语句意味着一个布尔表达式后面跟着两个语句列表：在表达式为真时执行一个，在表达式为假时执行另一个：

```
if( expression )
    statement list 1
else
    statement list 2
```

语句的 `else` 部分是可选的。图 6-1 显示了条件 `IF` 的两个分支路径，标记为 `true` 和 `false`。

示例1 使用 Java/C++ 语法，如果 `op1` 等于 `op2`，则执行两个赋值语句：

```
if ( op1 == op2 ) {
  X = 1;
  Y = 2;
}
```

高级语言编译器可能会将上述 `IF` 语句翻译为 `CMP` 指令以及一个多个条件跳转。假设 `op1` 和 `op2` 是内存操作数，在执行 `CMP` 之前必须将其中一个移动到寄存器中。以下代码实现了 `IF` 语句：

```
mov eax, op1
cmp eax, op2      ; 比较 eax 和 op2
je L1             ; 如果相等则跳转到 L1
jmp L2             ; 否则跳转到 L2
L1:
mov X, 1
mov Y, 2
L2:
```

必须意识到，相同的高级语言代码可以用多种方式翻译成汇编语言。在本章展示编译后的代码示例时，它们仅代表了假设的编译器可能产生的内容。

**示例 2** 在 MS-Windows 使用的 `FAT32` 文件系统中，磁盘簇的大小取决于磁盘的总体容量。在下面的伪代码中，如果磁盘大小（在名为 `gigabytes` 的变量中）小于 8 GB，则我们将簇大小设置为 4,096；否则，我们将簇大小设置为 8,192：

```
clusterSize = 8192;
if( gigabytes < 8 )
  clusterSize = 4096;
```

以下是一种用汇编语言实现这种结构的方法：

```
mov clusterSize, 8192      ; 假设较大的簇
cmp gigabytes, 8             ; 大于 8 GB ？
jae next
mov clusterSize, 4096      ; 切换到较小的簇
next:
```

（磁盘簇在第 14.2 节中描述。）

## 6.5.2 复合表达式

### 6.5.2.1 逻辑 AND 运算符

你可以用两种方式实现使用本地 `AND` 运算符的布尔表达式。考虑以下用伪代码编写的复合表达式：

```
if (al > b1) AND (b1 > cl)
{
  X = 1
}
```

我们假设这些值是无符号。以下是使用 `JA`（如果高于则跳转）的直接实现：

```
L1:
  cmp b1,cl               ; 第二个表达式...
  ja L2
  jmp next
L2:
  mov X,1                 ; 两个都真
                          ; 将 X 设置为 1
next:
```

但对于这样一个简单的问题，这些汇编代码似乎完全太多了。如果我们反转 `JA` 条件并改用 `JBE`，就可以简化代码。这相当于短路（或提前退出）求值，即如果第一个表达式为假，则不评估第二个表达式：

```
cmp al,bl      ; 第一个表达式...
jbe next        ; 如果为假则退出
cmp bl,cl      ; 第二个表达式
jbe next        ; 如果为假则退出
mov X,1        ; 两个都真
```

`next:` 

如果第一个 `JBE` 没有跳转，通过 CPU 直穿到第二个 `CMP` 指令，代码大小减少了 29%（七条指令减少到五条）。通常，高级语言编译器默认使用短路求值。

### 6.5.2.2 逻辑 OR 运算符

当复合表达式中出现多个表达式时，代码使用逻辑 `OR` 运算符进行分支；只要任何表达式为真，该表达式自动为真。让我们使用下面的伪代码作为示例：

```
if (al > bl) OR (bl > cl)
 X = 1
```

在下面的实现中，如果第一个表达式为真，代码跳转到 `L1`；否则，执行到第二个 `CMP` 指令。第二个表达式反转了 `>` 运算符并改用 `JBE`：

```
cmp al,bl      ; 1: 比较 AL 和 BL
ja L1           ; 如果为真，跳过第二个表达式
cmp bl,cl      ; 2: 比较 BL 和 CL
jbe next        ; 假：跳过下一条语句
L1: mov X,1     ; 真：跳过 X = 1
```

`next:` 

对于任何给定的复合表达式，在汇编语言中至少有几种实现方式。

## 6.5.3 WHILE 循环

`WHILE` 结构在执行语句块之前测试条件。只要循环条件保持为真，语句就会重复。下面的循环是用 C++ 编写的：

```
while(val1 < val2)
{
    val1++;
    val2--;
}
```

206 第 6 章 • 条件处理

在汇编语言中编写这种结构时，反转循环条件并在条件变为真时跳转到 `endif` 非常方便。假设 `val1` 和 `val2` 是变量，我们必须在开始将其中一个移动到寄存器并在并在恢复变量：

```
mov     eax,val1      ; 将变量复制到 EAX
_while:cmp     eax,val2      ; 如果不是 (val1 < val2)
jnl     endwhile      ; 退出循环
inc     eax              ; val++
dec     val2              ; val2--
jmp     _while          ; 重复循环
endwhile:
mov     val1,eax      ; 为 val1 保存新值
```

`EAX` 是循环内部 `val1` 的代理（替代）。对 `val1` 的任何引用必须通过 `EAX` 进行。此外，注意使用了 `JNL`，这意味着 `val1` 和 `val2` 是符号整数。

### 6.5.3.1 示例：嵌套在循环中的 If 语句

高级结构化语言特别擅长表示嵌套控制结构。在下面的 C++ 示例中，`if` 语句嵌套在 `WHILE` 循环内部：

```
while( op1 < op2 ) {
op1++;
if( op2 == op3 ) X = 2;\else X = 3;
}
```

在我们用汇编语言编写此循环之前，让我们使用图 6-2 中的流程图来描述逻辑。为了简化到汇编语言的翻译，用寄存器替代了变量（`EAX = op1`, `EBX = op2`, `ECX = op3`），并添加了标签。从流程图生成汇编代码的最简单方法是注意流程图与形状之间的相关性。

## 6.5.4 表驱动选择

表驱动选择是使用表来代替多路比较的方法。要使用它，必须创建一个包含过程偏移的表。例如，下面的程序 (`ProcTble.asm`) 用户输入一个字符。通过循环，将字符与表中的每个项进行比较。表中的第一个匹配项会导致调用不同的字符串，该字符串在循环期间显示：

```
TITLE Table of... (ProcTble.asm)
; 此程序包含一个偏移表。
; 它使用表进行间接执行。
```

`INCLUDE Irvine32.inc`

```
.data
CaseTable BYTE   'A'      ; 查找值
DWORD           Process_A
BYTE            'B'
DWORD           Process_B
BYTE            'C'
DWORD           Process_C
BYTE            'D'
DWORD Process_D
NumberOfEntries = ($ - CaseTable)
prompt BYTE "Press capital A,B,C,or D: ",0"
```

为每个过程定义一个单独的消息字符串：

```
msgA BYTE "Process_A",0
msgB BYTE "Process_B",0
msgC BYTE "Process_C",0
msgD BYTE "Process_D",0
```

```
.code
main PROC
mov edx,OFFSET prompt      ; 请求用户输入
call WriteString               ; 将字符读入 AL
call ReadChar                  
mov ebx,OFFSET CaseTable     ; EBX 指向表
mov ecx,NumberOfEntries  ; 循环计数
```

`L1:`

`cmp al,[ebx]                  ; 找到匹配？`

`jne L2                               ; 否：继续`

`call NEAR PTR [ebx + 1]      ; 是：调用过程`

这样的间接调用需要 `NEAR PTR` 运算符。

```
call WriteString               ; 显示消息
call Crlf                       ; 退出搜索
jmp L3
L2:
add ebx,EntrySize            ; 指向下一个项
loop L1                        ; 重复直到 ECX = 0
```

`L3:`

`exit`

`main ENDP`

以下每个过程都将不同的字符串偏移移动到 `EDX`：

```
Process_A PROC
mov edx,OFFSET msgA
ret
Process_A ENDP
```

## 第 6 章 • 条件处理

```assembly
Process_B PROC
    mov edx,OFFSET msgB
    ret
Process_B ENDP
Process_C PROC
    mov edx,OFFSET msgC
    ret
Process_C ENDP
Process_D PROC
    mov edx,OFFSET msgD
    ret
Process_D ENDP
END main
```

表驱动选择方法涉及一些初始开销，但它可以减少你必须编写的代码量。表格可以处理大量的比较，并且比长系列比较、跳转和 `CALL` 指令更容易修改。表格甚至可以在运行时进行修改和重新配置。

## 6.5.5 节复习

说明：在所有复合表达式中，均使用短路求值。假设 `X`、`val1`、`val2` 和 `val3` 是 16 位的变量。

- 1. 用汇编语言实现以下伪代码：
```assembly
if( bx > cx )
    X = 1;
```

- 2. 用汇编语言实现以下伪代码：
```assembly
if( dx <= cx )
    X = 1;
else
    X = 2;
```

- 3. 用汇编语言实现以下伪代码：
```assembly
if( val1 > cx AND cx > dx )
    X = 1;
else
    X = 2;
```

- 4. 用汇编语言实现以下伪代码：
```assembly
if( bx > cx OR bx > val1 )
    X = 1;
else
    X = 2;
```

## 6.6 应用：有限状态机

5. 用汇编语言实现以下伪代码：
```assembly
if( bx > cx AND bx > dx) OR ( dx > ax )
    X = 1;
else
    X = 2;
```

6. 挑战：重写以下代码（来自第 6.5.3.1 节），使其功能等效，但使用的指令更少：
```assembly
mov eax,op1           ; 将变量复制到寄存器
mov ebx,op2
mov ecx,op3
L1: cmp eax,ebx      ; EAX < EBX?
jmp L2               ; 真
jmp L7               ; 假
L2: inc eax
```
