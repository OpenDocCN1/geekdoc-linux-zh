
表示字体的 PostScript 名称是相同的。它还可能包含一个命令：

```
encodingfile
```

表示 PostScript 字体使用 `one_file` 中的编码进行重新编码；此文件应由一系列格式所示的行组成：

```
pschar code
```

其中 `pschar` 是字符，`code` 是其在编码中的位置。`pschar` 是字符的 PostScript 名称，`code` 是其在编码中的整数表示。

# grotty

## 另参见

`afmotdit(1)`, `groff(1)`, `psbb(1)`, `groff_out(5)`, `groff_font(5)`, `groff_char(7)`

Groff 版本 1.09, 1995年2月14日

## grotty

`grotty`—用于打字机类设备的驱动程序

### 概要

`grotty [-hfbudBuv][-FDir][-files ... ]`

### 描述

`grotty` 将 GNU `troff` 的输出转换为适用于打字机类设备的格式。通常，应该使用 `groff` 命令配合 `-TASCII` 或 `-Tlatin` 选项来调用 `grotty`。如果没有提供任何选项，`grotty` 将读取输入。文件名为 `-` 也会导致 `grotty` 读取标准输入。输出写入到标准输出 `stdout`。

通常情况下，`grotty` 使用序列 `BACKSPACE c'` 打印**粗体**字符 `c`，使用序列 `BACKSPACE c'` 打印*斜体* `c`。这些序列可以通过管道传输到 `ut(1)` 来显示。`asmuch(1)` 或 `less(1)` 也能显示这些序列。在传输到 `less(1)` 时使用 `-b` 或 `-u`；在传输到 `none(1)` 时使用 `-w`。不需要通过 `col(1)` 过滤输出，因为 `grotty` 永远不会反转换行。

字体描述字段可能包含

`internalname`

其中 `n` 是一个十整数。如果设置了 01 位，则该字体将被视为*斜体*字体；如果设置了 02 位，则将**视为**粗体**字体。字体描述字段包含用于输出字符的代码。该代码也可以用于 `troff` 中的 `8ja` 转义序列。

### 选项

- `-Fdir` 在目录 `dir/device` 中搜索字体和设备描述文件；name 是设备名称，通常为 `ascii` 或 `latin`。
- `-h` 在输出中使用水平制表符。假设制表符设置为 8 列。
- `-f` 在输出中使用表单页。在每个最后一行没有输出的页面末尾将有一个分页符 `form feed`。
- `-b` 抑制粗体字符的重叠打印 `overstriking`。
- `-u` 抑制斜体字符的下划线。
- `-B` 仅对粗体斜体字符使用重叠打印。
- `-O` 仅对粗体斜体字符使用下划线。
- `-O` 抑制重叠打印 `粗体或下划线除外`。
- `-d` 忽略所有 3D 命令。借此，`grotty` 将忽略至少具有零参数 `因此可以是水平或垂直` 且使用 `-`、`~` 和 `+` 字符的 `D1 ...` 命令。
- `-v` 打印版本号。

## 文件

- `/usr/lib/groff/font/devascii/DESC` `ascii` 设备的描述文件。
- `/usr/lib/groff/font/devascii/F` `ascii` 设备字体 `F` 的字体描述文件。
- `/usr/lib/groff/font/devlatin/DESC` `latin` 设备的设备描述文件。
- `/usr/lib/groff/font/devlatin/F` `latin` 设备字体 `F` 的字体描述文件。
- `/usr/lib/groff/mac/tmac.tty` 带有 `grotty` 的 mac 宏。
- `/usr/lib/groff/mac/tmac.tty-char` 为 `grotty` 额外的粗糙字符定义。

![](img/404e59cc9cb271dc62eb5b69e195df8b_267_0.png)

# 第一部分：用户命令

## 缺陷

`grotty` 仅用于简单文档。

不支持分数水平或垂直移动。

不支持除水平和垂直线以外的 `\d` 命令。

第一行以上的字符 `即垂直位置为 # 的` 无法打印。

## 另参见

`groff(1)`, `groff(1)`, `groff_out(5)`, `groff_font(5)`, `groff_char(7)`, `ul(1)`, `more(1)`, `less(1)`

Groff 版本 1.09, 1999年9月15日

# gsoelim

`gsoelim`—解释 `groff` 中的请求

### 概要

```
gsoelim [ -Cv ] [[files ... ]
```

### 描述

`gsoelim` 读取文件并将文件中的行

```
.sofile
```

替换为文件的内容。如果包含在 `so` 中的文件需要进行预处理，则该工具非常有用。通常，应该使用 `groff` 的 `-s` 选项调用 `gsoelim`。

