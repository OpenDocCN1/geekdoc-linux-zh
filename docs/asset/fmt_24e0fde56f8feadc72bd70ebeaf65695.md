
由于只有 SUSE 知道的原因，SUSE 发行版没有附带 `mpage`，它的功能与 `mpup` 相同，但通常做得更好。随当前 Fedora Linux 版本分发的 `mpage` RPM 可以在 SUSE 上正确安装和运行。

页头被 `-B` 抑制，而 `-R` 强制使用竖向格式。`-o` 选项指定输出文件。

## encrypt

`a2ps` 命令将文件转换为 PostScript 并创建一个文件或发送到打印机。如果你只需输入 `a2ps file`，文件将带有更漂亮的页头和页脚打印，显示文件名和日期、打印者的用户名以及打印日期。你可以通过多种选项来控制 `a2ps` 的工作；例如，此命令：

```
a2ps -j -B -columns=1 file -o output.ps
```

这将创建一个 PostScript 文件 `output.ps`，显示原始文件的文本，并且页面周围有一个精美的框（`-j` 选项），但没有其他页头或页脚。

## mpup 和 mpage

虽然在技术上不属于此主题，但这里是提到 `mpup` 以及 `useutils` 包中其他 PostScript 脚本的好时机。`mpup` 可以获取一个 PostScript 文件并创建一个物理页面包含多个页面的新文件。如果你想节省纸张墨水，这是你可能想要做的。例如：

```
mpup -4 file.ps:fileup.ps
```

在输出文件中每个物理页面放置四页 `file.ps`。

由于只有 SUSE 知道的原因，SUSE 发行版没有附带 `mpage`，它的功能与 `mpup` 相同，但通常做得更好。随当前 Fedora Linux 版本分发的 `mpage` RPM 可以在 SUSE 上正确安装和运行。

页头被 `-B` 抑制，而 `-R` 强制使用竖向格式。`-o` 选项指定输出文件。

## encrypt

`encrypt` 命令的功能与 `a2ps` 相同。`encrypt` 具有其他功能，包括以 HTML 格式输出。关于所有的选项列表，请参阅 `man` 页面。

## 比较文件

你通常会有同一个文件的不同版本，你需要一种方法来找到它们之间的差异。本节关注于版本控制。特别是，`diff` 和 `patch` 命令对于经常需要以文本格式分发更改的程序员来说非常重要。

## cmp

`cmp` 命令比较两个文件并告诉它们有何不同，但方式并不好用。对于大多数用途，`diff` 是一个更好的工具。

## diff 和 patch

`diff` 工具比较两个文件并产生描述它们差异的输出。在简单的情况下，如果两个文件是相同的，`diff` 命令不会产生输出。

`diff` 命令可以以多种格式返回文件之间的差异；这里不带选项使用 `diff`：

```
user@bible:- > cat file
red elephant, red wine
blue mango
redbatross
```

```
user@bible:- > cat file2
red elephant, pink wine
green plums
blue mango
redbatross
```

```
user@bible:- > diff file2
1,2
< elephant, red wine
---
> red elephant, pink wine
> green plums
```

如果你将此输出重定向到文件，它可以作为 `patch` 命令的输入。

```
user@bible:- > diff file2 > diff12
```

我们只是将这两个文件之间的差异的记录（`diff` 命令的输出）写入一个文件。该文件配合 `file`，可以作为 `patch` 命令的输入，`patch` 将差异应用到文件。文件 `file` 将变得与 `file2` 一致。

```
user@bible:- > patch file1 diff12
patching file file1
```

```
user@bible:- > cat file1
red elephant, pink wine
green plums
blue mango
redbatross
```

如果你修复了 `file1`，它现在与 `file2` 一致。

如果你尝试反过来 `patch`，`patch` 会检测到这一点并尝试反向补丁：

```
user@bible:- > patch file2 diff12
patching file file2 (or previously applied) patch detected! Assume -R ? [n]
```

如果你输入 `y`，你将会发现 `file2` 现在与原始文件一致。

