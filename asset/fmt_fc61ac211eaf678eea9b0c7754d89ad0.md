
在示例示例使用的 `-B` 选项用于省略每页头部的输出。当使用头部时，它们通常是 10 磅的 Courier 粗体；要为头部文本指定不同的字体，请将其名称作为 `-F` 选项的参数。

- 要在 PostScript 打印机上打印文本文件 `saved-mail` 的内容，字体设置为 10 磅的 Times Roman，头部文本设置为 18 磅粗体，请输入：

```bash
$ encrypt -f "Times-Roman10" -F "Times-Bold18" saved-mail RET
```

- 要创建一个包含文本文件 `saved-mail` 内容的 PostScript 文件 `saved-mail.ps`，文本和头部设置为 16 磅的 Palatino-Roman，请输入：

```bash
$ encrypt -f "Palatino-Roman16" -F "Palatino-Roman16" -p saved-mail.ps saved-mail RET
```

## 16.2.2 输出海报或标牌输出文本

你可以通过省略输入文件的名称，直接输出到打印机（或 PostScript 文件）任何你打印的文本；`encrypt` 将从标准输入读取文本，直到你使用新行。

这对于制作快速的标牌或海报非常有用——要做到这一点，你需要为文本指定大字体（例如 72 磅的 Helvetica Bold），并省略默认头部。

- 要将 72 磅的 Helvetica Bold 标牌打印到 PostScript 打印机，请输入：

```bash
$ encrypt -B -f "Helvetica-Bold72" RET
RET
CAUTION RET
RET
WET PAINT! RET
C-d
```

72 磅字体非常大；可能需要使用 `--word-wrap` 选项来防止文本行超出页面的风险。你也可以使用 `-r` 选项以横向方向打印文本。

- 要要在页面长边打印 63 磅的 Helvetica Bold 标牌，请输入：

```bash
$ encscript -B -r --wrap -f "Helvetica-Bold63" RET
RET
CAUTION RET
RET
WET PAINT! RET
```

**注意：** 为了制作更漂亮或更详细的消息或标牌，你应该在文本编辑器中创建一个文件，并使用 `-p` 选项输出到文件（参见 PostScript）。

## 16.2.3 带语言高亮输出文本

`encrypt` 工具识别四十多种语言和格式，从 Perl 到 HTML；`encrypt` 可以其语法高亮文本部分。在 Unix 术语中，这被称为*漂亮打印*。下表列出了可用的过滤器名称及其用途。

| FILTER | LANGUAGE |
| :--- | :--- |
| ada | Ada95 语言 |
| asm | 汇编列表 |
| awk | AWK 语言 |
| bash | Bourne-Again shell 语言 |
| c | C 语言 |
| changelog | ChangeLog |
| cpp | C++ 脚本语言 |
| csh | C-Shell 脚本语言 |
| delphi | Delphi 语言 |
| diff | diff 的普通报告 |
| diff | diff 的统一报告 |
| elisp | Emacs Lisp 语言 |
| fortran | Fortran77 语言 |
| hask | Haskell 语言 |
| html | 超文本标记 (HTML) |
| idl | IDL (CORBA 接口语言) |
| java | Java 语言 |
| javascript | JavaScript 语言 |
| ksh | Korn shell 语言 |
| m4 | M4 处理器语言 |
| mail | 电子邮件和 Usenet 文章 |
| makefile | make 的文件 |
| nroff | nroff 格式化的帮助页 |
| objc | Objective-C 语言 |
| pascal | Pascal 语言 |
| perl | Perl 语言 |
| postscript | PostScript 语言 |
| python | Python 语言 |
| scheme | Scheme 语言 |
| sh | Bourne shell 类语言 |
| sql | Sybase SQL |
| syncops | Synopsys 脚本语言 |
| tcl | Tcp 语言 |
| tcsh | TC-Shell 脚本语言 |
| vba | Visual Basic (for Applications) |
| verilog | Verilog 硬件描述语言 |
| vh | VHDL 硬件描述语言 |
| vrml | 虚拟建模语言 (VRML7) |
| zsh | Z-shell 语言 |

要漂亮打印文件，将使用的过滤器名称作为 `-E` 选项的参数，选项和参数之间不要留空格。

- 要漂亮打印 HTML 文件 `index.html`，请输入：

```bash
$ encrypt -Ehtml.html RET
```

- 要漂亮打印邮件 `important-mail`，并无头部输出到名为 `important-mail.ps` 的文件，请输入：

```bash
$ encrypt -B -p important-mail.ps important-mail RET
```

特殊的 `--help-pretty-print` 选项列出你使用的 `encrypt` 版本支持的语言。

- 要查看当前支持的语言列表，请输入：

```bash
$ encrypt --help-pretty-print | less RET
```

## 16.2.4 带花式标题输出文本

要输出带花式标题的文本（头部文本设置为各种灰色块），请使用带有 `-G` 选项的 `encrypt`。

- 要在 PostScript 打印机上带花式标题打印文件 `saved-mail` 内容，请输入：

```bash
$ encrypt -G saved-mail RET
```

- 要创建一个包含文本文件 `saved-mail` 内容的带花式标题 PostScript 文件 `saved-mail.ps`，请输入：

```bash
$ encrypt -p saved-mail.ps saved-mail RET
```

如果没有 `-G` 选项，`encrypt` 会带粗体普通头部输出文本，打印文件名和最后修改时间。如前所述，`-B` 选项省略所有头部。

你可以通过将想要的文本作为 `-b` 选项的引用参数来自定义头部文本。使用特殊符号 `%%` 来指定头部文本中的当前页码。

- 要带有包含当前页码的自定义头部标签打印文件 `saved-mail` 内容，请输入：

```bash
$ encrypt -b "Page %% of the email archive" saved-mail RET
```

**注意：** 你可以创建自己的自定义花式标题——这在 `encryptman` 页面的 `CUSTOMIZATION` 章节中描述。

## 16.2.5 以横向方向输出文本

要以*横向*方向输出文本（即文本逆时针旋转 90 度），请使用 `-r` 选项。

- 要将文本文件 `saved-mail` 的内容打印到 PostScript 打印机，并将字体设置为 28 磅 Times Roman 且为横向，请输入：

```
$ encrypt -f "Times-Roman28" -r saved-mail RET
```

- `-r` 选项用于通过将 `figlet` 工具的输出传递给 `encrypt` 来制作水平横幅（参见[水平文本字体](https://www.linuxcookbook.org/encryption/horizontal-fonts.html) 节）。

- 要以 figlet 字体输出文本 `This is a long banner`，并以 18 磅 Courier 字体和横向方向写入打印机文本中，请输入：

```
$ figlet "A long banner" | encrypt -B -r -f "Courier18" RET
```

## 16.2.6 输出多份副本的文本

在使用 `encrypt` 向打印机发送文本时输出多个副本，请将数字作为 `-n` 选项的参数。该选项在发送到文件时不起，但请注意 `pr` 采用相同的选项（参见[打印作业的副本](https://www.linux cookbook.org/encryption/multiple-copies.html) 节）。

- 要使用默认的 `encrypt` 头部将文本文件 `saved-mail` 的三份副本打印到 PostScript 打印机，请输入：

```
$ encrypt -n3 saved-mail RET
```
