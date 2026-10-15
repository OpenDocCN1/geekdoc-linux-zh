
.DATA

*斜体字*表示定义的术语或类别。在以下示例中，`number`指整数常量：

```
ALIGN [[ number ]]
```

当双括号`[[ ]]`包围一个项时，该项是可选的。在以下示例中，`text`是可选的：

```
[[text]]
```

当列表项之间出现垂直分隔符`|`时，必须重复其中一个项。以下示例表示在`NEAR`和`FAR`之间选择：

```
NEAR | FAR
```

省略号(...)表示列表最后一项重复。在下一个示例中，逗号后的初始化值可以重复多次：

```
[[ name ]] BYTE initializer [[, initializer]] ..
```

### D.2 MASM 保留字

以下是各种 MASM 指令的操作。它们也是保留字，意味着它们不能作为标识符（标签、常量等）。

| | |
|---|---|
| `$` | PARITY |
| `?` | PASCAL |
| `@B` | QWORD |
| `@F` | REAL4 |
| ADDR | REAL8 |
| BASIC | REAL10 |
| BYTE | SBYTE |
| C | SDWORD |
| CARRY? | SIGN? |
| DWORD | STDCALL |
| FAR | SWORD |
| FAR16 | SYSCALL |
| FORTRAN | TBYTE |
| FWORD | VARARG |
| NEAR | WORD |
| NEAR16 | ZERO? |
| OVERFLOW? | |

### D.3 寄存器名称

| AH | CR0 | DR1 | EBX | SI |
|---|---|---|---|---|
| AL | CR2 | DR2 | ECX | SP |
| AX | CR3 | DR3 | EDI | SS |
| BH | CS | DR6 | EDX | ST |
| BL | CX | DR7 | ES | TR3 |
| BP | DH | DS | ESI | TR4 |
| BX | DI | DX | ESP | TR5 |
| CH | DL | EAX | FS | TR6 |
| CL | DR0 | EBP | GS | TR7 |

### D.4 Microsoft 汇器 (ML)

`ML`程序（`ML.EXE`）汇编并链接一个或多个汇编源文件。命令行选项区分大小写。语法为：
`ML [[options]] filename [[options]] filename]]/link linkoptions]]`

必需参数是至少一个文件名，即汇编语言源文件的名称。以下命令汇编源文件`AddSub.asm`生成对象文件`AddSub.obj`：

```
ML -c AddSub.asm
```

## 表 D-1 ML 选项（续）

| 选项 | 动作 |
| --- | --- |
| `/Cp` | 保留所有用户标识符的大小写。 |
| `/Cu` | 将所有标识符映射为大写。 |
| `/Cx` | 保留公共和外部符号的大小写（默认值）。 |
| `/Dsymbol=value` | 使用给定的名称定义宏。如果缺少值，则留空。由空格分隔的多个标记必须用双引号括起来。 |
| `/EP` | 生成预处理后的源文件列表（发送到 STDOUT）。详见 `/Sf`。 |
| `/Fhexnum` | 将栈大小设置为 hexnum 字节（等同于 `/STACK:number`）。该值必须以十六进制形式表示。`/F`和`hexnum`之间必须有空格。 |
| `/efil` | 指定可执行文件的名称。 |
| `/Flfilename` | 生成汇编代码列表。详见 `/Sf`。 |
| `/Fmfilename` | 创建链接器映射文件。 |
| `/Ofname` | 指定对象文件名。 |
| `/Fpi` | 为浮点运算生成修复（仅限混合语言）。 |
| `/Frfilename` | 生成 Source Browser `.SBR`文件。 |
| `/FRfilename` | 生成扩展形式的 Source Browser `.SBR`文件。 |
| `/Gc` | 指定使用 Pascal 风格的函数调用和命名规范。等同于 `OPTION LANGUAGE:PASCAL`。 |
| `/Gd` | 指定使用 C 风格的函数调用和命名规范。等同于 `OPTION LANGUAGE:C`。 |
| `/Hnumber` | 将外部名称限制为数字。默认 31 个字符。 |
| `/help` | 调用 ML 的快速帮助（QuickHelp）。 |
| `/Ipathname` | 设置包含文件的路径。最多允许使用多个 `/I`选项。 |
| `/nologo` | 抑制汇编成功的消息。 |
| `/Sa` | 开启所有可用信息的列表。 |
| `/Sc` | 在列表中添加指令计时信息。 |

