

使用分号分隔命令，可以在一行命令中运行多个命令：

```
$ w ; free ; df
6:02pm up 4 days, 24 min, 1 user, load average: 0.00, 0.00, 0.00
USER TTY FROM LOGIN@ IDLE JCPU PCPU WHAT
bball pts/0 shuttle.home.org 1:14pm 0.00s 0.57s 0.01s w
total used free shared buffers cached
Mem: 190684 184420 6264 76 17620 142820
-/+ buffers/cache: 23980 166704
Swap: 1277156 2516 1274640
Filesystem 1k-blocks Used Available Use% Mounted on
/dev/hda1 11780296 4478228 6711248 41% /
none 95340 0 95340 0% /dev/shm
```

此示例显示了 w、free 和 df 命令的输出。长 shell 命令行可以通过使用反斜杠字符（\\）在 shell 脚本中或在命令行中进行扩展。例如，

```
$ echo "this is a long \
> command line and" ; echo "shows that multiple commands \
> may be strung out."
this is a long command line and
shows that multiple commands may be strung out.
```

此示例的前三行是一个单一的命令行。在该单行中包含两个 echo 命令。注意，当你使用反斜杠作为续行字符时，它必须是命令行上的最后一个字符（或在你的 shell 脚本中，如本章后面将看到的那样）。

使用 shell 命令行基本功能很容易，但掌握所有功能可能很困难。整本书都专门用于使用 shell、编写 shell 脚本以及使用模式匹配表达式。以下各节提供了 shell 命令行与编写脚本相关的一些功能的概述。

## 掌握 grep

如果你计划开发 shell 脚本来扩展 grep 等模式匹配命令的功能，那么你将受益于学习更多关于使用表达式的知识。关于使用 Unix 和 Linux 命令的模式匹配功能的最权威指南之一是 Jeffrey E. F. Friedl 所著的 Mastering Regular Expressions（O'Reilly），ISBN：0-596-52812-4。

## Shell 模式匹配支持

shell 命令行允许你使用专门构造的字符模式字符串进行通配符匹配。这是一种与 GNU 实用程序如 grep 支持的不同且更简单的功能，后者可以使用更复杂的模式，即表达式，来搜索文件或目录，或过滤输入到命令或从命令输出的数据。

shell 的模式字符串可以简单或复杂，但即使只使用可用字符中一小部分进行简单的通配符，也可以在命令行上获得有建设性的结果。一些常用的 shell 模式匹配字符是

- `*`—匹配任意字符。例如，要查找当前目录下以 `.txt` 结尾的所有文件，你可以使用：

  ```shell
  $ ls *.txt
  ```

- `?`—匹配单个字符。例如，要查找当前目录下以扩展名 `.d?c` 结尾的所有文件（其中 ? 可以是 0–9、a–z 或 A–Z）：

  ```shell
  $ ls *.d?c
  ```

- `[xxx]` 或 `[x-x]`—匹配一组字符的范围。例如，要列出目录中名称包含数字的所有文件，

  ```shell
  $ ls *[0-9]*
  ```

- `\x`—匹配或转义字符，例如 `?` 或制表符。例如，要创建一个名称包含问号的文件，

  ```shell
  $ touch foo\?
  ```

请注意，shell 可能不会以与 Linux 命令相同的方式解释某些字符或正则表达式，并且在 shell 脚本中混合使用通配符和正则表达式如果不小心可能会导致问题。例如，查找文本中的模式最好留给与 grep 等命令一起使用的正则表达式；简单的通配符应用于在命令行上过滤或匹配文件名。并且虽然 Linux 命令表达式和 shell 脚本都可以识别反斜杠作为模式中的转义字符，但美元符号 ($) 将具有两种截然不同的含义（表达式中的单字符模式匹配和脚本中的变量赋值）。

> **CAUTION**
>
> 使用通配符时请务必仔细阅读你的命令；一个过于常见的错误是输入类似 `rm -rf * .txt` 的内容，`*` 和 `.txt` 之间有一个空格。到你怀疑命令为什么花费这么长时间时，Bash 已经删除了你大部分文件。问题在于它会将 `*` 和 `.txt` 分开处理。`*` 将匹配所有内容，因此 Bash 将删除你的所有文件。

