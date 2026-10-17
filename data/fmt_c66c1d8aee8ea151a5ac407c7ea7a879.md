
`.ERRE` expression `[]`, `message|]`

```
如果表达式为假（0）则生成错误。
```

`.ERRIDN[I]<textitem1>, <textitem2> []`, `message|]`

```
如果文本项相同则生成错误。如果提供了 I，则不区分大小写。
```

`.ERNNB <textitem> []`, `message|]`

```
如果 textitem 不为空则生成错误。
```

`.ERRNDEF name [|]`, `message|]`

```
如果 name 未定义，则生成错误。
```

`.ERRNZ expression [|]`, `message|]`

```
如果表达式为真（非零）则生成错误。
```

## EVEN
将下一个变量或指令对齐到偶数字节上。

# `.EXIT [[expression|]]`
生成终止代码。将可选表达式返回给 shell（壳）。

# `EXITIM [[textitem|]]`
终止当前循环或宏块的展开，并开始在块之外组装下一个语句。在宏函数中，将返回该类型。

# `EXTERN [[langtype]] name [[type|], [[altid|]], [[langtype]] name [[altid|]] [[type|]]]] ..`
定义一个或多个类型为 `type` 的外部变量、标签或符号。该类型可以是 `ABS`，它会将 `name` 作为常量导入。与 `EXTRN` 相同。

# `EXTERNDEF [[langtype]] name:type|], [[langtype]] name:type|] ..`
定义一个或多个类型为 `type` 的外部变量、标签或符号。如果 `name` 在模块中已定义，则被视为 `PUBLIC`（公有）。如果 `name` 在模块中被引用，则被视为 `EXTERN`（外部）。如果 `name` 未被引用，则被忽略。该类型可以是 `ABS`，它会将 `name` 作为常量导入。通常用于文件。

# `EXTRN`
参见 `EXTERN`。

# `.FARDATA [[name|]]`
当与 `.MODEL` 一起使用时，为初始化数据启动一个数据段（段名为 `FAR_DATA` 或 `name`）。

# `.FARDATA? [[name|]]`
当与 `.MODEL` 一起使用时，为未初始化数据启动一个数据段（段名为 `FAR_BSS` 或 `name`）。

`FOR parameter [[:REQ |:=default|], [[argument argument|]]..`
`statements`

# `ENDM`
标记一个块，该块会对每个参数重复一次，在每次重复中用当前参数替换 `parameter`。与 `IRP` 相同。

# `FORC`
`parameter, <string> statements`

# `ENDM`
标记一个块，该块会对字符串中的每个字符重复一次，在每次重复中用当前字符替换 `parameter`。与 `IRPC` 相同。

`[[name|]] FWORD initializer [[, initializer|]] ..`
为每个初始化器分配并可选地初始化 6 字节的存储。也可以在任何合法的地方作为类型指定符使用。

# `GOTO macrolabel`
将汇编跳转到标记为 `:macrolabel` 的行。`GOTO` 仅在 `MACRO`、`FOR`、`FORC`、`REPEAT` 和 `WHILE` 块内部允许。标签必须是行上的唯一指令，且必须以冒号开头。

## D.7 MASM 指令

`name GROUP segment [[], segment]]..`
将指定的段添加到名为 `name` 的组中。此指令在 32 位平坦模型编程中使用时没有影响，且在与 `/coff` 命令行选项一起使用时会导致错误。

`.IF condition1`
`statements`
`[[.ELSEIF condition2`
`statements]]`
`[[.ELSE`
`statements]]`
`.ENDIF`
生成代码测试 `condition1`（例如 `AX > 7`），如果该条件为真，则执行语句。如果后续有 `.ELSE`，则当原始条件为假时执行其语句。请注意，条件是在运行时求求的。

`IF expression1`
`ifstatements`
`[[.ELSEIF expression2`
`elsestatements]]`
`[[.ELSE`
`elsestatements]]`
`ENDIF`
如果 `expression1` 为真（非零），则允许组装 `ifstatements`；如果 `expression1` 为假（0）且 `expression2` 为真，则允许组装 `elsestatements`。以下指令可以替换：`ELSEIF`, `ELSEIFB`, `ELSEDEF`, `ELSEDIF`, `ELSEIFDFTI`, `ELSEIFIFE`, `ELSEIFDN`, `ELSEIFIDNI`, `ELSEIFNB`, 和 `ELSEINFDEF`。可选地，如果上一个表达式为假，则组装 `elsestatements`。注意，表达式是在汇装时求求的。

`IF2 expression`
如果 `OPTION:SETIF2` 为 `TRUE`，则在每次汇装通过时评估 `IF` 块。查看 `IF` 的完整语法。

