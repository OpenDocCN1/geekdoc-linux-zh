
- 显式指定输入编码，覆盖所有其他方法。这对应于 `groff` 的 `-Kencoding` 选项。如果没有此开关，`preconv` 将使用下文描述的算法选择输入编码。

- `--help`
  - `-h` 打印帮助信息。

- `-r`
  - 不添加 `.If` 请求。

- `--version`
  - `-v` 打印版本号。

### 用法

`preconv` 尝试使用以下算法查找输入编码。

1. 如果使用选项 `-e` 显式指定了输入编码，则使用它。

2. 否则，检查输入是否以*字节顺序标记*（BOM，见下文）开头。如果找到，则使用它。

3. 最后，检查第一或第二行输入中是否有已知的*编码标记*（见下文）。如果找到，则使用它。

4. 如果所有方法都失败，则使用选项 `-D` 给出的默认编码、当前区域设置，或者如果区域设置为 ‘C’、‘POSIX’ 或为空（按此顺序），则使用 ‘latin1’。

请注意，`groff` 程序支持 `GROFF_ENCODING` 环境变量，该变量最终展开为选项 `-k`。

#### 字节顺序标记

Unicode 标准将字符 U+FEFF 定义为字节顺序标记（BOM）。另一方面，值 U+FFFE 保证不是 Unicode 字符。这使得可以检测数据流中的字节顺序（大端或小端），并且 MIME 编码 ‘UTF-16’ 和 ‘UTF-32’ 强制要求数据流以 U+FEFF 开头。类似地，编码为 ‘UTF-8’ 的数据流可能以 BOM 开头（以便于 UTF-16 和 UTF-32 之间的转换）。在所有情况下，字节顺序标记*不是*数据的一部分，而是编码协议的一部分；换句话说，`preconv` 的输出不包含它。

请注意，不在输入数据开头的 U+FEFF 实际上会被输出；此时它具有‘零宽不换行空格’字符的含义 - 这在 `groff` 中通常不需要。

#### 编码标记

支持多种字符编码的编辑器需要在输入文件中标记文件编码的标签。虽然借助启发式算法可以猜测代表较大量自然语言的数据的正确输入编码，但这仍然只是一个猜测。此外，所有算法对于太短或不表示自然语言的输入都很容易失败。

基于这些原因，`preconv` 支持 `GNU Emacs` 和 `XEmacs`（可能还有其他程序）使用的编码标记约定（带有一些限制）。

`GNU Emacs` 和 `XEmacs` 中的编码标记存储在某些所谓的*文件变量*中。`preconv` 识别以下必须放在 troff 注释的第一行或第二行中的语法形式。

### Iconv 问题

`preconv` 本身仅支持三种编码：latin-1、cp1047 和 UTF-8；所有其他编码都会传递给 `iconv` 库函数。在编译时会搜索并检查是否存在有效的 `iconv` 实现；调用 `preconv --version` 可以显示是否使用了 `iconv`。

`preconv` 中唯一相关的标签是 `coding`，它可以采用下方列出的值。这里有一个示例行，告知 `Emacs` 以 troff 模式编辑文件，并使用 latin2 作为其编码。

```text
." -*- mode: troff; coding: latin-2 -*-
```

以下列表给出了 `preconv` 支持的所有 MIME 编码标签（小写或大写）；此列表硬编码在源代码中。

- big5, cp1047, euc-jp, euc-kr, gb2312, iso-8859-1, iso-8859-2, iso-8859-5, iso-8859-7, iso-8859-9, iso-8859-13, iso-8859-15, koi8-r, us-ascii, utf-8, utf-16, utf-16be, utf-16le

此外，还识别以下其他硬编码标签列表，它们最终映射到上述列表中的值。

- ascii, chinese-big5, chinese-euc, chinese-iso-8bit, cn-big5, cn-gb, cn-gb-2312, cp878, csascii, csisolatin1, cyrillic-iso-8bit, cyrillic-koi8, euc-china, euc-cn, euc-japan, euc-japan-1990, euc-korea, greek-iso-8bit, iso-10646/utf8, iso-10646/utf-8, iso-latin-1, iso-latin-2, iso-latin-5, iso-latin-7, iso-latin-9, japanese-euc, japanese-iso-8bit, jis8, koi8, korean-euc, korean-iso-8bit, latin-0, latin1, latin-1, latin-2, latin-5, latin-7, latin-9, le-utf-8, le-utf-16, le-utf-16be, le-utf-16-le, le-utf-16be-with-signature, le-utf-16le, le-utf-16-le, le-utf-16le-with-signature, utf8, utf-16-be, utf-16-be-with-signature, utf-16be-with-signature, utf-16-le, utf-16-le-with-signature, utf-16le-with-signature

这些标签取自 `GNU Emacs` 和 `XEmacs`，以及一些别名。编码标签末尾的 `-dos`、`-unix` 和 `-mac` 后缀（指定文件中使用的行尾惯例）在与上述标签进行比较之前会被去除。

### 缺陷

`preconv` 尚不支持*局部变量列表*。这是在文件末尾指定局部变量的另一种语法形式。

### 参见

(1) `GNU Emacs` 和 `XEmacs` 信息页

### 版权

版权所有 2006-2014 Free Software Foundation, Inc.

允许制作和分发本手册的逐字副本，前提是在所有副本中保留版权声明和本许可声明。

允许在逐字复制的条件下，修改并分发本手册的修改版本，前提是最终的衍生作品整体根据与本许可声明相同的许可声明进行分发。

允许在修改版本的上述条件下，将本手册翻译成其他语言并分发，不同之处在于，此许可声明可以包含在 Free Software Foundation 批准的翻译中，而不是原始英文中。

### PRINTAFM

### 名称

`printafm` - 使用 ghostscript 打印 AFM 格式 Postscript 字体的 metrics

### 语法

```text
printafm fontna
```

### 描述

此脚本调用 (1) 以打印 AFM 格式字体的 metrics。输出到标准输出。

### 参见

(1)

### 版本

本文档最后修订于 Ghostscript 版本 9.16。

### 作者

Artifex Software, Inc. 是 Ghostscript 的主要维护者。本 manpage 由 George Ferguson 编写。

### PRINTENV

### 名称

`printenv` - 打印全部或部分环境变量

### 语法

```text
printenv [OPTION]... [VARIABLE]...
```

### 描述

打印指定环境变量 `VARIABLE` 的值。如果未指定 `VARIABLE`，则打印所有变量的名称和值对。

- `-0`, `--null`
  每行输出以 NUL 结束，而不是换行符

- `--help`
  显示此帮助并退出

- `--version`
  输出版本信息并退出

注意：你的 shell 可能有自己的 `printenv` 版本，通常此处描述的版本会被其取代。请查阅你 shell 的文档以了解它支持的选项详情。

### 作者

由 David MacKenzie 和 Richard Mlynarik 编写。

### 报告缺陷

GNU coreutils 在线帮助: <http://www.gnu.org/software/coreutils/> 将 `printenv` 翻译缺陷报告至 <http://translationproject.org/report.html>

### 版权

版权所有 2015 Free Software Foundation, Inc. 许可证 GPLv3+: GNU GPL 版本 3 或更高版本 <http://gnu.org/licenses/gpl.html>。这是自由软件：你可以自由修改和重新分发它。在法律允许的范围内，无保修。

### 参见

完整文档请访问: <http://www.gnu.org/software/coreutils/printenv> 或在本地通过 `info '(coreutils) printenv invocation'` 查看

### PRINTF

### 名称

`printf` – 格式化并打印数据
