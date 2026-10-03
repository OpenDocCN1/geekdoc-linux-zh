
# 第 9 章：查看文本

## 9.2.2 指定输出行数

你可以指定一个数字选项作为输出的行数。如果你指定的行数多于文件内容，`head` 将输出整个文本。

⇒ 以下是使用此方法的两种方式。

- 要输出 `placement-list` 的第一行，输入：
  `$ head -1 placement-list RET`
- 要输出 `placement-list` 的前 66 行，输入：
  `$ head -66 placement-list RET`

要输出指定数量的字符（字节而非行），可以使用 `-c` 选项将要输出的字符数作为参数。

⇒ 要输出 `placement-list` 中的第一个字符，输入：

```bash
$ head -c 1 placement-list RET
```

> **注意**：一个名为 `line` 的旧 UNIX 工具只输出其输入的第一行。Linux 中已经没有这个工具了，但你可以通过将 `line` 定义为 `head -1` 的别名来做一个非常好的模仿（关于创建别名的更多信息，请参见方案 3.6 [使用别名单词]，第 82 页）。

## 9.2.3 显示文本的结尾部分

`tail` 的工作原理类似于 `head`，但它输出的是输入的最后部分。

⇒ 以下是使用此方法的几种方式。

- 要输出 `placement-list` 的最后十行，输入：
  `$ tail placement-list RET`
- 要输出 `placement-list` 的最后 14 行，输入：
  `$ tail -14 placement-list RET`
- 要输出 `placement-list` 的最后一百个字符，输入：
  `$ tail -c 100 placement-list RET`

要根据相对于文本开头的关系指定输出文本的某部分，请在数字前加加号（`+`）。

要输出某些文本的中间部分，你可以在管道上组合多个 `head` 或 `tail` 命令（参见方案 3.2.4 [将输出重定向到另一个命令的输入]，第 69 页）。

以下是使用此方法的几种方式。

- 要输出 `placement-list` 中的第十行，输入：
  `$ head placement-list | tail -1 RET`
- 要输出 `placement-list` 倒数第五和第四行，输入：
  `$ tail -5 placement-list | head -2 RET`
- 要输出 `placement-list` 中的第 500 个字符，输入：
  `$ head -c 500 placement-list | tail -c 1 RET`
- 要输出 `placement-list` 第五行的第一个字符，输入：
  `$ head -5 placement-list | tail -1 | head -c 1 RET`

在前面的示例中，使用了三个命令：将 `placement-list` 的前五行传递给 `tail`，`tail` 输出中的最后一行（即文件中的第五行）；然后，最后一个命令输出该行的第一个字符，从而实现了所需的结果。

## 9.2.5 显示字符串之间的文本

使用 `sed` 选择两个字符串之间的行并输出该部分文本，或者输出除该部分以外的所有文本行。

## 9.2.7 显示文本的十六进制值

所有字符都以数值的形式存储（参见方案 9.7 [查看字符]，第 228 页）。有时你可能想以十六进制显示这些值。

⇒ 要以十六进制格式查看文件 `details`，并将文件的可打印字符单独列在一列中，请输入：

```bash
$ od -t x1z details | less RET
```

### 方法 #3

**Midnight Commander**
DEB: `mc-common`
RPM: `mc`
UWW: `http://www.ibiblio.org/mc/`

在 `mc` 中查看文件时，你可以切换十六进制值的显示。要进行此操作，在目录列表中选中一个文件并按 `F3` 查看文件，然后在查看文件时按 `F4` 即可在 ASCII 字符或其十六进制值之间切换视图；按 `F10` 退出文件查看，再次按 `F10` 退出 `mc`。

### 方法 #4

在 Emacs 中查看缓冲区的十六进制转储，请使用 `hexl-mode`。

⇒ 查看当前缓冲区的十六进制转储，请输入：
`M-x hexl-mode RET`

> **注意**：此模式适用于在 Emacs 中查看和编辑二进制文件。

## 9.3 查看特殊类型的文本

这些是查看以特殊方式格式或用特定语言编写的文本的方法。

### 9.3.1 查看 HTML 格式的文本

查看 HTML 格式文本通常有两种方法，取决于你是想查看 HTML 源代码（格式化文本本身），还是查看渲染后的 HTML（应用了格式命令的文本）。

#### 方法 #1

要查看 HTML 格式的文本本身，只需像查看任何文本文件一样使用 `less` 查看即可，如第 211 页食谱 9.1 [查阅文本] 所述。

⇒ 要将 HTML 格式文件 `homepage.html` 作为 HTML 源代码查看，请输入：

```bash
$ less homepage.html
```

#### 方法 #2

要查看应用了 HTML 格式的 HTML 文本文件，请按照第 157 页食谱 5.10 [浏览文件和目录] 中的方法 #2 和 #3 在 Web 浏览器中打开文件。

⇒ 要将 HTML 格式文件 `homepage.html` 作为渲染后的 HTML 查看，请输入：

```bash
$ mozilla homepage.html
```

### 9.3.2 查看 NROFF 格式的文本

要查看用 NROFF 编写的文本（旨在用于 TROFF 或 GROFF 文本处理器），请使用 `man` 并配合 `-l` 选项。将要查看的文件名作为参数给出（使用 `_` 作为文件参数以查看标准输入）。默认情况下，`man` 将输出发送到 `less` 以供查阅。

