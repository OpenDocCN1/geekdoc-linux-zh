
| | ---M--M-- | ---M--M-- |

当权限被掩码后，你最终在新文件和目录上获得以下权限：

| 最大 | 对于文件 | 对于目录 |
| --- | --- | --- |
| 掩码 | rw-rw-rw- | rwxrwxr-x |
| 结果 | ---M--M-- | ---M--M-- |
| | rw-r--r-- | rw-r--r-- |

你可以看到，`umask` 改变了文件和目录的默认权限。如果 `umask` 是 `022`，文件的计算结果为 `666 - 022 = 644` (`rw-r--r--`)。

| 最大 | 对于文件 | 对于目录 |
| --- | --- | --- |
| 掩码 | rw-rw-rw- | rwxrwxr-x |
| 结果 | rw-r--r-- | rwxrxr-x |

如所示，`umask` 改变了文件和目录的默认权限。如果 `umask` 是 `022`，文件的计算结果为 `666 - 022 = 644` (`rw-r--r--`)，目录的则为 `777 - 022 = 755` (`drwxr-xr-x`)。

## 修改用户所有权

`chown` 命令用于一次性设置用户所有者、组所有者或两者的组合。`chown` 命令的格式为：

```
chown options user:group object
```

`chown` 命令接受以下两种有效命令（所有者/组的分符可以是 `:` 或 `.`）：

```
chown snuffy:users file1
chown snuffy.users file1
```

此外，你可以使用 `chown` 的以下语法：

- `owner`—仅更改用户所有者
- `owner:group`—同时更改用户所有者和组所有者
- `owner=:`更改用户所有者并将组所有者设置为当前用户的主组
- `:group`—仅更改组所有者，不影响用户所有者

假设用户 `snuffy` 的主组是 `users`，该账户是 `accounting` 组的辅助组成。默认情况下，`snuffy` 创建的每个对象都有 `snuffy` 为用户所有者，`users` 为组所有者。这在共享目录中可能会导致问题。

如果 `snuffy` 访问一个组所有权设置为 `snuffy` 的共享目录并创建一个名为 `snuffyexpenses.txt` 的文件，那么共享该目录的其他用户除非他们也是 `users` 组的成员，否则将无法访问该文件。

假设用户 `martha` 负责费用并需要该文件的所有权，而你作为管理员，想要将该文件的组所有权更改为 `accounting` 。为了完成此任务，请使用此命令：

```
chown martha:accounting snuffyexpenses.txt
```

假设现在该文件的所有权需要属于另一个负责支票的用户 `fluchre`；你可以只更改用户所有者，而无需打扰组所有者：

[点击此处查看代码图像]

```
chown fluchre snuffxyexpenses.txt
```

如果出于某种原因，你决定需要更改整个文件树的所有权，可以使用以下命令更改它们的所有权：

[点击此处查看代码图像]

```
chown -R root:accounting /accounting
```

![](img/16cd7204aa58beaaf530d67f50f15fc5_394_0.png)

重要说明：系统中只有 `root` 用户可以更改对象的用户所有权。即使是文件的所有者也无法将所有权“移交”给另一个用户。然而，只要普通用户是要更改所有权的目标组的成员，他就可以更改对象的组所有权。

## 修改组所有权

![](img/16cd7204aa58beaaf530d67f50f15fc5_394_1.png)

当只需要更改组所有者时，最简单的方法是使用 `chgrp` 命令。该命令的语法非常直观：

```
chgrp staff file1
```

将大量文件更改为另一个组所有者需要使用 `R`（递归）选项：

```
chgrp -R staff /data/*
```

上一个命令将 `/data` 目录的内容（及其所有子目录）的组所有者更改为 `staff`，但保持用户所有者不变。

`chgrp` 命令的选项包括：

- `-c`—仅对更改的对象显示输出行
- `-h`—更改符号链接，而不是原始文件
- `-R`—递归地影响目标及其所有子节点
- `-v`—无论对对象执行了什么操作，都为每个对象显示一行输出