如果你在使用 `diff` 时使用了 `-c` 或 `-u` 选项，你可以更容易地应用补丁，因为创建 `diff` 文件的信息包含在其中。因此只需运行 `patch` 并以 `diff12` 作为输入。`patch` 可以从这个作为两个文件之间的 `diff` 创建的文件内容看出，因此它可以轻松地决定如何正确操作。

```
user@bible:- > diff -c file2 > diff12
user@bible:- > patch < diff12
```

# 第10章 文本处理

补丁文件 `file`

现在文件与原始文件2 完全相同。

`diff` 和 `patch` 命令也可以在目录级别上使用（并且通常是这样使用的）。如果你有一个包含大量源文件的目录，以及该目录的更新版本，可以使用 `diff` 命令将两个目录之间的所有差异合并成单个文件，该文件可以作为一个脚本应用。

`diff` 和 `patch` 命令是所有修订控制和版本控制系统的基础，对程序员来说具有巨大的意义。内核源文件的更改通常以 `diff` 形式分发，并使用 `patch` 应用。

在 `www.gnu.org/software/diffutils/manual/` 有一个关于 `diff` 和 `patch` 的说明手册。

# 从其他文件格式提取文本

一个常见的问题是，你收到的文件格式无法轻松读取，因为你没有相应的应用程序。这在二进制文件的情况下尤为令人恼恼，这些文件本打算由特定应用程序读取，但你实际上知道它们包含文本和格式指令。这类问题最常见的情况是你想从 Microsoft Word 文件中提取文本。同样，你可能还想从以 PostScript 或 PDF 格式发送给你的文件中提取文本：你可以在屏幕上显示文件，但并不总是清楚如何提取文本。本节讨论的工具可以帮助解决这一常见问题。

## antiword

典型的 Windows 用户并不知道 Microsoft Word 文件包含什么。它是一个二进制文件，其中夹杂着非常奇怪的文本片段；尝试用类似 `emacs`（或更好的）如 `ghex2` 的十六进制编辑器来查看 `.doc` 文件。此外，它可能包含许多作者并未察觉的内容，例如，她已经删除的内容。很少有人对这一功能感到惊讶，他们可能在无意中分发了 `.doc` 文件，然后面对了他们并不知道其中包含的内容。

从 Linux 用户的角度来看，更重要的是，当人们给你发送 `.doc` 文件时，你并不一定想通过 OpenOffice 或类似的程序打开它们。你可能只是想提取文本。幸运的是，`antiword` 做得非常好。你只需要做的是：

# 第三部分 在 SUSE Linux 中使用命令行

```
antiword filename.doc
```

你将看到文本格式的文件。

`antiword` 软件包不再包含在 SUSE Professional 版本中。你可以从 `www.winfield.demon.nl` 获取。只要你安装了必要的工具，安装就会非常快速和方便：解压存档并运行 `make install`。你可以以没有 root 权限的用户身份安装它；二进制文件将被复制到你的 `-bin` 目录。

## ps2ascii

`ps2ascii` 命令尝试从 PostScript（或 PDF）文件中提取全文本。通常情况下，这种效果非常好，但在输出中换行符所在的地方可能会出现问题，并且（取决于 PostScript 文件是如何创建的）可能会出现一些无法识别的字符。例如：

```
user@ascii:- ~ ps2ascii filename.ps
```

将把结果写入标准输出，

```
user@ascii:- ~ ps2ascii filename.ps outfile.txt
```

将输出输出写入文件。

## ps2pdf

如果你想将 PostScript 文件转换为 PDF 格式，以便使用 Windows 的人们方便查看，`ps2pdf file.ps` 就是你所需要的。该命令会创建一个名为 `file.pdf` 的 PDF 版本。

## dvi2tty

DVI（设备无关）文件由 TeX 和 LaTeX 排版系统（在下一节中解释）产生，然后可以使用适当的驱动程序打印到输出设备。在 Linux 上，最典型的是使用 `dvips` 命令转换为 PostScript 然后直接打印。DVI 文件可以使用如 `kdvi` 等程序直接查看。

你可以使用 `dvi2tty` 命令从 DVI 文件中提取文本。适用于为 `ps2ascii` 提到的类似注意事项：你得到的文本可能与输入的文本并不完全一致。如下所示命令：

# 第10章 文本处理
