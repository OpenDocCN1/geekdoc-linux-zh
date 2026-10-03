
| 选项 | 说明 |
| --- | --- |
| `-Lzn` | 左对齐并去除前导零；`n` 指定字段宽度 |
| `-Rn` | 右对齐；`n` 指定字段长度 |
| `-Rzn` | 右对齐并去除前导零；`n` 指定字段宽度 |

下面的示例显示了如何将 `typeset` 作为显示变量的另一种方式。

## 示例 7-7：使用 typeset 显示变量

```
$ typeset
export VISUAL
export PATH
export ERROR
integer CDPATH
export OPTIND
integer LINENO
export LOGNAME
export SECONDS
integer PPID
export PS1
export PS2
export USER
function RANDOM
integer TMOUT
export SAVEPID
export HOME
export TERM
export TZ
$
```

接下来的示例显示了如何使用 `typeset` 命令定义变量。

## 示例 7-8：typeset 命令用法

```
$ typeset -u upper="This is uppercase"
$ typeset -l lower="LOWERCASE This"
$ print "$upper $lower"
THIS AN UPPERCASE       lowercase this
$ typeset -r constant=8214
$ print $constant
8214
$ constant=9620
is read only
$ typeset +r constant=9620
$ print $constant
9620
$
```

- ① 定义变量 `upper` 并将其属性设置为大写。给它赋一个值。
- ② 定义变量 `lower` 并将其属性设置为小写。给它赋一个值。
- ③ 显示变量 `upper` 和 `lower`，之间有一些空格。`upper` 被强制转为大写，`lower` 被强制转为小写。
- ④ 定义变量 `constant` 并将其属性设置为只读。给它赋一个值。
- ⑤ 显示只读变量 `constant`。
- ⑥ 尝试给 `constant` 赋另一个值。因为它是只读的，无法更改值。要更改值，必须使用 `typeset +r` 取消属性，然后重置属性。
- ⑦ 取消 `constant` 的属性。
- ⑧ 重新定义变量 `constant`，设置属性并为其赋新值 9620。
- ⑨ 显示 `constant` 的值。

这里显示了 Korn Shell 命令的示例。

## 示例 7-9：更多 typeset 命令用法

```
$ typeset -L9 first=Ambrosia
$ typeset -L3 mi="B"
$ typeset -L10 last="Salad"
$ print "$first$mi$last"
AmbrosiaB. Salad
$ first="Leaf-lettuce"
$ print "$first$mi$last"
Leaf-lettuB. Salad
$ typeset -lur constant=9620
lower='lowercase this'
upper="THIS AN UPPERCASE TEST"
$
```

- 定义第一个变量，并将其属性设置为字段宽度为 9 的左对齐。给它赋一个值。
- 定义变量 `mi` 并将其属性设置为字段宽度为 3 的左对齐。给它赋一个值。
- 定义变量 `last` 并将其属性设置为字段宽度为 10 的左对齐。给它赋一个值。
- 显示 `first`、`mi` 和 `last` 的值。变量之间没有空格，以确保使用变量属性来提供间距。
- 给 `first` 赋值，其包含的字符超过了属性允许范围。
- 显示 `first`、`mi` 和 `last` 的值。注意 `Leaf-lettuce` 被截断为九字符。
- 显示所有具有小写、大写和只读属性的变量。

# Korn Shell 选项

若干选项影响 Korn Shell 处理命令的方式。Korn Shell 会开启某些选项并允许你指定其他选项。Korn 为选项分配默认值，但你可以更改大部分选项。

使用 `set` 命令开启、关闭或显示 Korn shell 选项。`set` 命令的格式如下所示。

## 示例 7-10：set 命令格式

```
set -o          # 显示所有选项
set -o [option] # 开启一个选项
set +o [option] # 关闭一个选项
```

下面的示例显示了如何关闭 `ignoreeof` 选项并开启 `gmacs`。

## 示例 7-11：使用 set 命令设置选项

```
$ set -o +ignoreeof
$ set -o gmacs
```

下一个示例并排显示了 `set -o` 命令的两个输出。左侧是上一个示例修改之前的输出。右侧是修改发生后的输出；在 `ignoreeof` 已关闭且 `gmacs` 已开启之后。

## 示例 7-12：使用 set 命令显示选项

| （修改前） | （修改后） |
| :--- | :--- |
| allport off | allport off |
| bgnice on | bgnice on |
| emacs off | emacs off |
| erreet off | erreet off |
| gmacs off | gmacs on |
| ignoreeof on | ignoreeof off |
| interactive off | interactive on |
| trackall off | trackall off |
| verbose off | verbose off |
| vi off | vi off |
| viraw off | viraw off |
| xtrace off | xtrace off |

### 现在试一试！

在实验练习中，你将显示默认变量，然后显示用户变量。

1. 使用 `set` 显示 Korn 变量，然后使用 `typeset` 命令（不带选项）。比较输出。注意 `set` 命令提供了变量的名称和属性。
2. 使用 `print $RANDOM` 显示变量。多次执行该命令。`RANDOM` 变量提供 0 到 3267 之间的随机数。
3. 如下赋值变量：

