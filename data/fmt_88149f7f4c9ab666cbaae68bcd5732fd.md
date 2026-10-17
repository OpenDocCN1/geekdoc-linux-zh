
Debian `dash` shell 有着有趣的历史。它是 Unix 系统上原始 Bourne shell 的简单拷贝（见第 1 章）。Kenneth Almquist 为 Unix 系统创建了一个小型的 Bourne shell 版本并将其命名为 Almquist shell，后来简写为 `ash`。这个原始 `ash` shell 版本极其精小且运行快速，但缺少许多高级功能，例如命令行编辑或历史记录，使其作为交互式 shell 使用非常困难。

NetBSD 操作系统采纳了 `ash` shell，并一直将其作为默认 shell。NetBSD 开发者通过添加新功能来定制 `ash` shell，使其更接近 Bourne shell，并添加了可以使用 `emacs` 和 `vi` 编辑器命令的历史命令。这个版本的 `ash` 也被 FreeBSD 操作系统作为默认 shell 使用。

# 第三部分：高级 Shell 脚本

基于 Debian 的 Linux 发行版使用 `bash` shell 作为默认登录 shell，并仅将 `dash` shell 用作安装脚本的快速启动 shell，用于安装发行版文件。

例外是流行的 Ubuntu 发行版。这经常让 shell 程序员感到困惑，并导致在 Linux 环境下运行 shell 脚本时出现大量问题。Ubuntu Linux 发行版使用 `bash` shell 作为默认交互式 shell，但使用 `dash` 作为默认的 `/bin/sh` shell。这种“特性”真的让 shell 程序员非常困惑。

正如你在第 11 章中看到的，每个 shell 脚本必须以一行声明脚本所用 shell 的代码开头。在我们的 `bash` 脚本中，我们一直使用：

```bash
#!/bin/bash
```

这告诉用户使用位于 `/bin/bash` 的 shell 程序来执行脚本。在 Unix 世界中，默认 shell 始终是 `/bin/sh`。熟悉 Unix 环境的 shell 脚本程序员会将此复制到他们的 Linux 脚本中：

```bash
#!/bin/sh
```

遗憾的是，Ubuntu Linux 发行版将 `/bin/sh` 文件链接到了 `/bin/dash` shell 程序。因为 `dash` shell 仅包含原始 Bourne shell 可命令的子集，这导致（且经常导致）某些脚本无法正常工作。

下一节将带你了解 `dash` shell 的基础及其与 `bash` shell 的区别。如果你编写可能需要在 Ubuntu 环境下运行的 `bash` 脚本，这一点尤为重要。

# dash Shell 特性

尽管 `bash` shell 和 `dash` shell 都是模仿 Bourne shell 设计的，但它们之间存在差异。本节将带你介绍 Debian `dash` shell 中的功能，以便在深入研究脚本特性之前让你熟悉 `dash` shell 的工作原理。

# dash 命令行参数

`dash` shell 使用命令行参数来控制其行为。表 23-1 列出了命令行参数并描述了每个参数的作用。

## 第 23 章：使用备用 Shell

| 参数 | 描述 |
| -a | --- |
| -a | 导出所有分配给 shell 的变量 |
| -c | 从指定的命令字符串读取命令 |
| -e | 如果不是交互模式，若任何未测试的命令失败，则立即退出 |
| -f | 显示路径通配符字符 |
| -n | 如果不是交互模式，读取命令但不执行 |
| -u | 尝试扩展未设置的变量时，向 `STDERR` 写入错误信息 |
| -V | 在读取时将输入写入 `STDERR` |
| -x | 在执行时将每个字符写入 `STDERR` |
| -I | 在交互模式下忽略输入中的 `EOF` 字符 |
| -i | 强制 shell 在交互模式下运行 |
| -s | 开启作业控制（在没有文件参数存在时是默认行为） |
| -E | 启用 `emacs` 命令行编辑器 |
| -V | 启用 `vi` 命令行编辑器 |

Debian 在原始 shell 命令参数列表中添加了一些额外的命令行参数。`-E` 和 `-V` 命令行参数开启了 `dash` shell 的特殊命令编辑功能。

