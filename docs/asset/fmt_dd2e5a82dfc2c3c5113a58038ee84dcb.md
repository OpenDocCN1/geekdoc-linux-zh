
你可以通过设置 `PS1` 变量的值来更改默认提示符，它包含显示在提示符中的信息的占位符，包括：

- `\u` 当前用户名
- `\h` 当前工作的主机名

如果你恰好在多个系统上有 shell 或登录了多个账户，这非常有用。通过使用 `\u` 和 `\h` 值，你可以一眼看出是谁以及你的系统是什么。

让我们玩点花并更改终端中的提示符。例如，你可以输入以下：

```bash
kali> PS1="World's Best Hacker: #"
World's Best Hacker: #
```

现在，每当你使用这个终端时，都会提醒你你是顶级黑客。但你打开的任何后续终端仍然具有默认命令提示符，因为 `PS1` 变量对对终端会话有效。如果你真的喜欢这个新命令提示符并想继续使用它，你需要导出它，如下：

```bash
kali> export PS1
```

再趣一点？假设你真的想让终端看起来像 Windows cmd 提示符。在这种情况下，你可以将提示符名称改为 `C:` 并保留 `\w` 让提示符显示你的当前目录，如列表 7-2 所示。

```bash
kali> export PS1='C:\w'
C:/tmp
```

列表 7-2：更改提示符中的目录对于初学者来说特别有用，所以当你更改 `PS1` 变量时，需要考虑这一点。

# 修改你的 PATH

环境变量中最最重要的变量之一就是 `PATH` 变量，它控制了 shell 在系统的何种位置查找你输入的命令，如 `grep`、`ls` 和 `echo`。大多数命令位于 `sbin` 或 `bin` 子目录下，例如 `/usr/local/sbin` 或 `/usr/local/bin`。如果 bash shell 在你变量中的某个目录中没有找到该命令，它将返回错误 `command not found`，即使该命令存在于你未包含的目录中。

你可以通过对 `PATH` 内容使用 `echo` 命令来查看其中存储了哪些目录，因此：

```bash
kali> echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/bin:/sbin:/bin
```

你的终端将在在此列出的目录中搜索所有命令。例如，当你输入 `ls` 时，系统将知道在这些目录中查找它，然后执行它。

每个目录之间用冒号（`:`）隔开。不要忘记在 `PATH` 中添加 `$` 内容符号。当我们在变量前加上 `$` 时，我们是在请求该变量的内容。

# 向 PATH 变量添加内容

你可能已经知道了解 `PATH` 变量中的内容有多重要：如果你下载并安装了一个新工具（例如，新目录 `newhackingtool`），你只有在进入该目录时才能使用该工具的命令，因为该目录不在 `PATH` 变量中。每当你想要使用该工具时，都必须先导航到 `/root/newhackingtool`，如果你经常使用该工具，这会非常不方便。

为了能够在任何目录下使用此工具，你需要将存放此工具的目录添加到 `PATH` 变量中。要将 `newhackingtool` 添加到你的 `PATH` 变量，请输入：

```bash
kali> PATH=$PATH:/root/newhackingtool
```

这会将原始 `PATH` 加上 `/root/newhackingtool` 目录赋值给新的 `PATH` 变量，因此该变量包含了之前的所有内容，加上新的工具目录。

如果你再次检查 `PATH` 变量的内容，你应该能看到目录已追加到 `PATH` 的末尾，如下所示：

```bash
kali> echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/bin:/bin:/root/newhackingtool
```

现在你可以在系统的任何地方执行 `newhackingtool` 程序，而无需导航到它的目录。bash shell 将在列出的所有目录中查找你的新工具。

将经常使用的目录添加到 `PATH` 是一种实用的技术，但要小心不要向 `PATH` 变量中添加多的目录。因为系统必须搜索 `PATH` 中的每一个目录来查找命令，添加大量目录可能会降低终端速度。

# 如何错误添加 PATH 变量