```
$ myname="Mickey Mouse"
$ address="Disneyland"
$ age="52"
```

4. 使用 `print` 命令显示变量。
5. 使用 `unset` 命令清除三个变量 `myname`、`address` 和 `age`。显示变量并验证这三个用户变量不存在。
6. 使用 `set -o` 显示所有 Korn 选项。
7. 找到一个关闭的选项并使用 `set -o option_name` 开启它。使用 `set +o option_name` 关闭它。验证该选项已开启，另一个选项已关闭。
8. 检查 `emacs`、`gmacs` 和 `vi` 选项的状态。如果它们都没有开启，请开启其中一个。关闭另一个选项。验证该选项已开启，而之前开启的那个选项现在已关闭。

### 答案

```
$ set
ERRNO=0
FCEDIT=/usr/bin/ed
HOME=/usr/users/you
.
```

```
$ print $RANDOM
14768
$ print $RANDOM
22034
$ print $RANDOM
13180
$ print $RANDOM
1729
$.
```

3. 不需要解决方案。

```
$ print "My name is " $myname
My name is Mickey Mouse
$ print "My address is " $address
My address is Disneyland
$ print "I am " $age "years old"
I am 52 years old
```

4.

```
$ unset myname address age
$ print $myname $address $age
$.
```

5.

6.

7.

```
$ set -o allexport
$ set -o
Current option settings
allexport   on

$ set +o allexport
$ set -o
Current option settings
allexport   off
```

8.

```
$ set -o
Current option settings
allexport   off
bgnice      on
emacs       off
gmacs       off
vi          off

$ set -o emacs
$ set -o
Current option settings
allexport   off
bgnice      on
emacs       on
gmacs       off
vi          off

$ set -o vi
$ set -o
Current option settings
allexport   off
bgnice      on
emacs       off
gmacs       off
vi          on
```

# 定义 Korn Shell 启动文件

## 概述

当用户登录时，默认 shell 会执行系统和用户登录文件以定制用户环境。用户环境是由变量和选项定义的。本节提供了 Korn shell 启动文件的示例，并描述了一些可以设置的变量和选项。

Korn shell 启动文件包括：

- `/etc/profile`
- `$HOME/.profile`
- 由 `ENV` 变量指定的文件（我们将使用 `$HOME/.kshrc`）

当您登录时，`/etc/profile` 脚本首先运行。系统上的每个 Korn shell 用户都拥有此脚本；因此，它是系统管理员提供每个用户所需信息的良好位置。

接下来运行 `$HOME/.profile` 脚本。由于该脚本位于每个用户的 `$HOME` 目录中，每个用户都可以根据自己的需求对脚本进行定制。

每当您启动一个新的 Korn shell 或运行一个 Korn shell 脚本时，系统会自动调用环境脚本，即由 `ENV` 变量展开后指定的脚本文件。

将文件名分配给 `ENV` 变量是在 `$HOME/.profile` 文件中完成的，稍后描述。

## Korn Shell .profile 文件

当使用 Korn shell 作为默认 shell 登录时，如果存在 `/etc/profile`，Korn shell 会先执行该脚本，然后执行您的 `$HOME/.profile` 脚本。

使用您的 `$HOME/.profile` 脚本可以：

- 为您想要运行的所有程序设置并导出变量
- 设置您只想应用于登录 shell 的选项
- 指定一个在注销时执行的脚本

下面的示例显示了一个 Korn `.profile` 文件的样本。

### 示例 7-13：Korn Shell .profile 文件

```
CDPPATH=..:$HOME
ENV=$HOME/.kshrc
EDITOR=emacs
FCEDIT=emacs
PS1='! ksh '
export PATH ENV PS1
trap $HOME/.kshlogout EXIT
```

## Korn Shell 环境脚本文件

每次调用 Korn 时，它都会展开 `ENV` 变量，如果该变量不为空，则执行该脚本文件。我们将使用上一个示例 `.profile` 中定义的 `$HOME/.kshrc`。

使用 `.kshrc` 环境脚本文件可以：

- 定义适用于交互式使用以及由 Korn 调用脚本的别名和函数
- 设置您希望应用于所有 Korn Shell 调用的默认选项
- 设置您希望应用于当前 Korn shell 调用的变量

下表显示可能包含在 Korn shell 环境文件中的命令。

### 表 7-5：一些 .kshrc 命令

| 命令 | 功能 |
| --- | --- |
| `set -o monitor` | 允许 Korn shell 在启动后台作业时显示作业号，并在作业完成时启动状态消息 |
| `set -o trackall` | 缩短 Korn shell 查找某些命令所需的时间；Korn shell 在首次执行命令时会为该命令创建别名 |
| `set -o noclobber` | 使用 `>`（重定向）运算符时，防止 Korn shell 覆盖现有文件 |
| `alias l='ls -al'` | 定义一个获取所有文件列表的别名 |
| `alias h=history` | 定义一个提供命令历史的别名 |
| `alias c=clear` | 定义一个清除屏幕的别名 |
| `HISTSIZE=64` | 定义您通过 Korn shell 访问的之前输入的命令的最大数量为 64；默认值为 128 |
| `umask 022` | 创建文件创建掩码；`umask` 是一个 3 位八进制数，指定了当 Korn shell 或其任何子进程创建文件时系统应该移除的权限 |

