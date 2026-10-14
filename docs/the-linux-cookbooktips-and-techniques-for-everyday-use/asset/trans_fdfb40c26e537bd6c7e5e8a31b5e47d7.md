

如果你的系统连接了不止一台打印机，请将要发送到的打印机作为参数指定给 `-P` 选项。（打印机也有名称，就像用户账户和主机一样，命名是管理员的特权；默认打印机通常称为 lp，即“行式打印机”。）

- 要将文件 `nightly-report` 发送到名为 bossomatic 的打印机，输入：

```
$ lpr -P bossomatic nightly-report RET
```

注意：lpr 工具的名称来源于“line printer”，这是该程序最初开发时流行的打印机硬件类型。

## 26.1.2 打印作业的多个副本

要打印一份打印作业的多个副本，请将要打印的副本数作为参数提供给 lpr 的 `-#` 选项。

- 要打印文件 `nightly-report` 的十二份副本，输入：

```
$ lpr -#12 nightly-report RET
```

## 26.1.3 列出你的打印作业

要列出你的打印作业，请使用 lpq，即“line printer queue”工具。它输出当前在默认打印机 spool 队列中的所有打印作业的列表——每行一个——给出其在队列中的排名、发送作业的用户名、打印作业编号、作业中的文件名以及要打印的数据大小，以字节为单位。

- 要查看默认打印机的 spool 队列，输入：

```
$ lpq RET
lp is ready and printing
Rank Owner Job Files Total Size
active groucho 83 cigar.ps 1739030 bytes
1st harpo 84 harp.ps 499 bytes
2nd chico 85 love.ps 45576 bytes
$
```

在此示例中，有三个作业排队等待默认打印机——一个由用户 groucho 提交，用于文件 `cigar.ps`，一个由用户 harpo 提交，用于文件 `harp.ps`，以及一个由用户 chico 提交，他打印了一个名为 `love.ps` 的文件。

用户 groucho 的作业是活动作业；这是当前正在打印机上打印的作业。其他作业必须等待此文件打印完成，然后按排名顺序打印。

与 lpr 一样，你可以指定打印机名称作为 `-P` 选项的参数。

- 要查看名为 bossomatic 的打印机的 spool 队列，输入：

```
$ lpq -P bossomatic RET
```

要仅列出特定用户的作业，请将用户名作为参数给出。

- 要列出用户 harpo 的打印作业，输入：

```
$ lpq harpo RET
```

注意：当没有打印作业时，lpq 输出文本 `no entries`。

## 26.1.4 取消打印作业

要取消打印作业并将其从 spool 队列中移除，请使用 lprm，即“line printer remove”工具。将要移除的打印作业的编号作为参数给出。

- 要取消打印作业 83，输入：

```
$ lprm 83 RET
```

要取消 spool 队列中你所有的打印作业，请使用连字符代替打印作业的编号。

- 要取消你所有的打印作业，输入：

```
$ lprm - RET
```

注意：如果尝试取消一个活动作业——即已 spool 到打印机的作业——不要惊慌，如果仍有部分页面打印出来；打印机可能已将作业的一部分缓存在其内部打印缓冲区中。要停止

## 26.2 打印的更多配方

除了创建打印作业之外，另一种打印方式是从应用程序内部打印。

并非所有应用程序都有打印控件，但有些应用程序有——包括 Emacs 和 LyX（参见章节 LyX Document Processing）。它们的打印命令本质上是通过 lpr 将打印作业发送到打印机，可能在发送前对要打印的数据进行格式化或其他准备。如果你正在使用此类应用程序并想打印你的工作，使用内置的打印控件可能比去 shell 运行 lpr 更容易。

例如，要在 LyX 文档处理应用程序中打印当前文档，请从文件菜单中选择打印；它会为你的打印机创建适当的输出并制作包含此输出的打印作业（参见章节 LyX Document Processing）。

一些工具，例如 dvips 和 enscript（参见章节 Converting Plain Text for Output），也配置为将输出 spool 到打印机。

你可以在 spool 队列中查看这些打印作业，也可以取消它们，就像任何打印作业一样。

- 26.2.1 Printing in Emacs
- 26.2.2 Printing with Dvips
+ Printing with dvips.
- 26.2.3 Printing the Contents of an Xterm Window
+ Printing an xterm window.

## 26.2.1 Printing in Emacs

要在 Emacs 中打印当前缓冲区，请从菜单栏上的工具菜单下的打印子菜单中选择打印缓冲区。打印子菜单上的另一个选项是打印区域，它仅打印点与标记之间的文本（参见章节 Getting Acquainted with Emacs）。这两个命令都会将硬拷贝输出分页，并为每一页顶部加上页眉，显示文件名和当前页码。

要生成并打印缓冲区的 PostScript 图像，请使用 ps-print-buffer 函数，该函数也在打印子菜单上。相关的函数 ps-print-region 打印区域的 PostScript 图像。这些命令对于将缓冲区的文本发送到 PostScript 打印机很有用。