## 表 D-1 ML 选项（续）

| 选项 | 动作 |
| --- | --- |
| `/Sf` | 在列表中添加第一遍列表。 |
| `/Sg` | 开启汇编生成代码的列表。 |
| `/Slwidth` | 设置源列表的每行宽度（字符）。范围为 60 到 255 或 0。默认值为 0。等同于 `/PAGE width`。 |
| `/Sn` | 在生成列表时关闭符号表。 |
| `/Splength` | 设置源列表的每页长度（行数）。范围为 10 到 255 或 0。默认值为 0。等同于 `/PAGE length`。 |
| `/Ss text` | 指定源列表的文本。等同于 `SUBTITLE text`。 |
| `/St text` | 指定源列表的标题。等同于 `TITLE text`。 |
| `/Sx` | 在列表中开启条件条件编译显示。 |
| `/Ta filename` | 汇编文件名不以 `.ASM`结尾的源文件。 |
| `/w` | 等同于 `/W0`。 |
| `/Wle` | 设置警告级别，级别为 0、1 或 3。 |
| `/WX` | 如果产生警告，则返回错误代码。 |
| `/Zd` | 在对象文件中生成行号信息。 |
| `/Zf` | 将所有符号设为公共。 |
| `/Zi` | 在对象文件中生成代码信息。 |
| `/Zm` | 启用 M51 以与 MASM 5.1 最大的兼容性。 |
| `/Gp[alignment]` | 在指定的字节边界上对齐结构。对齐可以是 1、2 或 4。 |
| `/Zs` | 仅执行语法检查。 |
| `/?` | 显示 ML 命令行语法的摘要。 |

## D.5 LINK

以下信息适用于微软汇编器提供的 16 位链接器。`LINK`工具将对象文件合并成单个可执行文件或动态链接库。其语法为：

`LINK options objfiles [[exefile]], [[mapfile]], [[libraries]], [[definition]]`

表 D-2 描述了 `LINK`命令选项，但在帮助文档中描述的几个少数使用的选项除外。

## 表 D-2 LINK 命令选项

| 选项 | 动作 |
| :--- | :--- |
| `/A:size` | 选项名：`/A=ALIGNMENT`。直接使用 LINK 将分段可执行文件中的段数据按 size 字节指定的边界进行对齐，其中 size 必须是 2 的幂。 |
| `/B` | 选项名：`/B=ATTACH`。抑制找不到库文件或对象文件的提示。 |
| `/CO` | 选项名：`/CO=VIEW`。添加微软 Code 调试器所需的符号数据和行号。此选项与 `/EXEPACK`选项不兼容。 |
| `/CP:number` | 选项名：`/CP=ARMAXALLOC`。将程序的最大内存分配设置为 16 字节段节。 |
| `/DO` | 选项名：`/DO=SSEG`。按照微软高级语言所使用的默认顺序对段排序。 |
| `/DS` | 选项名：`/DS=ALLOCATE`。指示 LINK 从数据段的高端加载所有数据。`/DS`选项用于创建 MS-DOS `.EXE`文件的汇编语言程序。 |
| `/E` | 选项名：`/E=EXEPACK`。压缩可执行文件。`/EXEPACK`选项与 `/DEFINITION`不兼容。 |
| `/F` | 选项名：`/F=INCREMENTAL`。为增量链接做准备。配合 `/C`使用。 |
| `/HE` | 选项名：`/HE=HELP`。指定 Windows 应用程序类型。 |
| `/HI` | 选项名：`/HI=HIGH`。指定链接类型。配合 `/C`使用。 |
| `/INC` | 选项名：`/INC=INCREMENTAL`。为增量链接做准备。配合 `/C`使用。 |
| `/INF` | 选项名：`/INF=IGNORE`。指定 Windows 应用程序。 |
| `/LI` | 选项名：`/LI=LIBRARY`。指定库路径。 |
| `/M` | 选项名：`/M=MEMORY`。指定内存类型。 |
| `/NOP` | 选项名：`/NOP=NOCODE`。关闭代码段。 |
| `/NOL` | 选项名：`/NOL=NOCASE`。保留标识符的大小写。 |
| `/PM` | 选项名：`/PM=PM`。指定 Windows 应用程序。 |
| `/ST:number` | 选项名：`/ST=STACK`。设置栈字节。 |
| `/T` | 选项名：`/T=TINY`。创建小型 `.COM`而不是 EXE。 |
| `/*` | 选项名：`/*`显示 LINK 命令行语法的摘要。 |

