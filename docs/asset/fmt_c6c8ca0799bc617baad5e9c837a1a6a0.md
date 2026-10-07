
### FillArray 过程

```
FillArray PROC USES eax edi ecx,

pArray:PTR DWORD,      ; 指向数组的指针

Count:DWORD,           ; 元素数量

LowerRange:SDWORD,     ; 下范围

UpperRange:SDWORD                       ; 上范围

; 用 LowerRange 到 (UpperRange - 1) 之间的随机 32 位
; 整数序列填充数组。
; 返回：无

--------------------------------------

mov edi,pArray                          ; EDI 指向数组
mov exc,Count                          ; 循环计数器
mov edx,UpperRange                    ; EDX = 绝对范围 (0..n)
sub edx,LowerRange

L1:
mov eax,edx                        ; 获取绝对范围
add eax,LowerRange                    ; 结果偏移
stod                               ; 存入 [EDI]
Loop1
ret
FillArray ENDP
```

## 9.5.3 复习

1. 如果对 32 位有符号整数数组进行冒泡排序，并执行二分查找，外循环执行多少次？
2. `冒泡排序`中的内循环执行多少次？
3. 在冒泡排序过程中，内循环执行多少次？
4. 如果发现对 500 个整数排序需要 0.5 秒，那么对于？
5. 对于包含 128 个元素的数组，二分查找需要多少次比较？
6. 给定 n 个元素的数组，二分查找需要多少次比较？
7. 挑战：在二分查找过程（9.5.2 节）中，标签 `L2` 如何被消除？
8. 挑战：在二分查找过程中，语句 `L4` 如何被消除？

## 9.6 章节总结

字符串原始指令是不常的，它们需要寄存器，并对高速内存访问进行了优化。它们：

- `MOVS`：移动字符串数据
- `CMPS`：比较字符串
- `SCAS`：扫描字符串
- `STOS`：存储字符串数据
- `LODS`：从字符串加载

这些指令实际上都带有 `B`、`W` 或 `D` 后缀，分别处理字节、字和双字。

`REP` 重复字符串指令，带有索引寄存器的自动递增或减少。例如，`REPNE` 用于 `SCAS`，扫描字节直到匹配 `AL` 寄存器的内容。方向标志决定索引寄存器递增还是减少。

字符串和数组实际上是相同的。传统的字符串是单字节 ASCII 数组，但现在字符串可以是 16 位 Unicode 字符。字符串与数组之间的唯一区别是字符串通常以空字节终止。

基址索引操作使得处理二维数组（表格）变得更容易。你可以将基寄存设置为行的地址，并将索引寄存器指向所选行中的列偏移。通用 32 位寄存器可以用作基址和索引寄存器。基址索引偏移操作与基址索引相似，只是它们包含了数组的名称：

```
ebx + esi             ;基址索引
array[ebx + esi]      ;基址索引偏移
```

## 9.7 编程练习

以下练习可以在保护模式（`Protected mode`）或实地址模式（`Real-address mode`）下进行。以下每个过程均假设使用空终止字符串。请确保编写一个简短的驱动程序来测试每个过程。

### 1. 改进的 Str_copy 过程

本章所示 `Str_copy` 过程没有限制复制的字符数。创建一个新版本（命名为 `Str_copyN`），它需要一个额外的输入参数，指示要复制的最大字符数。

### 2. Str_concat 过程

编写一个名为 `Str_concat` 的过程，将源字符串连接到目标字符串的尾。在调用此过程之前，目标字符串必须有足够的空间。传递源字符串和目标字符串的指针。以下是一个示例调用：

```
.data
targetStr BYTE "ABCDE",10 DUP(0)
sourceStr BYTE "FGH",0
.code
INVOKE Str_concat, ADDR targetStr, ADDR sourceStr
```

### 3. Str_remove 过程