## 总结

## 介绍 UNIX Shell

Tru64 UNIX 可用的 shell 及其默认提示符、文件名如下：

| 路径/提示符 | Shell |
| :--- | :--- |
| `/bin/csh` (%) | C shell |
| `/bin/sh` ($) | Bourne shell |
| `/bin/ksh` (*) | Korn shell |

Shell 可以作为编程语言使用，提供：

- 一个用于 Tru64 UNIX 解释器的用户界面
- 一个命令语言解释器

### 使用通配符运算符

- 星号 (`*`) 运算符可以匹配零或多个字符的任何字符串。
- 问号 (`?`) 运算符可以匹配任何单个字符。
- 通配符运算符的特殊含义可以通过在通配符前加上反斜杠 (`\`) 或将字符串括在单引号中来转义（关闭）。

## 描述 Korn Shell 环境

变量在定义 Korn shell 环境中起着重要作用。变量有两种类型：

- 预留变量
- 用户定义变量

Korn shell 有许多预留变量，它们分为两类：值为 Korn shell 命令的变量：

- 设置和更新
- 不自动设置

Korn 变量通过格式为 `name=value` 的赋值语句定义。使用 `set`、`typeset` 或 `print $name` 命令显示变量。`typeset` 命令设置变量的属性。

## 定义 Korn Shell 启动文件

系统和用户登录脚本定制以下环境特征：

- 终端特性
- 搜索路径
- Shell 变量
- 新文件的默认创建权限使用 `umask`
- 检查邮件
- 命令别名
- 历史变量
- `trap` 命令

以下文件设置 shell 变量和选项：

- `/etc/profile`
- `$HOME/.profile`
- 由 `ENV` 变量展开的环境文件

## 总结

# 单元概述

## 引言

本单元介绍了各种 UNIX 编辑器，并提供了 `vi` 编辑器的说明。`vi` 编辑器相对于 `emacs` 编辑器的主要优势是大多数 UNIX 系统都提供 `vi` 编辑器。如果您使用 `vi` 并移动到另一个 UNIX 系统，可能不需要学习其他编辑器。

本单元将向您展示如何启动和退出 `vi`、移动光标、查找和编辑文本、复制和移动文本。

## 目标

要在 UNIX 上编辑文件，您应该：

- 比较各种 UNIX 编辑器
- 启动和退出编辑会话
- 在文件中移动
- 查找和更改文本
- 复制和移动文本

## 资源

有关本单元主题的更多信息，请参阅：

- 命令和 Shell 用户指南附录 A `http://faqs/publications/base_doc/DOCUMENTATION/V40D_HTML/APS2HDTE/TITLE.HTM`
- `vi` 参考页面

## 介绍编辑器

下表显示了大多数 UNIX 系统上的标准编辑器。

### 表 8-1：标准 UNIX 编辑器

| 编辑器 | 说明 |
| --- | --- |
| `ed` | 逐行操作的行编辑器；`ed` 是单用户模式下唯一的可用编辑器 |
| `ex` | 与 `ed` 类似的行编辑器，但更强大；提供了 `vi` 屏幕编辑器命令的子集（可以从 `ex` 调用 `vi` 编辑） |
| `edit` | 为初学者设计的行编辑器；`ex` 的简化版本 |
| `sed` | 流编辑器，根据命令行或脚本文件中的命令修改行 |
| `vi` | 基于 `ex` 行编辑器的全屏显示编辑器；使用可以自定义的操作模式和选项 |
| `view` | `vi` 的只读版本 |
| `emacs` | 强大、可扩展的屏幕编辑器，允许在多个窗口中编辑并具有广泛的帮助功能；GNU `emacs` 编辑器可从自由软件基金和 Tru64 UNIX 免费软件光盘获取 |

通用桌面环境 (CDE) 还包含一个带有图形用户界面的基础文本编辑器。请查看前面板上的文本编辑器图标。

# 使用 vi 编辑

## 概述

本节将讨论 `vi` 的操作模式，以及如何开始和结束编辑会话。

## 设置你的终端

如果你正从远程主机使用远程的 Tru64 UNIX 系统，请将你的工作站窗口或终端设置为 VT100 模式。否则，当你按下 Escape (Esc) 键返回命令模式时，上一个输入字母的大小写可能会发生变化（从大写变小写，或反之亦然）。

例如，在 DECterm 窗口中，从 Options（选项）菜单选择 General...，然后选择 VT100 模式。

某些键盘没有标记为 Esc (Escape) 的键。在你的系统中可能有效的替代按键包括：

- 按 F11 键
- 在 DeCTerm 窗口中，下拉 Options 菜单并选择 Keyboard。然后选择 "F11 sends Escape"。
- 按 `Ctrl/[`

## 编辑模式

编辑器有三种操作模式：

### 命令模式 (Command mode)

使用 `vi` 编辑文件时进入的默认模式。用于移动光标以及删除或更改文本。