## D • MASM 参考

### 环境变量

| 变量 | 描述 |
| --- | --- |
| INIT | 指定 TOOLS.INI 路径。 |
| LIB | 指定库路径。 |
| LINK | 指定默认命令行选项。 |
| TMP | 指定 VM.TMP 文件路径。 |

## D.6 CodeView 调试器

微软 CodeView 调试器在运行汇编或编译程序的同时，显示程序源代码、变量、内存位置、处理器寄存器和其他相关信息。其语法为：

`CV [options] executablefile [arguments]`

表 D-3 列出了在 MS-DOS 下运行的 CodeView 命令行选项。

## 表 D-3 CodeView 命令行选项

| 选项 | 动作 |
| --- | --- |
| `/2` | 允许使用显示器。 |
| `/25` | 以 25 行模式启动。 |
| `/43` | 以 43 行模式启动。 |
| `/50` | 以 50 行模式启动。 |
| `/B` | 以黑白模式启动。 |
| `/commands` | 在启动时执行命令。 |
| `/F` | 通过翻页来交换屏幕。 |
| `/G` | 消除 CGA 显示器上的刷新闪烁。 |
| `/I\|01\|` | 开启（`/I1`）或关闭（`/I0`）不可中断和 8259 中断捕获。 |
| `/K` | 禁用对调试程序的安装键盘监控。 |
| `/M` | 禁用 CodeView 使用鼠标。 |
| `/N\|01\|` | `/N0`告诉 CodeView 捕获不可中断；`/N1`告诉它不捕获。 |

# 表 D-3 CodeView 命令行选项（续）

| 选项 | 动作 |
| :--- | :--- |
| `/R` | 启用 80386/486 调试寄存器。 |
| `/S` | 通过更改缓冲区来交换屏幕（主要用于图形程序）。 |
| `/TSF` | 切换 TOOLS.INI 条目以读取/不读取 CURRENT.STS 文件。 |

## D.7 MASM 指令

`name = expression`
将 `expression`的数值值赋值给 `name`。该符号在稍后可以被重新定义。

`.186`
启用针对 80186 处理器的指令的汇编；禁用对后续处理器引入的指令的汇编。同时启用 8087 指令。

`.286`
启用针对 80286 处理器的非特权指令的汇编；禁用后续处理器引入的指令的汇编。同时启用 80287 指令。

`.286P`
启用针对 80286 处理器的所有指令（包括特权指令）的汇编；禁用后续处理器引入的指令的汇编。同时启用 80287 指令。

`.287`
启用针对 8087 协处理器的指令的汇编；禁用后续处理器引入的指令的汇编。

`.386`
启用针对 80386 处理器的非特权指令的汇编；禁用后续处理器引入的指令的汇编。同时启用 80387 指令。

`.386P`
启用针对 80386 处理器的所有指令（包括特权指令）的汇编；禁用后续处理器引入的指令的汇编。同时启用 80387 指令。

`.387`
启用针对 80387 协处理器的指令的汇编。

`.486`
启用针对 80486 处理器的非特权指令的汇编。

`.486P`
启用针对 80486 处理器的所有指令（包括特权指令）的汇编。

`.586`
启用针对 Pentium 处理器的非特权指令的汇编。

`.586P`
启用针对 Pentium 处理器的所有指令（包括特权指令）的汇编。

`.686`
启用针对 Pentium Pro 处理器的非特权指令的汇编。

`.686P`
启用针对 Pentium Pro 处理器的所有指令（包括特权指令）的汇编。

`.8086`
启用 8086 指令（以及相同的 8088 指令）的汇编；禁用后续处理器引入的指令的汇编。同时启用 8087 指令。这是处理器的默认模式。

`.8087`
启用 8087 指令的汇编；禁用由后续协处理器引入的指令的汇编。这是协处理器的默认模式。

## ALIAS `<alias>` = `<actual-name>`
将旧函数映射到新名称。`Alias`是备用名称或别名，而 `actual-name`是函数或过程的实际名称。角括号是必须的。`ALIAS`指令用于创建库，允许链接器（`LINK`）将旧函数映射到新函数。

## ALIGN [[number]]
将下一个变量或指令对齐到 `number`的倍数的字节上。