`-E` 命令参数允许你使用 `emacs` 编辑器命令编辑命令行文本（见第 10 章）。你可以通过 `Ctrl` 和 `Meta` 组合使用所有 `emacs` 命令来处理单行文本。

`-V` 命令参数允许你使用 `vi` 编辑器命令编辑命令行文本。此功能允许你通过 `Esc` 键在命令行的普通模式和 `vi` 编辑器模式之间切换。当你处于编辑器模式时，可以使用所有标准的 `vi` 命令（例如用 `x` 删除字符，用 `i` 插入文本）。完成命令行编辑后，必须再次按 `Esc` 键退出编辑器模式。

# dash 环境变量

`dash` shell 使用了一些默认环境变量来跟踪信息，你也可以创建自己的环境变量。本节描述了这些环境变量以及 `dash` 如何处理它们。

# 默认环境变量

`dash` 环境变量与 `bash` 中使用的环境变量（第 6 章）非常相似。这并非偶然。记住，`dash` 和 `bash` shell 都是 Bourne shell 的扩展，因此它们包含了它的许多特性。然而，由于其目标是简单，`dash` shell 包含的环境变量明显少于 `bash` shell。在 `dash` shell 环境中编写脚本时，你需要考虑到这一点。

`dash` shell 使用 `set` 命令来显示环境变量：

```bash
$set
COLORTERM='default'
DESKTOP_SESSION='default'
DISPLAY='0.0'
DM_CONTROL='/var/run/xdmctl'
```

你可能认识 `bash` shell 中的所有这些内置命令。`dash` shell 支持许多与 `bash` shell 相同的内置命令。你会发现，它没有用于命令历史文件或目录栈的命令。`dash` shell 不支持这些功能。

## 在 dash 中编写脚本

遗憾的是，`dash` shell 并不识别 `bash` shell 的所有脚本功能。为 `bash` 环境编写的 shell 脚本在 `dash` shell 中运行时往往会失败，这给 shell 脚本程序员带来了许多各种困扰。本节描述了为了让你的 shell 脚本在 `dash` shell 环境中正常运行，你需要注意的差异。

## 创建 dash 脚本

你现在可能已经猜到，为 `dash` shell 创建 shell 脚本与为 `bash` shell 创建脚本非常相似。你应该始终在脚本中指定想要使用的 shell，以确保脚本在正确的 shell 中运行。

你可以在 shell 的第一行进行操作：

```bash
#!/bin/dash
```

你也可以在这一行指定 shell 命令行参数，正如之前在“命令行参数”章节中说明的那样。

## 不不起作用

遗憾的是，由于 `dash` shell 只是 Bourne shell 特性的子集，`bash` shell 中的某些功能在 `dash` shell 中无法工作。这些通常被称为 `bashisms`（`bash` 特）。本节简要总结了你可能在 shell 脚本中使用、但在 `dash` shell 环境下无法使用的 `bash` shell 特性。

## 使用算术

第 11 章展示了在 `bash` shell 脚本中表示数学运算的三种方法：

- 使用 `expr` 命令：`expr operation`
- 使用方括号括号：`$(( ))`
- 使用双括号：`$(( ))`

`dash` shell 支持 `expr` 命令和双括号方法，不支持方括号方法。如果你有大量使用方括号的数学运算，可能会导致问题。

# 第三部分：高级 Shell 脚本

```bash
$ cat test5b
#!/bin/dash
# testing mathematical operations

value1=10
value2=15

value3=$((value1 * $value2))
echo "The answer is $value3"
$ ./test5b
The answer is 150 $
```

现在 shell 就可以正常执行计算了。

## test 命令

尽管 `dash` shell 支持 `test` 命令，但你必须小心使用它。`bash` shell 版本的 `test` 命令与 `dash` shell 版本略有不同。

`bash` shell `test` 命令允许你使用双等号 (`==`) 来测试两个字符串是否相等。这是为了适应熟悉其他编程语言中这种格式的程序员而提供的扩展。

然而，`dash` shell 中的 `test` 命令不识别用于文本比较的 `==` 符号。相反，它只识别你 `bash` 脚本中的 `=` 符号，你需要将文本比较改为单等号：