> 注意
>
> 尽管这不属于考试大纲，但在涉及组所有权时，`newgrp` 命令可能非常有用。如果普通用户是 `groupname` 的成员，他可以执行 `newgrp groupname` 命令。这会打开一个新的 shell，其中主组为 `groupname`。这在创建一组需要由次要组拥的文件时非常有用。要关闭这个新 shell，只需执行 `exit` 命令即可。

## 总结

在本章中，你学习了基本权限的概念，包括如何设置权限以及如何指定对象的默认权限。你还学习了特殊权限的工作原理，以及它们对于保护系统安全有多重要。

## 考试准备任务

正如引言中“如何使用本书”节所提到的，你有几种准备考试的选择：此处的练习题、第 21 章“最终准备”以及 DVD 上的模拟考试。

## 复习所有关键主题

复习本章中最重要的主题，这些主题在页外边缘用“关键主题”图标标记。表 10-2 列出了这些关键主题的索引及其所在的页码。

| 关键主题元素 | 描述 | 页码 |
|---|---|---|
| 段落 | 权限三元组 (Permission trio bits) | 292 |
| 段落 | 这些值对应于文件的以下权限 | 293 |
| 段落 | 这些权限对于目录具有相似但略有不同的含义 | 293 |
| 段落 | 数字权限是最常用的 | 294 |
| 段落 | 何时使用 chmod 命令 | 296 |
| 段落 | 特殊位权限 (Special bit permissions) | 298 |
| 段落 | 特殊位仅在必要时使用 | 298 |
| 段落 | SUID 位的一个良好示例 | 299 |
| 段落 | 粘滞位 (Sticky bit) 用 | 302 |
| 段落 | find 命令运算符 | 302 |
| 段落 | 典型 Linux 系统的默认权限 | 303 |
| 段落 | umask 值 | 305 |
| 段落 | chown 命令 | 305 |
| 段落 | 能够更改某些权限的用户 | 306 |
| 段落 | 修改组所有权 | 306 |

表 10-2 第10 章关键主题

## 定义关键术语

定义本章中的以下关键术语，并在词表表中检查你的答案：

- 权限三元组 (permission trios)
- 数字模式 (numeric mode)
- 符号模式 (symbolic mode)
- SGID
- 粘滞位 (sticky bit)
- umask 值

## 复习题

这些复习题的答案在附录 A 中。

- 1. 目录的执行权限提供什么访问？
  - a. 在目录中列出文件名的能力
  - b. 向目录添加文件的能力
  - c. 从目录删除文件的能力
  - d. 进入目录的能力
- 2. 考虑以下 `ls -l` 命令的输出：

```
-rw-rw-r-x  2  users  0 Jan 26 13:08 22  test.mp3
```

以下哪个说法正确？
  - a. 用户对 `test.mp3` 只有读取权限。
  - b. 用户对 `test.mp3` 只有读取和写入权限。
  - c. 用户对 `test.mp3` 具有读取、写入和执行权限。
  - d. 用户对 `test.mp3` 无权限。
- 3. 下列哪项等同于命令：
  - a. `chmod u+r file`
  - b. `chmod u+w file`
  - c. `chmod u+x file`
  - d. `chmod u+s file`
- 4. 下列哪项设置了 SUID 权限？（选择两个）
  - a. `chmod u+s file`
  - b. `chmod +s file`
  - c. `chmod 4755 file`
  - d. `chmod s file`
- 5. 考虑以下命令：

```
umask 077
```

假设执行了此命令，以下哪些是正确的？（选择两个）
  - a. 新创建的文件对组和其他用户没有权限。
  - b. 新创建的文件所有者拥有所有权限。
  - c. 新创建的目录对组和其他用户没有权限。
  - d. 新创建的目录对所有人都有所有权限。
- a. `tzselect`
- b. `TZ=America/Thunder_Bay date`
- c. `LC_TIME=America/Thunder_Bay date`
- d. `--timezone=America/Thunder_Bay`
- 6. 亚太办公室的一位同事发给你一个文件，其中包含如何设置他正在开发的新应用程序的说明。当你在编辑器中查看该文件时，它看起来团乱糟。你对消息运行了 `file` 命令并看到：

