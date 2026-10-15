
## 描述

`nm` 命令显示每个 ELF 对象文件的符号表。
如果有效输入文件可用符号信息，`nm` 命令会报告该事实，但不将其视为错误。

## 选项

你可以以任何顺序指定选项

# 944

## nm

- `-d` 以十进制格式写入偏移量（默认）。
- `-o` 以八进制格式写入偏移量。
- `-x` 以十六进制格式写入偏移量。

由于对象文件格式的更改，以下选项已过时，将在未来的版本中删除。

- `-e` 仅打印外部和静态符号。符号表现在只包含静态和外部符号。自动符号不再出现在符号表中。它们会出现在由 `cc -g` 产生的调试信息中，你可以使用 `dump(1)` 进行检查。

- `-f` 产生完整输出。之前存在的冗余符号（如 `.text` 和 `.data`）不再存在。产生完整输出与默认输出相同。

- `-T` 默认情况下，`nm` 打印列出的符号的完整名称。由于符号名称已移动到最后一列，溢出问题已消除；不再需要截断符号名称。

### `/usr/ccs/bin/nm`

- `-u` 仅打印未定义符号。

### `/usr/xpg4/bin/nm`

- `-u` 为每个未定义符号打印详细列表。
- `-v` 在打印外部符号之前先按值进行排序。
- `-V` 在标准错误输出上打印正在执行的 `nm` 命令的版本。
- `-x` 使用十六进制而不是十进制打印符号的值和大小（等同于 `-t x`）。

### 操作数

- `file` 对象文件、可执行文件或对象文件库的路径名。

## 输出

### 标准输出

对于每个符号，将打印以下信息：

- Index 符号的索引。（索引显示在括号中）。
- Value 符号的值以下之一：
    - 可重定位文件中定义符号的节偏移量。
    - 节索引为 `SHN_COMMON` 的符号的对齐约束。
    - 可执行文件和动态库文件中的虚拟地址。
    - 关联对象以字节为的大小。

符号为以下类型之一。

|  |  |
| --- | --- |
| NOTYPE | 未指定类型。 |
| OBJECT | 数据对象，例如数组或变量。 |
| FUNC | 函数或其他可执行代码。 |
| SECTION | 节符号。 |
| FILE | 源文件名。 |

符号的绑定属性。

|  |  |
| --- | --- |
| LOCAL | 将作用域限制在包含其定义的对象文件中。 |
| GLOBAL | 对所有合并的对象文件可见。 |
| WEAK | 指定全局符号的优先级低于 GLOBAL。 |

预留供未来使用，当前包含 0。

除三个特殊值外，与定义符号相关的节头表索引。存在以下特殊值：

|  |  |
| --- | --- |
| ABS | 符号的值在重定位过程中不改变。 |
| COMMON | 未分配的块，且值提供了对齐约束。 |
| UNDEF | 未定义符号。 |

符号名称。

如果你指定了 `-A`，则打印对象或库的名称。

如果你指定了 `-P` 选项，将使用以下可移植格式显示前面的信息。三个版本取决于你是否指定了 `-dt`、`-t` 或 `x`。

```
%s %s %s %%dn\n library/object-name, name, type, value, size
%s %s %o %%n\n library/object-name, name, type, value, size
%s %s %s %%x\n library/object-name, name, type, value, size
```

其中 `library/object-name` 的格式如下：

- 如果你指定了 `-A`，`library/object-name` 为空字符串。
- 如果你指定了 `%s` 且对应的文件操作不是库：`%s , file`
- 如果你指定了 `-A` 且对应的文件操作数为库。在这种情况下，`object-file` 是包含所描述符号的库中的文件名：`%s[%s]: , file, object-file`

# 946

如果你没有指定 `-λ`，如果指定了多个文件操作数，或者只指定了一个文件操作数并命名为库，`nm` 会在包含这些符号的行之前写一行来识别包含这些符号的对象，采用以下形式之一：

- 如果对应的文件操作数不是库：`%s:\n`
- 如果对应的文件操作数为库；在这种情况下，`object-file` 是库中包含以下符号的文件名：`%s[%s]:, file, object-file`

如果你指定了 `-P` 但没有指定 `-t`，其格式等同于你指定了 `-t x`。

## 示例

下面的示例显示了 `zipinfo` 命令输出的前几行。

```
castle# /usr/ccs/bin/nm /bin/zipinfo
[Index] Value Size Type Bind Other Shnd Name
[20] 216572 0 SEC LOCL 0 19
[2] 65748 0 SEC LOCL 0 1
[3] 65768 0 SEC LOCL 0 2
[4] 67380 0 SEC LOCL 0 3
[5] 70420 0 SEC LOCL 0 4
[6] 73532 0 SEC LOCL 0 5
[7] 73564 0 SEC LOCL 0 6
[8] 73588 0 SEC LOCL 0 7
[9] 73624 0 SEC LOCL 0 8
[10] 74296 0 SEC LOCL 0 9
[11] 148616 0 SEC LOCL 0 11
[12] 148672 0 SEC LOCL 0 12
[13] 148728 0 SEC LOCL 0 13
[14] 148732 0 SEC LOCL 0 14
[15] 148924 0 SEC LOCL 0 15
[16] 215644 0 SEC LOCL 0 16
[17] 215648 0 SEC LOCL 0 17
[18] 216372 0 SEC LOCL 0 18
[19] 216540 0 SEC LOCL 0 20
[21] 232300 0 SEC LOCL 0 21
[39] 0 0 NOTY 0 UNDEF
[22] 233152 0 SEC LOCL 0 22
[23] 0 0 SEC LOCL 0 23
[24] 0 0 SEC LOCL 0 24
[25] 0 0 SEC LOCL 0 25
[26] 0 0 SEC LOCL 0 26
[27] 0 0 SEC LOCL 0 27
[28] 0 0 SEC LOCL 0 27
[38] 0 0 NOTY 0 UNDEF
[566] 215996 0 FUNC 0 UNDEF .div
[473] 216008 0 FUNC 0 UNDEF .rem
[565] 216188 0 FUNC 0 UNDEF .udiv
[471] 216116 0 FUNC 0 UNDEF .urem
[484] 216608 4 OBT GLOB 0 19 Argv
```

* nm*

# nohup 947

|  |  |
| --- | --- |
| [522] | 216604 | 4 OBJT | GLOB | 0 | 19 | __cg8_used |
| [523] | 216604 | 4 OBJT | GLOB | 0 | 19 | __cg92_used |

## 环境变量

查看 `environ(5)` 以了解影响 `nm` 执行的以下环境变量：`LC_COLLATE`、`LC_CTYPE`、`LC_MESSAGES` 和 `NLSPATH`。

## 退出状态

- `0` 成功完成。
- `>0` 发生错误。

## 属性

查看 `attributes(5)` 以了解以下属性：

`/usr/ccs/bin/nm`

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNwbtool |

`/usr/xpg4/bin/nm`

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNWcu4 |

## 参见

`ar(1)`, `as(1)`, `dump(1)`, `ld(1)`, `ld.so(1)`, `a.out(4)`, `ar(4)`, `attributes(5)`, `environ(5)`, `XPG4(5)`

# nohup — 忽略挂断的命令

### 概要

```
/usr/bin/nohup command [argument...]
/usr/xpg4/bin/nohup command [argument...]
```