编写一个名为 `Str_remove` 的过程，从字符串中删除 n 个字符。传递字符串中待删除字符位置的指针。传递一个指定要删除字符数的整数。例如，以下代码显示了如何从目标中删除 "xxxx"

```
.data
target BYTE "abcxxxdefghijklmnop",0
.code
INVOKE Str_remove, ADDR [target+3], 4
```

### 4. Str_find 过程

编写一个名为 `Str_find` 的过程，在目标字符串中搜索源的第一个匹配项并返回匹配位置。输入参数应该是源字符串的指针和目标字符串的指针。如果找到匹配项，该过程将设置零标志（Zero flag），`EAX` 指向目标字符串中的匹配位置。否则，清除零标志。例如，以下代码搜索 "ABC" 并返回，此时 `EAX` 指向目标字符串中的 "A"：

```
.data
target BYTE "123ABC342432",0
source BYTE "ABC",0
pos WORD ?
```

```
.code
INVOKE Str_find, ADDR source, ADDR target
jnz notFound
mov pos, eax ; 存储位置值
```

### 5. Str_nextword

编写一个名为 `Str_nextword` 的过程，扫描字符串中某个分隔符的首次出现，并将分隔符替换为空字节。有两个输入参数：字符串指针和分隔符字符。调用后，如果找到分隔符，则设置零标志，`EAX` 包含分隔符之后下一个字符的偏移量。否则，清除零标志。例如，我们可以这样传递 `target` 的地址和一个逗号：

```
.data
target BYTE "Johnson,Calvin", 0
.code
INVOKE Str_nextword, ADDR target, ','
jnz notFound
```

调用 `Str_nextword` 后，`EAX` 将指向逗号被发现（并被替换）的位置之后的字符：

### 6. 构建构造频率表

编写一个名为 `Get_frequencies` 的过程来构建字符频率表。该过程的输入应该是指向字符串的指针，以及一个指向包含 256 个双字（doublewords）数组的指针。数组的每个位置由其对应的 ASCII 码索引。当过程返回时，数组中的每个项目都包含该字符在字符串中出现的次数。

```
.data
target BYTE "AAEBDCFBBC", 0
freqTable DWORD 256 DUP (0)
.code
INVOKE Get_frequencies, ADDR target, ADDR freqTable
```

以下是字符串以及频率表中项目 41（十六进制）到 48 的图片。位置 41 包含值 2，因为字母 A（ASCII 码 41h）在字符串中出现了两次。其他字符也显示了类似的计数：

目标字符串：

| A | E | B | D | C | F | B | C | 0 |
|---|---|---|---|---|---|---|---|--|
| ASCII 码: 41 | 41 | 45 | 44 | 43 | 46 | 42 | 42 | 0 |

频率表：

| 2 | 3 | 2 | 1 | 1 | 1 | 0 | 0 | 0 | 0 |
|---|---|---|---|---|---|---|---|---|---|
| 索引: 42 | 43 | 44 | 45 | 46 | 47 | 48 | 49 | 4B | 等. |

频率表在数据压缩和其他涉及字符处理的应用程序中非常有用。例如，霍夫编码算法将出现频率最高的字符比出现频率较低的字符存储更少的位数。

### 7. 埃拉托尼筛法

埃拉托尼筛法由一位同名的希腊数学家发明，提供了一种在给定范围内找到所有质数的方法。该算法涉及创建一个数组，其中通过以下方式标记位置：从 2 开始，在每个 2 的倍数位置插入 1。

## 第 9 章 字符串与数组

## 10. 结构

结构是给一组逻辑相关变量的模板或模式。结构中的每个变量被称为字段。程序语句可以整体访问结构，也可以访问单个字段。

结构已经存在很长时间了，与编程语言本身一样。当程序需要在一个过程之间传递大量数据时，结构至关重要。例如，假设一个过程输入是关于驱动器的二十个不同单元。按顺序传递所有参数是不现实的。相反，可以将所有相关数据放在一个结构中，并将结构的地址传递给过程。这将使用极少的栈空间（一个地址），并为调用过程提供向结构插入新数据的机会。

