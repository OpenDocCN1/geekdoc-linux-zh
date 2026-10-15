
# 编写和执行 Shell 脚本

shell 程序不需要比 shell 任何额外的库支持，或者使用系统中安装的命令。创建和测试 shell 脚本的过程通常比相应 C 语言命令的开发过程更简单更快速。

![](img/757e95bd85c59465935194247625328c_352_0.png)

Ubuntu 包含的数百个命令实际上都是 shell 脚本，互联网上还有许多其他 shell 脚本示例——快速搜索即可获得许多来自 Linux 用户和开发者的在线教程和脚本指南。例如，用于从文本控制启动 X Window 会话的 `startx` 命令就是大多数用户每天使用的 shell 脚本。要学习更多关于使用 `bash` 脚本的知识，请参考本章结尾“参考”部分的《Advanced Bash-Scripting Guide》。你还会发现《Sams Teach Yourself Shell Programming in 24 Hours》是一本学习 shell 并构建你自己的命令的有用指南。

当你学习编写和执行第一个 shell 脚本时，从简单但实用的任务脚本开始。从短小的示例开始，随着你经验和知识的增长不断扩展脚本。大量使用注释（以 `#` 符号开头的行）来记录你的脚本。在脚本的每个部分都包含作者声明和脚本概述作为额外帮助，并附上创建日期或版本号。使用 `vi` 等文本编辑器编写 shell 脚本，因为它不会自动换行。自动换行可能会破坏 shell 语法并导致问题。如果你使用 `nano` 编辑器，请包含 `-w` 标志来禁用换行。

在本节中，你将学习编写一个简单的脚本，在每次登录时设置一些别名（命令同义词）。不需要每次登录都输入所有别名，可以使用文本编辑器（如 `vi`）将它们放在一个文件中，然后执行该文件。

通常这些更改保存在 `/etc` 目录下的系统级 shell 配置文件中以对所有用户生效，或者存在家目录下的 `.bashrc`、`.zshrc`（如果你使用它们）或 `.bash_profile` 文件中。

以下是 `myenv` 的内容，为此目的创建的示例 shell 脚本（针对 `bash`）：

```bash
#!/bin/sh
alias ll='ls -l'
alias dir='ls -aF'
alias copy='cp'
```

这个简单的脚本为 `ls` 和 `cp` 命令创建了别名或快捷快捷形式。`ll` 别名提供长目录列表：`dir` 别名是 `ls` 命令，但它会在列表中打印指示（针对目录或可执行文件）。`copy` 别名与 `cp` 命令相同。你可以尝试并添加自己的选项，或为你经常使用的其他命令创建别名。

你可以在 Linux 下以多种方式执行 `myenv`。如示例所示，你可以使用 `chmod` 命令使 `myenv` 可执行，然后像执行任何原生 Linux 命令一样执行它：

```bash
$ chmod +x myenv
```

此行开启了 `myenv` 的执行权限，可以使用 `ls -l` 选项对其进行检查：

```bash
$ ls -l myenv
-rwxrxrxr-x 1 winky winky 11 Aug 26 17:38 myenv
```

## 运行新的 Shell 程序

你可以通过多种方式运行新的 shell 程序。每种方法都会产生相同的结果，这证明了在 Linux 中使用 shell 的灵活性。运行新 shell 程序的一种方法是从命令行执行文件 `myenv`，就像它是 Linux 命令一样：

```bash
$ ./myenv
```

在特定 shell（如 `pdsh`）下执行 `myenv` 的另一种方法如下：

```bash
$ pdsh myenv
```

这会调用一个新的 `pdsh` shell并将文件名 `myenv` 作为参数来执行该文件。第三种方法要求你在家目录下创建一个名为 `bin` 的目录，然后将新的 shell 程序复制到该目录中。你无需指定特定位置或使用 shell 即可运行程序。操作如下：

```bash
$ mkdir bin
$ mv myenv bin
$ myenv
```

这之所以有效是因为 Ubuntu 默认将执行路径 `$HOME/bin` 包含在你的 shell 环境中。你可以通过将 `env` 命令的输出通过给 `fgrep` 来查看名为 `PATH` 的环境变量：

```bash
$ env | fgrep PATH
/usr/kerberos/bin:/usr/local/bin:/bin:/usr/bin:/usr/X11R6/bin:/sbin
```
