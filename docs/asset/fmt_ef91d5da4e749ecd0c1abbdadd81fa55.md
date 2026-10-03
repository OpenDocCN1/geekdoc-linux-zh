
$ encrypt --help-pretty-print | less RET

# 15.2.5 输出带有底纹的文本

你可以指定文本底纹（即水印）显示在页面上。要这样做，请使用 `-u` 选项，并将你想使用的文本作为参数引用。

⇒ 要向 PostScript 打印机打印 72 磅 Helvetica Bold 字体的标牌，请输入：

```
$ encrypt -B -f "Helvetica-Bold72" RET

RET
RET
CAUTION RET
RET
RET
WET PAINT RET
CTRL-D
```

此示例中的文本前面有几个空格，以便将其与边框隔开。

由于 72 磅字体非常大，你可能希望对较长的文本行使用 `--word-wrap` 选项，以便在单词边界处进行换行。你可能需要这个选项，因为由于较大的字体号，你可能会面临行超出页面宽度的风险。你还可以使用 `-r` 选项以横向方向打印文本，正如第 15.2.7 节 [以横向方向输出文本] 第 369 页所示。

要在页面的长边上打印 63 磅 Helvetica Bold 字体的标牌，输入：

```
$ enscript -B -r --word-wrap -f "Helvetica-Bold63" RET
RET
CAUTION WET PAINT RET
CTRL-D
```

**注意：** 要制作一个更华丽或更详细的消息或标牌，请在文本编辑器中创建一个文件，并按照你希望打印的效果对文件中每行的单词进行对齐，在必要的地方留空行。如果你很有野心，使用 `-p` 选项输出到文件也是明智的，在打印之前预览该文件（参见第 17.4.2 节 [预览 PostScript 文件] 第 414 页）。

# 15.2.4 输出带有语言高亮的文本

**encrypt** 工具可以识别超过四十种语言和格式，从 PERL 和 C 编程语言到 HTML、电子邮件和 Usenet 文章；enscript 可以根据语法高亮文本部分。在 UNIX 术语中，这被称为*格式化打印*。

下表列出了编写时可用的一些语言过滤器名称，并描述了它们所使用的格式或语言。

| 名称 | 过滤器格式或语言 |
| :--- | :--- |
| ada | Ada95 编程语言 |
| asm | 汇编列表 |
| awk | AWK 编程语言 |
| bash | Bash shell 编程语言 |
| c | C 编程语言 |
| changelog | ChangeLog 文件 |
| cpp | C++ 编程语言 |
| csh | Csh 脚本语言 |
| delphi | Delphi 编程语言 |
| diff | 由 diff 生成的普通“差异报告” |
| diffu | 由 diff 生成的统一“差异报告” |
| elisp | Emacs Lisp 编程语言 |
| fortran | FORTRAN 77 编程语言 |
| haskell | Haskell 编程语言 |
| html | 超文本标记语言 (HTML) |
| idl | IDL (CORBA 接口定义语言) |
| java | Java 编程语言 |
| javascript | Javascript 编程语言 |
| ksh | Ksh 编程语言 |
| m4 | M4 宏处理器编程语言 |
| mail | 电子邮件和 Usenet 文章 |
| makefile | make 的规则文件 |
| nroff | 使用 NROFF 格式化的手册页 |
| objc | Objective-C 编程语言 |
| pascal | Pascal 编程语言 |
| perl | PERL 编程语言 |
| postscript | PostScript 编程语言 |
| python | Python 编程语言 |
| scheme | Scheme 编程语言 |
| sh | Bourne shell 编程语言 |
| skill | Cadence Design Systems 类似 Lisp 的语言 |
| sql | Sybase 11 SQL |
| synopsys | Synopsys dc shell 脚本语言 |
| tcl | TCL 编程语言 |
| tsh | Tesch 脚本语言 |
| vba | Microsoft 的 Visual Basic for Applications 语言 |
| verilog | Verilog 硬件描述语言 |
| vhdl | VHSIC 硬件描述语言 (VHDL) |
| vrml | 虚拟现实建模语言 (VRML97) |
| zsh | Zsh 编程语言 |