> 联合（union）也分组多个标识符，但这些标识符重叠相同的内存区域。联合将在第 10.1.7 节介绍。

一点消息：汇编语言中的结构本质上是 C 和 C++ 中的结构。通过少量翻译工作，你可以获取 Windows API 库中的任何结构并应用于汇编语言。良好的调试器如 Microsoft Visual Studio 会运行时显示结构字段的名称和内容。

`COORD` 结构从一个简单的示例开始：Windows 使用的 `COORD` 结构识别 X 和 Y 坐标。字段 `X` 相对于结构起始位置偏移为 0：

```
COORD STRUCT
X WORD ? ; 偏移 00
Y WORD ? ; 偏移 02
COORD ENDS
```

使用结构涉及三个连续步骤：

1. 定义结构。
2. 声明一个或多个结构类型的变量。
3. 编写访问结构的运行时指令。

### 10.1.1 定义结构

使用 `STRUCT` 和 `ENDS` 指令定义结构。在结构内部，使用与普通变量相同的语法定义字段。基本语法为：

```
name
字段声明
name ENDS
```

#### 字段初始化器

当你为结构（structure）中的字段提供初始化器时，它们将成为结构变量声明时的默认值。你可以使用多种类型的初始化器：

- 未定义（Und）：使用 `?` 让字段内容保持未定义。
- 字符串（Strings）：使用引号括的字符来初始化字符串字段。
- 整数（Integers）：使用整数常量或整数表达式来初始化整数字段。
- 数组（Arrays）：当字段为数组时，使用 `DUP` 运算符初始化数组元素。

例如，让我们定义一个名为 `Employee` 的结构来描述员工信息，包含 ID 编号、姓氏、工龄以及薪资历史数组等字段。以下结构定义将在声明任何 `Employee` 类型的变量之前插入程序中：

```
Employee STRUCT
IdNum BYTE "000000000"
LastName BYTE 30 DUP(0)
Years WORD 0
SalaryHistory DWORD 0,0,0,0
Employee ENDS
```

下图显示了该结构的线性表示：

![](img/ea8a6a99b0e33c5c1bf5dd603b329094_361_0.png)

## 10.1.2 声明结构变量

你可以声明结构的实例（称为结构变量）并用特定值对其初始化。如果使用空括号 `<>`，汇编器将保留结构的默认字段初始化器。或者，你也可以在选定的字段中插入新变量。这里展示了这两种方法的示例，使用了 `COORD` 和 `Employee` 结构：

```
.data
point1 COORD <5,10>
point2 COORD <>
worker Employee <>
```

可以覆盖部分或全部默认字段。以下示例覆盖了 `Employee` 的 `IdNum` 字段：

```
person1 Employee = "555223333"
```

另一种表示法使用大括号 `{ ... }` 代替角括号 `< >`：

```
person2 Employee = "555223333"
```

当字符串字段的初始化器比字段短时，剩余位置将用空格填充。需要注意的是，字符串字段末尾会自动插入一个空字节。如果你计划调用 `WriteString` 等库函数，则必须手动插入空字节。

你可以通过插入逗号作为占位符来跳过结构字段。例如，以下语句跳过了 `IdNum` 字段并初始化了 `LastName` 字段：

```
person3 Employee, "Jones",
```

如果字段包含数组，使用 `DUP` 运算符初始化部分或全部数组元素。如果初始化器比字段短，剩余位置将用零填充。在这里，我们初始化了前两个 `SalaryHistory` 值，并将其余部分设置为零：

```
person4 Employee <<,,2 DUP(20000)>
```

#### 结构数组

你可以像下一个示例那样声明一个结构数组。`AllPoints` 的每个元素都被初始化为 `<0,0>`：