`IFB testitem`
如果 `testitem` 为空，则允许组装。查看 `IF` 的完整语法。

`IFDEF name`
如果 `name` 是之前定义的标签、变量或符号，则允许组装。查看 `IF` 的完整语法。

`IFDIFF[1|| testitem1, testitem2`
如果测试项不同，则允许组装。如果给出了 `I`，则比较不区分大小写。查看 `IF` 的完整语法。

# `IFE expression`
如果 `expression` 为假（0），则允许组装。查看 `IFE` 的完整语法。

# `IFIDN||I|text1,textitem2`
如果文本项相同，则允许组装。如果给了 `I`，则比较不区分大小写。查看 `IF` 的完整语法。

# `IFNB textitem`
如果 `textitem` 不为空，则允许组装。查看 `IF` 的完整语法。

# `IFNDEF name`
如果 `name` 未被定义，则允许组装。查看 `IF` 的完整语法。

# `INCLUDE filename`
在汇装期间将由文件名指定的源文件代码插入到当前源文件中。如果文件名包含反斜杠、分号、大于号、小于号、单引号或双引号，则必须包含角括号内。

# `INDELIB libraryname`
告知链接器当前模块应与 `libraryname` 链接。如果 `libraryname` 包含反斜杠、分号、大于号、小于号、单引号或双引号，则必须包含角括号内。

# `name INSTR ||position,|textitem1,textitem2`
在 `text1` 中查找 `textitem2` 的第一次出现。起始位置可选的。每个文本项可以是文字字符串、以 `%` 开头的常量或宏函数返回的字符串。

# `INVOKE expression ||,arguments`
调用 `expression` 给出的地址处的程序，根据语言类型的标准约定通过栈或寄存器传递参数。传递给程序的每个参数都可能是。

# `IRP`
参见 `FOR`。

# `IRPC`
参见 `FORC`。

# `name LABEL ||type`
通过表达式设置计数器。

# `name LABEL ||type`
通过表达式设置计数器。

# `name LABEL ||type`
通过表达式设置计数器。

# `name LABEL ||type`
通过表达式设置计数器。

# `name LABEL ||type`
通过表达式设置计数器。

# `name LABEL ||type`
通过表达式设置计数器。

# `name LABEL ||type`
通过表达式设置计数器。

# `name LABEL ||type`
通过表达式设置计数器。

# `name LABEL ||type`
通过表达式设置计数器。

# `name LABEL ||type`
通过表达式设置计数器。

# `LOCAL dename`
在过程定义（`PROC`）内部，`LOCAL` 定义在宏期间存在的变量。

`name MACRO [[parameter |:=default|]]..`
`statements`

# `ENDM`
标记一个块，该块会对每个参数重复一次，在每次重复中用当前参数替换 `parameter`。与 `IRP` 相同。

# `MMX`
启用 `MMX` 汇装。

`.MODEL memorymodel [[langtype]], [[stackoption]]`
初始化程序模型。`memorymodel` 可以是 `TINY`, `SMALL`, `COMPACT`, `MEDIUM`, `LARGE`, `HUGE` 或 `FLAT`。`langtype` 可以是 `C`, `FORTRAN`, `PASCAL`, `SYSCALL` 或 `STD`。`stackoption` 可以是 `NEARSTACK` 或 `FARSTACK`。

# `ORG expression`
通过表达式设置计数器。

# `%OUT`
参见 `ECHO`.

`[[name||] OWORD initializer [[, initializer|]] ..`
为每个初始化器分配并可选地初始化一个双字（16 字节）的存储。也可以在任何合法的地方作为类型指定符。此数据类型主要用于流 SIMD 指令；它包含一个 4 字节字节数组。

# `PAGE [[length||, width]]`
设置程序列表的行长度字符宽度。如果没有给出参数，则产生分页。

# `PAGE *`
增加节并将页码重置为 1。

# `POPCONTEXT context`
恢复部分或全部上下文（由 `PUSHCONTEXT` 指令保存）。上下文可以是 `ASSUMES`, `RADIX`, `LISTING`, `CPU` 或 `ALL`。

## D.7 MASM 指令

`[[ USES registlist ||], parameter ||:tag ||]..`
`- 语句`
`label ENDP`
标记名为 `label` 的过程块的开始和结束。该块中的语句可以使用 `CALL` 指令或 `INVOKE` 指令调用。

`label PROTO |||distance || ||langtype ||], [parameter ||:tag ||].`
函数的原型定义。

`PUBLIC |||langtype || name ||, [langtype || name ||]..`
使指定为 `name` 的每个变量、标签或绝对符号对程序中的所有其他模块均可用。