点击此处查看代码图像

```
message: Big-endian UTF-16 Unicode text (大端 UTF-16 Unicode 文本)

如何解码这个文件？
a. 不可能解码；同事必须以 ISO-8859 格式发送它。
b. LANGUAGE=en_US.UTF-16 cat message
c. tr -d UTF-16 < message
d. icon -f UTF-16 -t ASCII message
```

## 基础主题

## 在 Shell 中工作

Shell 是文本界面的桌面。Shell 接收你输入的命令，将其发送到操作系统，并将结果显示给你。在此过程中，Shell 实现了诸如通配符匹配（globbing）等功能，它通过通配符匹配文件，使得更短命令更加强大。你还可以向 Shell 添加自己的命令，以进一步减少工作量。

到本书为止，你已经看到了许多 Shell 命令，例如处理文件的命令。在这里你将学习如何自定义 Shell 环境，使你目前所学的内容更加强大。

除非你更改默认设置，否则 Linux Shell 通常是 `bash` shell。当然，还有许多其他 Shell。表 11-2 显示了部分列表。

| ash | Bourne Again Shell | C-shell Korn | T C-shell zsh |
|---|---|---|---|---|---|
| 可执行文件 | ash | bash | csh ksh | tcsh | zsh |
| 作业控制 | N | Y | Y | Y | Y |
| 别名 | N | Y | Y | Y | Y |
| 函数 | Y | Y | N | N | Y |
| 重定向 | Y | Y | Y | Y | Y |
| 历史 | N | Y | Y | Y | Y |
| 补全 | N | Y | Y | Y | Y |
| 编辑 | N | Y | Y | Y | Y |

### **表 11-2** Linux Shell 示例

除了其他信息外，用户的默认 Shell 在该用户的 `/etc/passwd` 条目中进行指定。如果指定的 Shell 不存在，用户将默认获得 `bash` shell。

![](img/16cd7204aa58beaaf530d67f50f15fc5_402_0.png)

可以指定特殊的 Shell，例如 `/bin/false`（它返回非零错误代码，实际上阻止尝试登录的用户访问）或 `/sbin/nologin`（它也会阻止登录，但会给出一个礼貌的消息）。

选择 Shell 是一个个人问题。大多数 Shell 之间通过某种方式相互关联。`bash`（即 Bourne Again Shell）是对 Bourne shell 的改进，而 Bourne shell 本身是对 Unix 原始 Thompson shell 的改进。Korn shell 派自 Bourne，但实现了 C-shell 的一些优秀特性。

本书将描述 `bash` 的用法。这些概念可以应用于所有其他 Shell。

## 环境变量

`变量`是一个存储信息的“桶”。如果你需要存储刚刚启动的那个 Web 服务器的进程 ID（PID），可以将其放入名为 `WEBSERVER_PID` 的变量中，当你下次需要它时它会在那里，如 **示例 11-1** 所示。

### **示例 11-1** 变量示例

```
$ WEBSERVER_PID=29565

$ echo $WEBSERVER_PID
29565
$ ps -ef grep $WEBSERVER_PID      00:04:09 nginx: worker
nginx             14747 29565 0 Apr10 ? 
process
root             29565      1 0 Mar27 ?      00:00:00 nginx: master
```

第一行将值 `29565` 赋值给名为 `WEBSERVER_PID` 的变量。在变量名前前加上美元符号 `$` 告诉 Shell 在该处替换变量的值。前一个示例中的接两个命令使用了该变量：首先通过 `echo` 命令显示，然后使用 `ps` 和 `grep` 查找包含该数字的进程。

记住：赋值时使用变量名本身。使用变量内部的值时在前面加上美元符号。此外，等号周围不能有空格，这也很重要。

变量名可以是大写或小写，并包含字母、数字和下划线 `_`。按照习惯，你在 Shell 中设置任何内容都是大写的。脚本中的变量是小写或混合大小写的。

