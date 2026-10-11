
**参数**也出现在命令名之后，但并不以连字符开头。它们指定了命令处理的参数，这些参数并不是由命令开发者预定义的。例如，你想列出硬盘上 `/var/ftp/etc` 目录下的所有文件。你可以像示例所示使用 `ls` 命令配合 `-a` 选项（告诉 `ls` 命令列出所有文件）和 `/var/ftp/etc` 参数（告诉 `ls` 在 `/var/ftp/etc` 目录中查找）：

```bash
[root@localhost root]# ls -a /var/ftp/etc
  .. group ld.so.cache ld.so.conf passwd
[root@localhost root]#
```

# 第 3 章 Linux 的安装与使用

一旦你输入命令并按回车键，`ls` 命令在上面的输出中向你显示 `/var/ftp/etc` 目录中有四个文件，并返回你的命令提示符，以便你输入另一个命令。

> 命令、选项和参数是对大小敏感的；例如，大写字母 `A` 的方式与小写字母不同。

> 务必在命令名、选项和参数之间留有空格；否则 shell 将无法理解它们是分开的，你的命令可能无法按预期工作。

尽管你可以向命令传递选项或参数，但并不是所有命令都需要在命令行提供参数或选项才能正常工作。`date` 命令就是一个示例，它只需打印当前的日期和时间：

```bash
[root@localhost root]# date
Tue Mar 26 08:58:36 EST 2002
[root@localhost root]#
```

无需指定任何选项或参数即可使用的某些命令列表 3-3 中。

## 表 3-3 常用 Linux 命令

| 命令 | 描述 |
| --- | --- |
| `clear` | 清除终端屏幕 |
| `reset` | 重置终端以使用默认终端设置 |
| `finger` | 显示系统用户信息 |
| `who` | 显示当前登录的用户 |
| `w` | 显示当前登录的用户及其正在的任务 |
| `whoami` | 显示你的登录名 |
| `id` | 显示与你的用户账户名和组名相关的数字。这些通常称为用户 ID (UID) 和组 ID (GID) |
| `date` | 显示当前的日期和时间 |
| `cal` | 显示当前月的日历 |
| `exit` | 退出当前的 shell |

如果某个命令的输出太大而无法适应终端屏幕，只需同时按下 `Shift` 和 `Page Up` 键即可查看之前的屏幕信息。同样，同时按下 `Shift` 和 `Page Down` 可以反向导航。

用户可以使用键盘键（上、下、右、左箭头键）回以前在 BASH Shell 中输入过的命令。因此，如果你想再次输入相同的命令，只需用键盘光标在可用命令列表中循环并按回车键重新输入。

## 元字符

shell 的另一个重要特性是元字符，它们具有特殊含义。shell 解释的最常用字符是变量。变量是存储在内存中的一段信息；例如，如果你需要在命令中使用变量，可以在其前面加上 `$`。为了这样做，只需用单引号 `' '` 包裹元字符。单引号将保护元字符不被解释（即，在单引号内，`$` 将被视为文本）。你也可以使用双引号 `" "` 来执行相同的任务；然而，双引号不保护 `$` 字符。如果只有一个字符需要保护，可以在该字符前加上 `\`。这种类型的引号示例如下：

```bash
[root@localhost root]# echo My $SHELL
My Shell is /bin/bash
[root@localhost root]# echo 'My $SHELL'
My Shell is $SHELL
[root@localhost]# echo "My $SHELL"
My Shell is /bin/bash
[root@localhost root]# echo My \$SHELL
My Shell is $SHELL
```

从上面可以看出，`$` 被翻译成了变量。书中讨论的常用元字符列表 3-4。

## 表 3-4 常用 Shell 元字符

| 元字符 | 描述 |
| --- | --- |
| `$` | Shell 变量 |
| `&` | 后台执行 |
| `;` | 命令结束 |
| `\|` | 输入/输出重定向 |
| `\|` | 命令管道 |
| `*` | Shell 通配符 |
| `"` | Shell Quotes |
| `()` | 命令分组 |

