

## 第 14 章 交互式与非标准 shell 特性

事实，所有主要的交互式 shell 都允许你指定哪个 shell——实际上是 Unix 或 Linux 发行版包含的数千个程序之一——来运行文件。如果文件的第一行两个字符是 #$`，该行的剩余部分将指定该文件的解释器。因此：

```bash
#!/bin/ksh
```

指定 Korn shell，而

```bash
#!/bin/bash
```

指定 Bash。如果你使用了某个特定 shell 的结构或符号约定，可以使用此特性强制该 shell 运行你的程序，从而避免兼容性问题。

由于你可以指定任何所需的程序，一个开头为

```bash
#!/usr/bin/perl
```

的 Perl 程序将强制 shell 调用 `/usr/bin/perl` 来解释文件中的行。

你必须谨慎地使用此特性，因为许多程序（如 Perl）并不存在于每个 Unix 系统的标准位置。此外，这并没有被 POSIX 标准规定，尽管在每个现代 shell 中都能找到，并且在许多 Unix 版本中甚至在操作系统层面实现。

最常见的是，你会看到系统程序使用这种符号来确保无论用户的登录 shell 是什么，都使用 Bourne Shell，其开头为：

```bash
#!/bin/sh
```

### ENV 文件

当你启动 shell 时，它做的第一件事是在你的环境中查找名为 `ENV` 的变量。如果找到且不为空，则执行 ENV 文件，就像登录时执行 `.profile` 一样。ENV 文件包含了设置 shell 环境的命令。在本章中我们将提到许多可能想要放入此文件的内容。

如果你决定拥有一个 ENV 文件，你应该在自己的 `.profile` 文件中设置并导出 `ENV` 变量：

```bash
$ cat .profile

export ENV=$HOME/.alias
... own$
```

注意上面的快捷写法：与其先给变量赋值再调用 `export`，实际上你可以在同一行内完成这两个操作以提高效率。

## 命令行编辑

对于用户来说，只有当以 `sh` 名称调用 Bash、使用 `--posix` 命令行选项，或者在执行 `set -o posix` 之后，才会读取 ENV 文件（这些都是为了强制遵守 POSIX 标准）。默认情况下，当启动非交互式 Bash shell 时（例如，运行一个 shell 程序时），它会从 `BASH_ENV` 环境变量指定的文件读取命令；当启动交互式 Bash shell 时（例如，在命令提示符输入 `bash`），则不会读取。

如果你运行的是旧版系统，还应该在 `.profile` 文件中导出 `SHELL` 变量。

```bash
$ SHELL .profile
SHELL=/bin/ksh ; export SHELL
$
```

该变量被某些应用程序（如 `vi`）用于在执行 shell 转义时确定启动什么 shell。在这种情况下，你希望确保每次启动新 shell 时，启动的是你想要的 shell 而不是 Bourne。可能 `SHELL` 已经由你的登录 shell 设置好了。你可以通过以下命令测试：

```bash
$ echo SHELL
/bin/bash
$
```

另外注意，之前的示例演示了另一种设置和导出变量的方法，即在同一行上使用两个独立的命令，并用分号隔开。为什么不一致？因为 Unix 是如此灵活，你会发现你阅读的 shell 程序——以及你合作的用户——经常以多种方式完成相同的任务。何不尝试这些符号变化的变体呢！

行编辑模式是 shell 的一项功能，允许你以模拟两种流行的编辑器功能的方式来编辑命令行。POSIX 标准提供了模拟 `vi` 的能力，而 Bash 和 Korn shell 都支持 emacs 行编辑模式。我们在附录 A 的表 A.4 中列出了完整的命令集。

如果你用过这些基于文本的编辑器，你会发现 shell 内置的编辑器在功能角度上是忠实的复制。这种能力是 shell 中最实用的功能之一。

使用 `set` 命令配合 `-o` 模式开启行编辑，其中模式可以是 `vi` 或 `emacs`：

```bash
$ set -o vi
Turn on vi mode
```

将此放入你的 `.profile` 文件中，以便自动开启一种编辑模式启动 shell。

## 命令历史

无论你使用哪种 shell，它都会保留你之前输入的所有命令的历史。每当你按下回车键执行命令时，该命令就会添加到历史末尾。

根据你的设置，你的命令历史甚至可以保存到文件中并在会话之间恢复，这样你可以快速访问之前会话的命令。

默认情况下，历史保存在家目录下名为 `.sh_history` (Bash) 的文件中。你可以通过设置 `HISTORYFILE` 变量将此文件名改为任何你。该变量可以在 `.profile` 中设置并导出。

shell 存储的命令数量有一个限制。最小值为 128，大多数现代 shell 在列表中使用 500 个或更多命令。每次登录时，shell 都会将你的历史文件截断到该长度。

你可以通过设置 `HISTSIZE` 变量来控制历史文件的大小。如果默认值不能满足你的需求，将 `HISTSIZE` 设置为较大的值，例如 500 或 1000。分配给 `HISTSIZE` 的值可以在 `.profile` 文件中设置并导出：

```bash
$ HISTSIZE .profile
HISTSIZE=500
$
```

当光标后是你想要更改的字符时，你可以使用 `x` 命令删除当前字符（将其“X”掉）。注意，当删除 `x` 时，光标向左移动了，它现在是当前字符。

要向命令行添加内容，你可以使用 `i` 前或 `a` 命令。`i` 命令在当前字符之前插入，`a` 命令在当前字符之后添加。这两个命令都会让你回到输入模式，记得按 `Esc` 回到命令模式。

```bash
$ mary had a little lab im $ mary had a little lamb
$ mary had a little lamb m $ mary had a little lambm
$ mary had a little lambb Esc $ mary had a little lammb
$ mary had a little lambb x $ mary had a little lamb
$ mary had a little lamb a $ mary had a little lamb_
$ mary had a little lamb_ da $ mary had a little lambda_
```