## .ALPHA
按字母顺序排列段段。

`ASSUME register:name |], segregister:name |]`
`ASSUME datareister:type |], datareister:type |]`
`ASSUME register:ERROR |], register:ERROR |]`
`ASSUME (register:| NOTHING |], register:NOTHING |]`

对寄存器值进行检查。当 `ASSUME`生效时，汇器会监控给定寄存器值的变化。如果使用了寄存器，`ERROR`会生成错误。`NOTHING`移除寄存器错误检查。你可以在一个语句中组合不同类型的假设。

## .BREAK [[IF condition]]
生成代码，如果条件为真，则终止 `.WHILE`或 `.REPEAT`块。

`[[name || BYTE initializer ||], initializer]...`
为每个初始化器分配并可选地初始化字节存储。也可以在任何允许类型的地方用类型指定符。

## D.7 MASM 指令

`name CATSTR [[textitem[, textitem2]] ...]]`
拼接文本项。每个文本项可以是字面量字符串、以 `%`开头的常量，或者宏函数返回的字符串。

`.CODE[[name]]`
当与 `.MODEL`使用时，指示名为 `name`的代码段的开始（tiny、small、compact 和 flat 模型的默认段名为 `_TEXT`，其他模型的段名为 `module_TEXT`）。

`COMM definition [[definition]] ...`
根据 `definition`中指定的属性创建一个公共变量。每个定义具有以下格式：

```
[[langtype]] [[NEAR | FAR |label:type]]:count
```

标签是变量名。类型可以是任何类型指定符（`BYTE`、`WORD`等）或指定字节数的整数。`count`指定数据对象的数量（默认为 1）。

`COMMENT delimiter [[text]]`

```
[[text]]
```

```
[[text]] delimiter [[text]]
```

将同一行内或分隔符之间的所有文本视为注释。

`.CONST`
当与 `.MODEL`使用时，启动一个常量数据段（段名为 `CONST`）。该段具有只读属性。

`.CONTINUE[[IF condition]]`
如果条件为真，生成代码跳转到 `.WHILE`或 `.REPEAT`块的顶部。

`.CREF`
启用在符号表和浏览器文件的符号部分列出符号。

`.DATA`
当与 `.MODEL`使用时，启动一个用于初始化数据的近段（段名为 `_DATA`）。

`.DATA?`
当与 `.MODEL`使用时，启动一个用于未初始化数据的近段（段名为 `_BSS`）。

`.DOSSEG`
按字母顺序排列段。

`.DOSSEG`
与 `DOSSEG`相同。

`[[name]] DW []`
为每个初始化器分配并可选地初始化一个双字存储。也可以在任何允许类型的地方作为类型指定符。

## ECHO message
将消息显示到标准输出设备（默认为屏幕）。

`.ELSE`
参见 `.IF`。

## ELSE
标记条件块中的另一种分支。参见 IF。

`ELSEIF`
将 ELSE 和 IF 合并为一个语句。参见 IF。

`ELSEIF2`
当 `OPTION:SETIF2`为真时评估 `ELSEIF`。

## END [[address]]
标记模块的结束，并可选地设置程序入口为地址。

`.ENDIF`
参见 `.IF`。

`.ENDIF`
参见 `.IF`。

## ENDM
终止宏或重复块。参见 `MACRO`、`FOR`、`REPEAT`或 `WHILE`。

`name ENDP`
标记过程 `name`的结束。参见 `PROC`。

`name ENDS`
标记段、结构体或联合体的结束。

`.ENDW`
参见 `.WHILE`。

`name EQU expression`
将 `expression`的数值值赋值给 `name`。该名称在稍后可以被重新定义。

`name EQU <text>`
将指定的文本赋值给 `name`。该名称稍后可以分配不同的文本。参见 `TEXTEQU`。

```
.ERR [message|]
```

生成错误。

```
.ERR2 [message|]
```

当 `OPTION:SETIF2`为真时评估 `ERR2`。

```
.ERRB [<textitem>|], message|]
```

如果 `textitem`为空则生成错误。

```
.ERRDEF name [|], message|]
```

如果 `name`是已定义的标签、变量或符号，则生成错误。

```
.ERRDIF[I ||]<textitem1>, <textitem2> [], message|]
```

如果文本项不同则生成错误。如果提供了 `I`，则不区分大小写。