如表 3-4所示，并不是所有的引号都能防止解释。反引号 ``` `` ``` 可用于命令替换；反引号内的任何内容都被 shell 视为另一个命令，其输出将替换反引号的内容。以 `date` 表达式为例：

```bash
[root@localhost]# echo Today is `date`
Today is Tue Mar 26 09:28:11 EST 2002
```

如果你不小心使用了这些字符之一，且 shell 没有返回到正常提示符，只需按下 `Ctrl+C` 即可取消当前命令。

## 获取命令帮助

大多数 Linux 发行版在配置中包含超过1000个 Linux 命令，记忆每个命令的语法和用法是不现实的。幸运的是，Linux 将每个命令的文档存储在可以访问的位置。Linux 命令常用的文档形式是手册页（通常称为 man 页）。只需输入 `man` 命令后跟命令名，该 Linux 命令的详细信息就会逐页显示在终端屏幕上。这些信息包括命令的描述及其语法、可用选项以及相关的文件和命令。例如，要获取 `whoami` 命令的格式和用法信息，你可以输入以下：

```bash
[root@localhost root]# man whoami
```

# Linux 基础用法 107

随后，终端屏幕上会逐页显示帮助页内容。你可以使用键盘上的方向键滚动查看信息，或按 `q` 退出。`whoami` 的帮助页类似于下面：

```text
WHOAMI(1)                FSF                WHOAMI(1)
whoami - print effective userid

SYNOPSIS
whoami [OPTION]...

DESCRIPTION
打印与当前有效用户 ID 关联的用户名。同于 id -un。

--help 显示此帮助并退出

--version
输出版本信息并退出

AUTHOR
由 Richard Mlynarik 编写。

REPORTING BUGS
向 <bug-sh-utils@gnu.org> 报告错误。

COPY
Copyright (c) 2000 Free Software Foundation, Inc.
这是免费软件；复制条件请参阅源代码。不提供任何保证；即使是对商品性或特定用途的适用性也不保证。
```

`SEE ALSO`

`whoami` 的完整文档作为 Tex-info 手册维护。如果你的站点正确安装了 `info` 和 `who` 程序，执行命令 `info whoami` 应该可以让你访问完整的手册。

```text
GNU sh-utils 2.0.11        July 2001        WHOAMI(1)
[root@localhost root]#
```

注意，在上面的帮助页中，`whoami` 命令显示为 `WHOAMI(1)`。`(1)` 表示帮助页的一个章节；第 `(1)` 节表示 `whoami` 是一个任何用户都可以执行的命令。所有帮助页都包含某些章节，描述命令在帮助页数据库中的类别；帮助页章节编号列表可以在表 3–5 中找到。

## 表 3-5 帮助页章节编号

| 帮助页章节 | 说明 |
| --- | --- |
| 1 | 用户可以执行的命令 |
| 2 | Linux 系统调用 |
| 3 | 库例 |
| 4 | 特殊设备文件 |
| 5 | 文件格式 |
| 6 | 游戏 |
| 7 | 宏包 |
| 8 | 只有 root 用户可以执行的命令 |
| 9 | Linux 内核例 |
| n | 未分类的新命令 |

有时，会有多个同名的命令、库例或文件。如果你以该名称作为参数运行 `man` 命令，Linux 将返回章节编号最低的帮助页。例如，如果有一个名为 `whoami` 的文件和一个名为 `whoami` 的命令，当你输入 `man whoami` 时将显示 `whoami` 命令的帮助页（帮助页的第 1 节）。如果要显示 `whoami` 文件格式的帮助页，你只需输入 `man 5 whoami`（帮助页的第 5 节）即可。

记住，Linux 用户有许多可用命令；因此，如果不使用 Linux 命令字典，要找到执行特定任务所需的命令可能非常繁琐。幸运的是，你有通过关键词搜索帮助页的能力。要找到所有名称或描述中包含“who”单词的命令，请输入：

```bash
[root@localhost]# man -k who
```

此命令将产生以下输出：

```text
at.allow [at] (5) - 确定谁可以通过 at 或 batch 提交作业
at.deny [at] (5) - 确定谁可以通过 at 或 batch 提交作业
biff (1) - 如果邮件到达且来自某人则收到通知
```

# Linux 基础用法 109