新 Linux 用户常犯的一个错误是按这种方式将新目录（如 `/root/newhackingtool`）直接赋值给 `PATH` 变量：

```bash
kali> PATH=/root/newhackingtool
kali> echo $PATH
/root/newhackingtool
```

如果你使用此命令，你的 `PATH` 变量将只包含 `/root/newhackingtool` 目录，不再包含包含 `/bin`、`/sbin` 等其他存放关键命令的系统二进制文件。当你尝试使用任何系统命令时，将收到 `command not found` 错误，如下所示，除非你在执行命令时先导航到系统二进制文件目录：

```bash
kali> ls
bash: ls: command not found
```

记住，你想向 `PATH` 变量**追加**（append）内容，而不是替换它。如果你不确定，请在修改之前先将变量的内容保存到某处。

# 创建自定义变量

在 Linux 中，你只需为你命名的新变量赋值即可创建自己的自定义用户定义变量。当你进行一些高级的 shell 脚本编写或发现自己厌了反复输入某个长命令时，这可能有用。

语法非常简单：输入变量名、不带空格的赋值符号（`=`）以及要放入变量中的值，如下：

```bash
kali> MYNEWVARIABLE='Hacking is the most valuable skill set in the 21st century'
```

这会将字符串赋值给变量 `MYNEWVARIABLE`。要查看该变量中的值，使用 `echo` 命令和变量名的 `$` 符号，正如我们之前做的那样：

```bash
kali> echo $MYNEWVARIABLE
Hacking is the most valuable skill set in the 21st century
```

就像环境变量一样，用户定义变量必须导出（`export`）才能在新的会话中持续。

如果你想删除这个新变量或任何变量，请使用 `unset` 命令。但在删除系统变量之前务必深思，因为之后系统的运行可能会大不相同。

```bash
kali> unset MYNEWVARIABLE
kali> echo $MYNEWVARIABLE
kali>
```

如你所见，当你输入 `unset MYNEWVARIABLE` 时，你删除了变量及其值。如果你对同一个变量使用 `echo`，Linux 现在将返回一个空行。

## 总结

你可能觉得环境变量很陌生，但它们值得了解。它们控制着你在 Linux 中工作环境的外观、行为和感受。你可以通过更改、导出甚至创建自己的变量来管理这些变量，以量身定制环境。在某些情况下，它们可能对于作为黑客隐藏踪迹有用。

# 练习

- 1. 使用 `more` 命令查看所有的环境变量。
- 2. 使用 `echo` 命令查看 `HOSTNAME` 变量。
- 3. 找到一种将斜杠 (`/`) 更改为反斜杠 (`\`) 方法。
- 4. 创建名为 `MYNEWVARIABLE` 的变量并输入你的名字。
- 5. 使用 `echo` 查看 `MYNEWVARIABLE`。
- 6. 导出 `MYNEWVARIABLE` 使在所有环境中可用。
- 7. 使用 `echo` 查看 `PATH` 的内容。
- 8. 将你的主目录添加到 `PATH` 变量中。

# Bash 快速入门

## BASH 脚本

任何自重的黑客都必须学会脚本。黑客经常需要自动化命令，有时涉及多个工具，这通过他们编写的短程序可以高效实现。在，*shell* 是用户与操作系统之间的接口，允许你操作文件并运行命令、实用程序等。shell 的优势在于你可以直接从计算机执行这些任务，而不是通过抽象（如 GUI），后者允许你根据需要自定义任务。正如第 7 章提到的，Linux 有许多不同的 shell，包括 Korn shell、Z shell 和 Bourne Again shell（通常称为 bash）。

最近，Kali Linux 的开发者已将默认 shell 从 bash 更改为 Z。虽然 Z shell 没有问题（macOS 也发生了变化），由于 Linux 和 Unix 发行版（Red Hat、Ubuntu 等）仍在使用 bash shell，我认为我们也应该。幸运的是，Kali Linux 的开发者可以通过 `kali-tweaks` 命令轻松地切换回 bash。

只需输入此命令

```
kali> kali-tweaks
```