⇒ 这里有两种使用方法：

- 要查看 `program.1`，请输入：
  `$ man -l program.1 RET`
- 要将 NROFF `program.1` 转换为文本并写入新文件 `program.txt`，请输入：

```bash
$ man -l program.1 > program.txt
```

在此示例中，新文件 `program.txt` 将包含表示粗体的覆盖字符。原始文件 `program.1` 保持不变。

> **注意**：所有手册页都以 NROFF 格式编写，因此使用该命令进行查看。

### 9.3.3 查看 C 程序源代码

查看 C 程序源代码至少有两种方法。

#### 方法 #1

**Cutils**
DEB: `cutils`
WWW: `http://www.sigala.it/sandro/software.html#cutils`

使用作为 Cutils 软件包分发的 `chilight` 过滤器来带有语言高亮地查看 C 程序代码。将文件名作为参数给出（如果省略文件名则使用标准输入），`chilight` 会输出以多种格式之一高亮的 C 程序源代码。通过向 `-f` 选项提供以下内容之一作为参数来指定高亮格式；默认值为 `tty`。

- `ansi_color`: 带有 ANSI 的 ASCII 文本。
- `ansi_bold`: 带有 ANSI 的 ASCII 文本。
- `html_color`: 带有颜色高亮的 HTML。
- `html_font`: 带有粗体和斜体高亮的单色 HTML。
- `roff`: TROFF 输入。
- `tty`: 带有覆盖字符的 ASCII 文本（默认）。

由于文本中的 ANSI 高亮由非打印控制序列组成，查阅此类输出请配合 `-R` 选项使用 `less`（参见第 214 页食谱 9.1.4 [查阅原始文本]）。

⇒ 要带有彩色语言高亮查阅文件 `myprog.c` 中的 C 程序源代码，请输入：

```bash
$ chilight -f ansi_color myprog.c | less -R RET
```

默认情况下，`chilight` 将输出发送到标准输出。若要写入文件，请将要写入的文件名作为 `-o` 选项的参数。

⇒ 要将文件 `myprog.c` 中的 C 程序源代码格式化为带有颜色高亮的 HTML 并输出到 `myprog.html`，请输入：

```bash
$ chilight -f html_color -o myprog.html myprog.c RET
```

#### 方法 #2

要带有高亮查看 C 程序源代码，请使用 `enscript` 对其进行“美化”，如第 365 页食谱 15.2.4 [输出带有语言高亮的文本] 所述。

此方法以 PostScript 格式输出文本，然后对其进行查看或打印。它也适用于许多语言和格式，而不只是 C ——参见上述食谱中的表格。

- 要以语言高亮的 PostScript 格式显示文件 `myprog.c` 中的 C 程序源代码，请输入：
  `$ enscript -E c -o - myprog.c | gv RET`

### 9.3.4 查看排序后的文本

使用 `sort` 按顺序显示行。将文件名作为参数给出，行将进行排序。

- 要查看排序后的 `list.txt`，请输入：
  `$ sort list.txt`
- 要将排序后的 `list.txt` 保存为 `sorted.txt`，请输入：
  `$ sort list.txt > sorted.txt`

### 9.3.5 查看下划线文本

使用 `grep` 查找下划线的行。将文件名作为参数给出，行将进行过滤。

- 要查看 `list.txt` 中的下划线行，请输入：
  `$ grep '_' list.txt`
- 要将 `list.txt` 中的下划线行保存为 `underlined.txt`，请输入：
  `$ grep '_' list.txt > underlined.txt`

### 9.3.6 在二进制文件中列出文本

使用 `strings` 输出二进制文件中的任何打印文本。将文件名作为参数给出，所有非文本将被过滤。有时，通过 `fmt` 过滤文本可以改进显示。

- 要将 `table.com` 中的任何字符串保存到 `table.txt`，请输入：
  `$ strings table.com > table.txt`
- 要查阅 `table.com` 中的任何字符串，请输入：
  `$ strings table.com | less`
- 要查阅 `table.com` 中任何字符串的格式化输出，请输入：
  `$ strings table.com | fmt | less`

### 9.3.7 查看字符集

字符集规范了集合中每个字符的数值表示。ASCII（美国信息交换标准）是一个自 1968 年以来一直使用的字符集，它仍然是计算的标准字符集。其他字符集也可用。Linux 默认字符集是 ISO 8859-1（拉丁1）字符集加上额外的 128 个字符。这些额外字符有时被称为扩展字符。

若干字符集有自己的手册页；要查看这些字符集之一，请查看相应的手册页（参见第 46 页 [从系统手册读取页面]）。

要查看 ASCII 集中所有有效字符的列表以及使用的字符代码，请查看 `ascii` 手册页。

⇒ 要查看 ASCII 字符集，请输入：

```bash
$ man ascii RET
```

这显示了每个字符的八进制、十进制和十六进制值，还显示了转义码。这些值对于引用特殊字符很有用。

`iso_8859_1` 手册页包含了整个 ISO 8859-1 字符集，包括标准 127 个 ASCII 字符以上的扩展字符。

⇒ 要查看 ISO 8859-1 字符集，请输入：

```bash
$ man iso_8859_1 RET
```
