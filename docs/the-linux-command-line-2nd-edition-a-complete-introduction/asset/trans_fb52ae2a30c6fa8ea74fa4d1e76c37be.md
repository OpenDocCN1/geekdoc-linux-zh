

## 一点背景

vi 的第一个版本由比尔·乔伊（Bill Joy）于1976年编写，他当时是加州大学伯克利分校的学生，后来共同创立了 Sun Microsystems。vi 得名于“visual”一词，因为它旨在允许在具有移动光标的视频终端上进行编辑。在可视化编辑器之前，存在行编辑器，它们一次只操作一行文本。要指定更改，我们会告诉行编辑器转到特定行并描述要进行的更改，例如添加或删除文本。随着视频终端（而非打印机式终端如电传打字机）的出现，可视化编辑成为可能。vi 实际上包含了一个功能强大的行编辑器 ex，我们在使用 vi 时可以使用行编辑命令。

大多数 Linux 发行版并不包含真正的 vi；相反，它们提供了一个增强的替代品 vim（是“vi improved”的缩写），由 Bram Moolenaar 编写。vim 相较于传统的 Unix vi 有了实质性的改进，并且通常在 Linux 系统上符号链接（或别名）为“vi”。在下面的讨论中，我们将假设我们有一个名为“vi”的程序，实际上是 vim。

## 启动和退出 vi

要启动 vi，我们只需输入以下命令：

```
[me@linuxbox ~]$ vi
```

并且应该会出现如下屏幕：

```
- -
- -
-                 VIM - Vi Improved
- -
-                     version 7.1.138
-                     by Bram Moolenaar et al.
-                 Vim is open source and freely distributable
- -
-                     Sponsor Vim development!
-                 type :help sponsor<Enter>      for information
- -
-                 type :q<Enter>                 to exit
-                 type :help<Enter>  or  <F1>    for on-line help
-                 type :help version?<Enter>     for version info
- -
-                     Running in Vi compatible mode
-                 type :set nocompatible<Enter>  for Vim defaults
```

```
~       type :help cp-default<Enter> for info on this
~       
~       
~       
~       
```

正如我们之前使用 nano 时一样，首先要学习的是如何退出。要退出，我们输入以下命令（请注意冒号字符是命令的一部分）：

```
:q
```

shell 提示符应该返回。如果由于某种原因 vi 无法退出（通常是因为我们对尚未保存的文件进行了更改），我们可以告诉 vi 我们是认真的，通过在命令后加上感叹号：

```
:q!
```

提示：如果你在 vi 中“迷路”了，尝试按两次 Esc 键来重新找回方向。

## 兼容模式

在上面的示例启动屏幕中（取自 Ubuntu 8.04），我们看到文字“Running in Vi compatible mode”。这意味着 vim 将以更接近 vi 的正常行为而不是 vim 的增强行为的模式运行。为了本章的目的，我们希望以增强行为运行 vim。为此，你有几个选择：
- 尝试运行 vim 而不是 vi。
- 如果可行，考虑在你的 .bashrc 文件中添加 alias vi='vim'。
- 或者，使用以下命令向你的 vim 配置文件添加一行：
echo "set nocompatible" >> ~/.vimrc
不同的 Linux 发行版以不同的方式打包 vim。一些发行版默认安装仅支持有限 vim 功能的最小版本 vim。在进行以下练习时，你可能会遇到缺少的功能。如果是这种情况，请安装完整的 vim 版本。

## 编辑模式

让我们再次启动 vi，这次传递一个不存在的文件名作为参数。这就是我们如何使用 vi 创建新文件的方式：

```
[me@linuxbox ~]$ rm -f foo.txt
[me@linuxbox ~]$ vi foo.txt
```

如果一切顺利，我们应该得到如下屏幕：

```
~
~
~
~
~
~
~
~
~
~
~
~
~
~
~
~
"foo.txt" [New File]
```

前导波浪号字符（"~"）表示该行上没有文本。这表明我们有一个空文件。暂时不要输入任何内容！

关于 vi 的第二件最重要的事情要学习（在学习如何退出之后）是 vi 是一个模式编辑器。vi 启动时开始于命令模式。在此模式下，几乎每个键都是一个命令，因此如果我们开始输入，vi 基本上会发疯并制造一团混乱。