### 选项

- `-C` 当 `so` 后面跟随非空格或换行符字符时识别它
- `-v` 打印版本号

## 另参见

`groff(1)`

Groff 版本 1.09, 1999年9月15日

# gtbl

`gtbl`—为 `troff` 格式化表格

### 概要

```
gtbl [ -Cv ] [[files ... ]
```

### 描述

本手册页描述了 `gtbl` 的 GNU 版本，它是 `groff` 格式化系统的一部分。`gtbl` 将嵌入 `troff` 输入文件中的表格描述编译为 `troff` 可理解的命令。通常，应该使用 `groff` 的 `-t` 选项来调用它。它与 UNIX `ttbl` 具有高度兼容性。GNU `gtbl` 生成的输出不能用 UNIX `troff` 处理；必须用 GNU `troff` 处理。如果命令行上没有提供文件，将读取标准输入。文件名为 `-` 将导致读取标准输入。

### 选项

- `-C` 即使 `.TS` 和 `.TE` 后面跟随非空格或换行符字符也识别它们
- `-v` 打印版本号

### 用法

- `-C` 即使 `.TS` 和 `.TE` 后面跟随非空格或换行符字符也识别它们
- `-v` 打印版本号

### 缺陷

此页面描述了 `gtbl` 的 GNU 版本，它是 `groff` 格式化系统的一部分。`gtbl` 将嵌入 `troff` 输入文件中的表格描述编译为 `troff` 可理解的命令。通常，应该使用 `groff` 的 `-t` 选项来调用。它与 UNIX `ttbl` 具有高度兼容性。GNU `gtbl` 生成的输出不能用 UNIX `troff` 处理；必须用 GNU `troff` 处理。如果命令行上没有提供文件，将读取标准输入。文件名为 `-` 将导致读取标准输入。

# 270

# 第一部分：用户命令

### 描述

本手册页描述了 `gtbl` 的 GNU 版本，它是 `groff` 格式化系统的一部分。`gtbl` 将嵌入 `troff` 输入文件中的表格描述编译为 `troff` 可理解的命令。通常，应该使用 `groff` 的 `-t` 选项来调用。它与 UNIX `ttbl` 具有高度兼容性。GNU `gtbl` 生成的输出不能用 UNIX `troff` 处理；必须用 GNU `troff` 处理。如果命令行上没有提供文件，将读取标准输入。文件名为 `-` 将导致读取标准输入。

### 选项

- `-a` 生成...的 ASCII 表示
- `-E` 抑制所有错误消息
- `-C` 启用兼容模式
- `-dcs,name=s` 定义 `name` 为字符串；`c` 必须是单字母名称
- `-ffan` 使用 `fan` 作为默认字体族
- `-mname` 读入 `tmac` 文件
- `-R` 不加载 `roff`
- `-nnum` 打印第一页
- `-olist` 只输出文本中的页码，逗号分隔的页范围列表；`n` 表示打印第 `n` 页；`n-m` 表示打印 `n` 到 `m` 之间的所有页；`n` 表示从第一页到 `n` 页；打印列表结束后退出
- `-rcn,name=n` 设置设备号或名称为 `n`；`c` 必须是单字符名称；`n` 可以是任何 `troff` 数字表达式
- `-Tname` 为设备号准备输出，而不是默认的 `ps`
- `-Fdir` 在目录 `dir` 中搜索子目录 `devname` `即的` DESC 文件和字体文件，在正常的 `/usr/lib/groff/font` 之前
- `-Mdir` 在正常的 `/usr/lib/groff/tmac` 之前搜索宏文件

### 用法

此处仅描述了 UNIX `troff` 不包含的功能。

## 长名称

寄存器、字体、字符串/宏、特殊字符的名称可以是任意长度。转义序列中您可以使用 `[]` 用于双字符名称，您可以使用 `\[xxx]` 用于任意长度：

- `\[xxx\]` 打印名为 `xxx` 的特殊字符
- `\f\[xxx\]` 设置字体 `xxx`
- `\^\[xxx\]` 插入字符串 `xxx`
- `\n\[xxx\]` 插入数字寄存器 `xxx`

## 分数点大小

一个缩放点等于 `1/izescale`，其中 `izescale` 在 `DESC` 文件中指定 `默认为 1`。这里有一个新的指示符 `z`，其效果是乘以大小。`troff` 中的请求和转义序列解释表示点大小的参数时是以缩放点为单位的，但它们使用默认比例对每个参数进行求值。

`gtroff`