要预打印一个文件，将文件名作为 `-E` 选项的参数，选项和参数之间不要有空格。
以下是使用此项的一些方法。

- 预打印 HTML 文件 `index.html`，输入：
  `$ encrypt -Ehtml index.html RET`
- 预打印保存到文件 `important-mail` 的电子邮件消息，并将其无表头输出到名为 `important-mail.ps` 的文件，输入：
  `$ encrypt -B -Email -p important-mail.ps important-mail RET`
- 预打印保存到文件 `important-mail` 的电子邮件消息，并在默认打印机上带有花丽的头部打印，输入：
  `$ encrypt -G -Email important-mail RET`

使用特殊的 `--help-pretty-print` 选项列出你所拥有的 encrypt 版本支持的语言。
要查看当前支持的语言列表，输入：

```
$ encrypt --help-pretty-print | less RET
```

# 15.2.5 输出带有底纹的文本

你可以指定文本底纹（即水印）显示在页面上。要这样做，请使用 `-u` 选项，并将你想使用的文本作为参数引用。

⇒ 要向 PostScript 打印机打印 72 磅 Helvetica Bold 字体的标牌，请输入：

```
$ encrypt -B -f "Helvetica-Bold72" RET
RET
RET
CAUTION RET
RET
RET
WET PAINT RET
CTRL-D
```

此示例中的文本前面有几个空格，以便将其与边框隔开。

由于 72 磅字体非常大，你可能希望对较长的文本行使用 `--word-wrap` 选项，以便在单词边界处进行换行。你可能需要这个选项，因为由于较大的字体号，你可能会面临行超出页面宽度的风险。你还可以使用 `-r` 选项以横向方向打印文本，正如第 15.2.7 节 [以横向方向输出文本] 第 369 页所示。

要在页面的长边上打印 63 磅 Helvetica Bold 字体的标牌，输入：

```
$ enscript -B -r --word-wrap -f "Helvetica-Bold63" RET
RET
CAUTION WET PAINT RET
CTRL-D
```

**注意：** 要制作一个更华丽或更详细的消息或标牌，请在文本编辑器中创建一个文件，并按照你希望打印的效果对文件中每行的单词进行对齐，在必要的地方留空行。如果你很有野心，使用 `-p` 选项输出到文件也是明智的，在打印之前预览该文件（参见第 17.4.2 节 [预览 PostScript 文件] 第 414 页）。

后跟一个数字来指定切片（slice）；切片从 1 开始编号。

⇒ 要打印文件 `annual-report.txt` 的第二个切片，请输入：
`$ encrypt --slice=2 annual-report.txt RET`

## 15.2.9 输出带缩进的文本

要对 encrypt 处理的过程进行缩进，请将缩进的字符数作为 `-i` 的参数，注意不要在选项和参数之间留空格。若要指定字符以外的单位，请在数字后加上以下之一：`"i"` 代表英寸，`"c"` 代表厘米，或 `"p"` 代表 PostScript 点。

⇒ 要使用 encrypt 的默认设置将文件 `installment.007` 的内容打印到默认打印机，并将行缩进半英寸，请输入：
`$ encrypt -i.5i installment.007 RET`

## 15.2.10 输出多份文本

在发送文本时，通过向 `#-n` 选项传递参数来输出多份副本。此选项在发送到文件时无效，但请注意 `lpr` 采用相同的选项（参见第 510 页的 [打印多个作业副本]，配方 25.1.2）。

⇒ 要使用默认的 encrypt 表头向 PostScript 打印机打印三份文件 `saved-mail`，请输入：
`$ encrypt -3 saved-mail RET`

## 15.2.11 输出列文本

若要指定以列输出文本，请将列数作为 `-columns=` 选项的参数。

⇒ 要使用 encrypt 处理将 `payroll-data` 发送到默认打印机，设置每页四列文本，请输入：
`$ encrypt -columns=4 payroll-data RET`

如果列数为 1 或 2，也可以直接将数字本身作为选项。使用 `-j` 选项为每列添加边框。

⇒ 要使用 encrypt 处理将 `payroll-data` 发送到默认打印机，设置每页两列文本，且每列都有边框，请输入：
`$ encrypt -j -2 payroll-data RET`

