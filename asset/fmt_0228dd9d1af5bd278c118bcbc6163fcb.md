
使用 `-j` 选项在页面周围绘制边框。

⇒ 要将 72 点 Helvetica 粗体字体的标牌打印到 PostScript 打印机，输入：

```
$ enscript -B -j -f "Helvetica-Bold72" RET
RET
RET
CAUTION RET
RET
RET
WET PAINT RET
CTRL -D
```

此示例中的文本前面加上了几个空格字符，以将其与边框区分开。

由于 72 点字体非常大，对于较长的文本行，你可能希望使用 `--word-wrap` 选项在单词边界处换行。你可能需要此选项，因为在这些较大的字体大小下，你可能会创建比页面宽度更长的行。你也可以使用 `-r` 选项以横向打印文本，如 Recipe 15.2.7 [Outputting Text in Landscape Orientation], page 369 中所述。

⇒ 要将 63 点 Helvetica 粗体字体的标牌横向打印在页面的长边上，输入：

```
$ enscript -B -r --word-wrap -f "Helvetica-Bold63" RET
RET
RET
CAUTION -- WET PAINT RET
CTRL -D
```

NOTES: 要制作更精美或更详细的标语或标牌，请在文本编辑器中创建一个文件，并在文件中按所需打印方式对每行文字进行对齐，并在必要处留出空行。如果你有如此大的野心，最好使用 `-p` 选项先输出到文件，并在打印前预览该文件（参见 Recipe 17.4.2 [Previewing a PostScript File], page 414）。

## 15.2.4 使用语言高亮输出文本

`enscript` 工具目前识别超过四十种语言和格式的格式，从 PERL 和 C 编程语言到 HTML、电子邮件和 Usenet 新闻文章；`enscript` 可以根据语法高亮文本的某些部分。在 UNIX 术语中，这称为 pretty-printing。

下表列出了截至本书撰写时可用的一些语言过滤器的名称，并描述了它们所使用的格式或语言。

| Filter Name | Format or Language |
|---|---|
| ada | Ada95 programming language |
| asm | Assembler listings |
| awk | AWK programming language |
| bash | Bash shell programming language |
| c | C programming language |
| changelog | ChangeLog files |
| cpp | C++ programming language |
| csh | Csh script language |
| delphi | Delphi programming language |
| diff | Normal "difference reports" made from diff |
| diffu | Unified "difference reports" made from diff |
| elisp | Emacs Lisp programming language |
| fortran | FORTRAN 77 programming language |
| haskell | Haskell programming language |
| html | HyperText Markup Language (HTML) |
| idl | IDL (CORBA Interface Definition Language) |
| java | Java programming language |
| javascript | Javascript programming language |
| ksh | Ksh programming language |
| *(continued)* |  |
| m4 | m4 macro processor programming language |
| mail | Electronic mail and Usenet news articles |
| makefile | Rule files for make |
| nroff | Manual pages formatted with NROFF |
| objc | Objective-C programming language |
| pascal | Pascal programming language |
| perl | PERL programming language |
| postscript | PostScript programming language |
| python | Python programming language |
| scheme | Scheme programming language |
| sh | Bourne shell programming language |
| skill | Cadence Design Systems Lisp-like language |
| sql | Sybase 11 SQL |
- `states` `states` 的定义文件
- `synopsys` Synopsys dc shell 脚本语言
- `tcl` TCL 编程语言
- `tcsh` Tcsh shell 脚本语言
- `vba` Microsoft 的 Visual Basic for Applications 语言
- `verilog` Verilog 硬件描述语言
- `vhdl` VHDL 硬件描述语言 (VHDL)
- `vrml` Virtual Reality Modeling Language (VRML97)
- `zsh` Zsh 编程语言

要美化打印一个文件，请将要使用的过滤器的名称作为 `-E` 选项的参数给出，且选项与参数之间不要有任何空白。

⇒ 以下是一些使用方法。

- 要美化打印 HTML 文件 `index.html`，输入：

  `$ enscript -Ehtml index.html [RET]`

- 要美化打印保存到文件 `important-mail` 中的电子邮件消息，并将其无头输出到名为 `important-mail.ps` 的文件，输入：

  `$ enscript -B -Email -p important-mail.ps important-mail [RET]`

- 要美化打印保存到文件 `important-mail` 中的电子邮件消息，并使用花哨的页眉打印到默认打印机，输入：

  `$ enscript -G -Email important-mail [RET]`

使用特殊的 `--help-pretty-print` 选项来列出你所拥有的 `enscript` 副本支持的语言。

⇒ 要浏览当前支持的语言列表，输入：

`$ enscript --help-pretty-print | less [RET]`

## 15.2.5 使用底纹输出文本

你可以指定一个文本 *underlay*，这是一种印刷水印，会出现在文本页上。要做到这一点，请将文本作为 `-u` 选项的参数给出，确保选项与文本之间不要跳过任何空格。如果文本多于一个词，请将其引用。

⇒ 要使用默认的 enscript 格式打印文件 `intelligence.report`，并带有“TOP SECRET”的底纹，输入：

```
$ enscript -u"TOP SECRET" intelligence.report [RET]
```

有许多选项用于指定底纹的属性，如下表所述。

| Option | Description |
|---|---|
| --ul-angle=angle | 指定底纹的角度，单位为度（默认为两个变量的反正切：负的页面高度和其宽度）。 |
| --ul-font=name | 指定底纹的字体和磅值（默认为 200 磅的 Times Roman）。 |
| --ul-gray=number | 指定用于着色底纹的灰度值，取值范围在 0 到 1 之间（默认为 0.8）。 |
| --ul-position=position | 指定底纹的起始位置，以 PostScript 坐标表示。X 位置给出，其前面加上“+”或“-”，后面跟随 Y 位置，Y 位置以同样方式给出（例如，左上角为“+0-0”）。 |
| --ul-style=style | 指定文本样式，要么是“outline”仅打印字符轮廓（默认值），要么是“filled”，字符用灰色填充。 |

## 15.2.6 使用花哨页眉输出文本

要使用花哨的图形页眉输出文本，其中页眉文本以不同灰度块设置，请使用 `-G` 选项运行 `enscript`。

⇒ 以下是两种使用方法。

- 要将文本文件 `saved-mail` 的内容打印到 PostScript 打印机，输入：