- `NumPoints = 3`
- `AllPoints COORD NumPoints DUP<0,0>`

## 10.1.3 引用结构变量

可以使用 `TYPE` 和 `SIZEOF` 运算符对结构变量和名称均进行引用。例如，让我们回到之前看到的同一个 `Employee` 结构：

```
Employee STRUCT bytes
IdNum BYTE "000000000" ; 9
LastName BYTE 30 DUP(0) ; 30
Years WORD 0 ; 2
SalaryHistory DWORD 0,0,0,0 ; 16
Employee ENDS ; 总共57
```

给定以下定义：

```
.data
worker Employee <>
```

以下每个表达式都返回相同的值：

```
TYPE Employee ; 57
SIZEOF Employee ; 57
SIZEOF worker ; 57
```

请记住，`TYPE` 运算符返回标识符存储类型（BYTE、WORD、DWORD 等）所使用的字节数。`LENGTHOF` 运算符返回数组中元素的计数。`SIZEOF` 运算符将 `LENGTHOF` 与 `TYPE` 相乘。这些在第 4.3 节中介绍过。

## 10.1 结构

### 字段引用

对单个字段的直接引用需要结构变量作为限定符。使用 `Employee` 结构，可以在汇编时生成以下常量表达式：

```
TYPE Employee.SalaryHistory      ; 4
LENGTHOF Employee.SalaryHistory  ; 4
TYPE Employee.Years              ; 2
```

以下是对结构变量 `worker` 的运行时引用：

```
.data
worker Employee <
.code
mov dx,worker.Years
mov worker.SalaryHistory,20000      ; 第一份薪资
mov [worker.SalaryHistory+4],30000  ; 第二份薪资
mov edx, OFFSET worker.LastName
```

间接操作数（Indirect Operands）允许使用寄存器（如 `ESI`）访问结构数据。这种寻提供了灵活性，特别是将结构地址传递给过程或使用结构数组时。引用间接操作数时需要 `PTR` 运算符：

```
mov esi, OFFSET worker
mov ax,(Employee PTR [esi]).Years
```

如果我们编写以下语句，它将无法汇编，因为 `Years` 本身无法识别特定的结构：

```
mov ax, [esi].Years              ; 无效
```

### 遍历数组

循环通常配合间接或索引寻址来处理结构数组。以下程序（AllPoints）为以下分配坐标：

```
# TITLE Loop Through Array (AllPoints.asm)
INCLUDE Irvine32.inc
.data
NumPoints = 3
AllPoints COORD NumPoints DUP<0,0>
.code
main PROC
mov esi, OFFSET AllPoints
mov ecx, NumPoints
loop1:
mov ax,(Employee PTR [esi]).Years
; ... process data ...
add esi, SIZEOF Employee
loop loop1
ret
main ENDP
END main
```

# 第 10 章 • 结构与宏

```
call WaitMsg ; "Press Enter..."
exit
main ENDP
END main
```

该程序使用了来自 `SmallWin.inc` 的定义（由 `Irvine32.inc` 自动包含）：

```
STD_OUTPUT_HANDLE EQU -11
SYSTEMTIME STRUCT . .
COORD STRUCT . .
GetStdHandle PROTO,
StdHandle:DWORD
GetLocalTime PROTO,
lSystemTime:PTR SYSTEMTIME
SetCursorPosition PROTO,
StdHandle:DWORD,
coords:COORD
```

以下是下午 12:16 拍摄的屏幕输出截图：

![](img/ea8a6a99b0e33c5c1bf5dd603b329094_366_0.png)

## 10.1.5 嵌套结构

你可以创建嵌套结构定义，其中结构包含其他结构。例如，可以根据左上角和右下角定义一个矩形（Rectangle），这两个角都是 `COORD` 对象：

```
Rectangle STRUCT
UpperLeft COORD <>
LowerRight COORD <>
Rectangle ENDS
```