# 第 15 章：排版与文字处理 371

注：你也可以使用 `pr` 将文本置于分页的列布局中，然后将其发送给 `encript`（参见第 314 页的 [将文本置于分页列]，配方 13.3.4）。

## 15.2.12 输出文本的指定页面

若要指定 `encript` 输出文本的某些页面，请将页码范围作为 `-a` 选项的参数。你可以通过数字指定单个页，通过逗号分隔指定页列表，通过提供起始和结束页码（用连字符 `"-"` 分隔）指定页范围。

- 要使用默认 `encript` 表头打印文件 `saved-mail` 的第 2 到 10 页，请输入：

```
$ encript -a 2-10 saved-mail RET
```

打印奇数页或偶数页，使用特殊的 `"odd"` 和 `"even"` 参数。这对于打印双面页面很有用：首先打印奇数页，将输出送回打印机并打印偶数页。

- 这里有两种使用方法：

- 要使用默认表头打印文件 `saved-mail` 的奇数页，请输入：

```
$ encript -a odd saved-mail RET
```

- 要使用默认表头打印文件 `saved-mail` 的偶数页，请输入：

```
$ encript -a even saved-mail RET
```

## 15.2.13 通过过滤器输出文本

你可以将输入文本通过外部过滤器传递，由 `encript` 转换为 PostScript。该过滤器可以是工具或带引号的命令。将过滤器作为 `-I` 选项的参数，注意不要在选项和参数之间留空格。

- 要使用默认 `encript` 设置将文件 `sensitivity_training` 打印到默认过滤器，但在此之前将输入文本通过 `newspeak` 过滤器处理，请输入：

```
$ encript -I newspeak sensitivity_training RET
```

# 15.3 使用 TeX

teTeX
DEB: `tetex-base` `tetex-bin` `tetex-doc` `tetex-extra`
RPM: `tetex`
WWW: http://www.tug.org/teTeX/

基于 Linux 的系统，最强大的排版工具是 TeX 排版系统及软件。它是顶级的计算机排版工具——其输出超过或可比目前的所有其他系统。它能够执行的高级换行、分段落、连字符、间距调整等特性策略和算法，以及执行的精确度，在文字处理器中尚无法比拟。

TeX 系统本身——不是文字处理器或单一程序，而是一个大型文件和数据集合——以发行版的形式封装；`tetex` 是为 Linux 设计的 TeX 发行版。

TeX 输入文档是使用 TeX 排版语言编写的纯文本，TeX 工具可以对其处理并输出用于打印或查看的文件。这种方法对作者有很大益处：纯文本输入文件无论操作系统或编辑软件如何，可以在许多不同计算机之间编写和交换，且输入文件不会随着 TeX 版本的更新而过时或不可用。

世界算法领域的顶级权威 Donald E. Knuth 在 1984 年编写了 TeX，将其作为排版书籍的一种方式，因为他不满意现有系统的质量。自从发布以来，已经出现了许多事实上的扩展，最著名的是 LaTeX，它由 Leslie Lamport 在 1984 年创建。LaTeX 是构建在 TeX 之上的一个宏集，使得创建复杂文档变得更容易。

TeX 系统是一个大型文件和数据集合，以发行版的形式封装；`tetex` 是为 Linux 设计的 TeX 发行版。其他发行版包括 TeX Live，它是一套全面的 TeX 相关的软件。

TeX 文档是使用 TeX 排版语言编写的纯文本，TeX 工具可以对其处理并输出用于打印或查看的文件。这种方法对作者有很大益处：纯文本输入文件无论操作系统或编辑软件如何，可以在许多不同计算机之间编写和交换，且输入文件不会随着 TeX 版本的更新而过时或不可用。世界算法领域的顶级权威 Donald E. Knuth 在 1984 年编写了 TeX，将其作为排版书籍的一种方式，因为他不满意现有系统的质量。自从发布以来，已经出现了许多事实上的扩展，最著名的是 LaTeX，它由 Leslie Lamport 在 1984 年创建。LaTeX 是构建在 TeX 之上的一个宏集，使得创建复杂文档变得更容易。
