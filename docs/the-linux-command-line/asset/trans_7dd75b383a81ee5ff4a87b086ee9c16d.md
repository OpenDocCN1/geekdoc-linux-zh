

## 一点背景

vi 的第一个版本由比尔·乔伊（Bill Joy）于 1976 年编写，他是加州大学伯克利分校的学生，后来联合创立了 Sun Microsystems。vi 的名字来源于单词“visual”，因为它旨在允许在带有移动光标的视频终端上进行编辑。在可视化编辑器之前，有行编辑器，一次只对单行文本进行操作。要指定更改，我们告诉行编辑器转到特定行并描述要进行的更改，例如添加或删除文本。随着视频终端（而不是像电传打字机那样基于打印机的终端）的出现，可视化编辑成为可能。vi 实际上包含了一个称为 ex 的强大行编辑器，我们可以在使用 vi 时使用行编辑命令。

大多数 Linux 发行版并不包含真正的 vi；相反，它们附带了一个被称为 vim（“vi improved”的缩写）的增强替代品，由布拉姆·莫勒纳尔（Bram Moolenaar）编写。vim 是传统 Unix vi 的重大改进，在 Linux 系统上通常以符号链接（或别名）的方式命名为“vi”。在接下来的讨论中，我们将假设我们有一个实际是 vim 的名为“vi”的程序。

## 启动和停止 vi

要启动 vi，我们只需输入以下内容：

```
[me@linuxbox ~]$ vi
```

然后应该会出现这样的屏幕：

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
- -         type  :help sponsor<Enter>      for information
- -         type  :q<Enter>                 to exit
- -         type  :help<Enter>  or  <F1>    for on-line help
- -         type  :help version?<Enter>     for version info
- -
-                     Running in Vi compatible mode
- -         type  :set nocompatible<Enter>  for Vim defaults
```

```
~       type :help cp-default<Enter> for info on this
~       
~       
~       
~
```

就像我们之前使用 nano 一样，首先要学习的是如何退出。要退出，我们输入以下命令（注意冒号字符是命令的一部分）：

```
:q
```

应该会返回到 shell 提示符。如果由于某种原因 vi 无法退出（通常是因为我们修改了尚未保存的文件），我们可以通过在命令中添加感叹号来告诉 vi 我们确实要退出：

```
:q!
```

提示：如果你在 vi 中“迷路”了，试着按两次 Esc 键来找到方向。

## 兼容模式

在上面的示例启动画面中（取自 Ubuntu 8.04），我们看到“Running in Vi compatible mode.”（以 Vi 兼容模式运行）的文字。这意味着 vim 将以更接近 vi 正常行为而不是 vim 增强行为的模式运行。就本章而言，我们希望以增强行为运行 vim。为此，你有几个选项：

- 尝试运行 vim 而不是 vi。
- 如果可行，考虑在 .bashrc 文件中添加 alias vi='vim'。
- 或者，使用以下命令向 vim 配置文件添加一行：

```
echo "set nocp" >> ~/.vimrc
```

不同的 Linux 发行版以不同方式打包 vim。有些发行版默认安装最小版本的 vim，只支持有限的一组

vim 功能。在执行后续课程时，你可能会遇到缺少功能的情况。如果是这种情况，请安装完整版的 vim。

## 编辑模式

让我们再次启动 vi，这次向它传递一个不存在的文件名。这是用 vi 创建新文件的方法：

```
[me@linuxbox ~]$ rm -f foo.txt
[me@linuxbox ~]$ vi foo.txt
```

如果一切顺利，我们应该会看到这样的屏幕：

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
"foo.txt" [New File]
```

开头的波浪号字符（"~"）表示该行没有文本。这表示我们有一个空文件。现在什么都不要输入！

关于 vi 需要学习的第二重要的事情（在学会退出之后）是 vi