变量对你可能有意义，也可以对 Shell 有意义。`HOME` 由 Shell 自动设为当前用户的家目录，所以上面的第一个命令是多余的！

如果你在赋值右侧有空格，你需要转义空格或将其用引号括起来。这两个命令的效果相同：

```
$ GREETING="Hello World"
$ GREETING=Hello\ World
```

## 变量范围

环境变量一个令人困惑的属性是：在一个 Shell 中设置它们，仅适用于该 Shell，而不适用于父 Shell、子 Shell或其他 Shell。

![](img/16cd7204aa58beaaf530d67f50f15fc5_402_0.png)

可以指定特殊的 Shell，例如 `/bin/false`（它返回非零错误代码，实际上阻止尝试登录的用户访问）或 `/sbin/nologin`（它也会阻止登录，但会给出一个礼貌的消息）。

选择 Shell 是一个个人问题。大多数 Shell 之间通过某种方式相互关联。`bash`（Bourne Again Shell）是对 Bourne shell 的改进，而 Bourne shell 本身是对 Unix 原始 Thompson shell 的改进。Korn shell 派自 Bourne，但实现了 C-shell 的一些优秀特性。

本书将描述 `bash` 的用法。这些概念可以应用于所有其他 Shell。

*(注：由于文本中存在大量重复段落，译文已根据要求去重并进行高质量翻译)*

变量，用于从命令行或其他函数向脚本传递信息。任何传递给 `set` 且被识别为选项的内容都会分配给这些位置参数之一：

点击此处查看代码图像

```
$ set a b c d e f g h i j k l m
$ echo $1
a
$ echo ${10}
j
```

注意在尝试展开 `$10` 时要使用大括号。如果不使用大括号，shell 会认为你正尝试展开 `$1` 然后追加一个零，因此你最终会得到 `a0`。

### 子壳 (Subshells)

你已经看到过父 shell 和子 shell 如何在环境变量方面进行交互。在某些情况下，你可能想临时使用子壳以确保你拥有一个干净的环境，或者在不改变当前 shell 的情况下临时设置某些变量。

![](img/16cd7204aa58beaaf530d67f50f15fc5_407_0.png)

获取子壳最简单的方法是将命令括在括号中。将示例 11-4 复制到名为 `test.sh` 的文件中并运行它。

# 示例 11-4 用于演示子壳的 脚本

点击此处查看代码图像

```
echo "In parent $BASH_SUBSHELL pid $$"
FOO=bar
echo $FOO
(FOO=baz; echo -n "In subshell $BASH_SUBSHELL "; echo $$)
echo $FOO
```

脚本执行的第一步是在控制台写入一些信息。这两个变量是 Bash 内置的：`$BASH_SUBSHELL` 提供当前的子壳级别，`$$` 提供当前进程的 pid。

之后，脚本设置了变量 `FOO` 并将其打印到屏幕上。

接着是在子壳内部再次运行脚本。`FOO` 被赋予了一个新值，并打印了 `BASH_SUBSHELL` 和 pid 的当前值。子壳可以跨多行，但为了紧凑，命令用分号（`;`）隔开。

最后，脚本打印 `FOO` 的内容。运行该脚本将产生如 [示例 11-5] 所示的输出。

# 示例 11-5 用于演示 BASH_SUBSHELL 层级的脚本

```
$ sh test.sh
In parent 0 pid 11966
bar
In subshell 1 11966
bar
```

`FOO` 的值在[父 shell] 中没有改变，因为它只在子壳中被改变了。此外，子壳并没有产生新进程。

# env 包装器

子壳是一种确保某些工作不会污染你当前环境的方法。有时你希望在一个已知环境中执行工作，这时 `env` 就派上用场了。

你已经通过 `[WORK_FACTOR=3 /my_command]` 示例看到了这种需求。

`env` 命令（注意它不是 shell 内置的命令）允许你在运行命令之前修改环境。它会显示所有的环境变量。

`env` 最常用的用法是在 shell 脚本开头。脚本通常以 shebang 行开头，告诉 Linux 使用哪种解释器：`[#!/usr/bin/ruby]`。