`PURGE ||macroname ||, macroname ||]..`
从内存中删除指定的宏。

`PUSHCONTEXT context`
保存当前上下文的所有或部分：段寄存器假设、基数值、列表和 cref 标志，或处理器/协处理器值。上下文可以是 `ASSUMES`, `RADIX`, `LISTING`, `CPU` 或 `ALL`.

`=name || QWORD initializer ||, initializer ||]..`
为每个初始化器分配并可选地初始化 8 字节的存储。也可以在任何类型的地方作为类型指定符使用。

# `.RADIX expression`
将默认基数（范围 2 到 16）设置为 `expression` 的值。

`name REAL4 initializer ||, initializer ||]..`
为每个初始化器分配并可选地初始化一个单精度（4字节）浮点数。

`name REAL8 initializer ||, initializer ||]..`
为每个初始化器分配并可选地初始化一个双倍精度（8字节）浮点数。

`name REAL10 initializer ||, initializer ||]..`
为每个初始化器分配并可选地初始化一个 10 字节浮点数。

`recordname RECORD fieldname:width ||= expression ||| [[fieldname:width ||= expression]..`
声明一个由指定字段组成的记录类型。`fieldname` 为字段命名，`width` 指定位数，`expression` 给出其初始值。

`.REPEAT`
`语句`

# `.UNTIL condition`
生成代码以重复执行语句块，直到条件变为真。可以用 `.UNTILCXZ`（当 `CX` 为 0 时变为真）来替换 `.UNTIL`。对于 `.UNTILCXZ`，条件是可选的。

# `REPEAT expression`
`语句`

# `ENDM`
标记一个重复 `expression` 次的块。与 `REPT` 相同。

# `REPT`
参见 `REPEAT`.

# `.SALL`
参见 `.NOLISTMACRO`.

# `name SBYTE initializer ||, initializer ||...`
为每个初始化器分配并可选地初始化一个有符号字节存储。也可以在任何类型的地方作为类型指定符使用。

# `name SDWORD initializer ||, initializer ||...`
为每个标识符分配并可选地初始化一个有符号双字（4字节）存储。也可以在任何类型的地方作为类型指定符使用。

# `name SEGMENT [[READONLY]] [[align]] [[combine]] [[use]] [[class]]`
`语句`
定义一个名为 `name` 的程序段，具有属性 `align` (`BYTE`, `WORD`, `DWORD`, `PARA`, `PAGE`), `combine` (`PUBLIC`, `STACK`, `COMMON`, `MEMORY`, at address, `PRIVATE`), `use` (`USE16`, `USE32`, `FLAT`) 和 `class`.

# `.SEQ`
按顺序排列段（默认顺序）。

# `.SFCOND`
参见 `.NOLISTIF`.

# `name SIZESTR textitem`
查找文本项的大小。

# `.STACK [[size]]`
当与 `.MODEL` 一起使用时，定义一个栈段（段名为 `STACK`）。可选的 `size` 指定栈的字节数（默认 1024）。`.STACK` 指令自动关闭栈语句。

# `.STARTUP`
生成程序启动代码。

# `STRUC`
参见 `STRUCT`.

```
name STRUCT [[alignment]], [[ NONUNIQUE]]
fielddeclarations
name ENDS
```
声明一个具有指定 `fielddeclarations` 的结构类型。每个字段必须是有效的数据定义。与 `STRUC` 相同。

```
name SUBSTR textitem, position [[, length]]
```
返回从 `position` 开始的 `textitem` 子字符串。文本可以是字面量字符串、以 `%` 前缀的常量或宏函数返回的字符串。

# `SUBTITLE text`
定义列表副。与 `SUBTTL` 相同。

# `SUBTTL`
参见 `SUBTITLE`.

```
name SWORD initializer [[, initializer]]..
```
为每个初始化器分配并可选地初始化一个有符号字（2字节）存储。也可以在任何类型的地方作为类型指定符使用。

```
name TBYTE initializer [[, initializer]]..
```
为每个初始化器分配并可选地初始化 10 字节存储。也可以在任何类型的地方作为类型指定符使用。

```
name TEXTEQU [[textitem]]
```
将 `textitem` 赋值给 `name`。文本可以是字面量字符串、以 `%` 前缀的常量或宏函数返回的字符串。

# `TFCOND`
切换假条件块的显示。

# `TITLE text`
定义程序列表标题。

# `name TYPEDEF type`
定义一个名为 `name` 的新类型，等同于 `type`.

```
name UNION [[alignment]], [[ NONUNIQUE]]
```
```
fielddeclarations
```
```
name || ENDS
```
