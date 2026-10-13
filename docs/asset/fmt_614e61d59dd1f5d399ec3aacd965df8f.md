
在命令提示符处输入带有大量选项和参数的命令时，你通常需要将光标后移以添加或修改内容。例如，如果你作为普通用户输入一个长命令，然后发现命令需要在开头添加 `sudo`，快速将光标移动到命令开头。这是一个节省时间的快捷方式。命令行有很多快速移动的按键组合。表 7-2 列出并解释了其中几个。

| 组合键 | 操作 |
| :--- | :--- |
| Ctrl+a / Home | 将光标移动到命令行开头 |
| Ctrl+e / End | 将光标移动到命令行末尾 |
| Ctrl+u | 删除整行 |
| Ctrl+k | 从光标处删除到命令行末尾 |
| Alt+f | 光标逐次向右移动一个单词 |
| Alt+b | 光标逐次向左移动一个单词 |
| Ctrl+f / 右箭头 | 光标逐次向右移动一个字符 |
| Ctrl+b / 左箭头 | 光标逐次向左移动一个字符 |

表 7-2 有用的命令行编辑快捷键

对于经常在命令行下工作的普通用户和管理员来说，这些按键组合对节省时间非常有帮助。

## Tab 键自动补全

`Tab` 键自动补全（也称为命令行补全）是 `bash` shell 的一项功能，在命令行处输入文件、目录或命令名称的一个或多个初始字符，然后按两次 `Tab` 键即可自动补全整个名称。如果有多个可能项匹配输入的字符，它将补全到它们共同的部分为止，并在屏幕上打印其余的可能项。你可以输入一个或多个后续字符并再次按 `Tab` 键进一步缩小范围。当出现所需的名称时，按 `Enter` 键接受并执行操作。使用此功能的主要优点之一是节省了输入长文件、目录或命令名称的时间。

在你的 Linux 终端窗口中尝试此功能并熟悉它。

## 波浪号替换

波浪号替换（或波浪号扩展）适用于以波浪号字符 `~` 开头的单词。使用 `~` 时需要记住以下规则：

- 如果 `~` 作为独立字符使用，shell 指向运行命令的用户的 `$HOME` 目录。以下示例显示了 `user1` 的 `$HOME` 目录：

```
[user1@server1 ~]$ echo ~
/home/user1
```

- 如果加号 `+` 紧跟在 `~` 之后，shell 指向当前目录。例如，如果 `user1` 在 `/usr/bin` 目录：

```
[user1@server1 ~]$ echo ~+
/usr/bin
```

- 如果连字符 `-` 紧跟在 `~` 之后，shell 指向上一个工作目录。例如，如果 `user1` 在 `/usr/bin` 目录并执行 `~-`，输出显示上一个工作目录：

```
[user1@server1 ~]$ echo ~
/usr/bin
```

- 如果用户名前加了 `~`，shell 指向该用户的 `$HOME` 目录：

```
[user1@server1 ~]$ echo ~user1
/home/user1
```

波浪号替换也可以用于 `cd` 和 `ls` 等命令。例如，在任何地方使用 `~` 进入 `user1` 的主目录，指定用户名并带有 `~`：

```
[user1@server1 ~]$ cd ~user1
/home/user1
```

命令只有在 `user1` 有权限进入目标目录时才能成功。让我们作为 `root` 用户尝试此示例：

```
[root@server1 ~]$ cd ~user1
/home/user1
```

上述示例演示了作为 `root` 用户进入 `user1` 的主目录。另一个示例显示了用户如何从任何地方（如 `/etc/systemd/system`）进入子目录之一（例如 `/home/user1/dir1`），在目录结构中（创建 `dir1`）：

```
[user1@server1 ~]$ cd
[user1@server1 ~]$ mkdir dir1
[user1@server1 ~]$ cd /etc/systemd/system/
[user1@server1 system]$ pwd
/etc/systemd/system
[user1@server1 system]$ cd ~/dir1
[user1@server1 ~]$ pwd
/home/user1/dir1
```

尝试配合 `ls` 命令使用 `~`。例如，作为 `user1` 运行 `sudo -ld /root/Desktop`。

## 别名替换

别名替换（也称为命令别名）允许你为复杂的命令或命令集定义快捷方式。定义和使用别名可以节省时间并避免重复输入。当运行别名时，shell 会执行相应的命令或命令集。

`bash` shell 包含了用户登录时设置的几个预定义别名。可以使用 `alias` 命令查看这些别名。以下显示了当前为 `user1` 设置的所有别名：

```
[user1@server1 ~]$ alias
alias vi='vim'
alias which='(alias: declare -f) | /usr/bin/which --tty-only --read-alias --read-functions --show-tilde --show-dot'
```

`root` 用户有更多的默认别名。作为 `root` 运行 `alias`：

```
[root@server1 ~]$ alias
alias cp='cp -i'
alias ls='ls -l'
alias mv='mv -i'
alias rm='rm -i'
alias which='(alias: declare -f) | /usr/bin/which --tty-only --read-alias --read-functions --show-tilde --show-dot'
```

表 7-3 描述了上述两个输出中的别名。

| Alias | Value | Definition |
| --- | --- | --- |
| vi | vim | 运行 vim 命令而不是旧的 vi |
| cp | cp -i | 在交互模式下执行 cp 命令 |
| ll | ls -l | 以长格式显示 ls 命令的输出 |
| mv | mv -i | 在交互模式下执行 mv 命令 |
| rm | rm -i | 在交互模式下运行 rm 命令 |
| which | (alias; declare -f) | /usr/bin/which --tty-only --read-alias --read-functions --show-tilde --show-dot | 使用指定的选项运行 which 命令 |

表 7-3 预定义别名

除了列出别名集，`*alias*`（别名）还可以用于定义新的别名。取消别名的反向功能通过 `*unalias*` 命令完成。`*alias*` 和 `*unalias*` 都是 shell 内部命令。让我们来看几个例子。

创建一个别名为“search”的别名，以缩写带有多个开关和参数的 `*find*` 命令。将整个命令封装在单引号（''）中，以确保处理空格。在等号（=）前后不要留任何空格。

```
[user@server1 ~]$ alias search='find /name core -exec ls -l {}' \;
```

现在，当你在命令提示符输入字符串“search”并按下回车键时，shell 将别名“search”替换为存储的内容并运行它。本质上，你为该冗长的命令创建了一个快捷方式。

有时，你定义的别名名称与某些系统命令或程序的名称匹配。在这种情况下，shell 会赋予别名执行优先级。这意味着 shell 将运行别名而不是该命令或程序。例如，`rm` 命令在普通用户执行时会删除文件而不会发出任何警告。为了防止使用 `rm` 意外删除文件，你可以创建一个与命令同名的别名，但添加交互式选项，如下：

```
[user1@server1 ~]$ alias rm='rm -i'
```

现在当你执行 `rm` 来删除文件时，shell 将运行存储在 `rm` 别名中的内容，而不是 `rm` 命令。如果你想运行 `rm` 命令，可以在它前面加一个反斜杠（`\`）来运行：

```
[user1@server1 ~]$ \rm file
```

你可以使用 `unalias` 命令来取消一个或多个指定的别名，如果它们不再需要。以下操作将取消为示例中定义的两个别名：

```
[user1@server1 ~]$ unalias search rm
```

## 元字符与通配符

元字符（Metacters）是对 shell 具有特殊含义的特殊字符。其中包括美元符号（`$`）、脱（`^`）、点（`.`）、星号（`*`）、问号（`?`）、管道（`|`）、尖括号（`<>`）、大括号（`{}`）、中括号（`[]`）、括号（`()`）、加号（`+`）、叹号（`!`）、分号（`;`）和反斜杠（`\`）。它们被用于模式匹配（也称为文件名扩展或文件通配）和正则表达式。本节讨论用于模式匹配的元字符（`* ? []`）。`*`、`?` 和 `[]` 字符也被称为通配符。

### * 字符

星号（`*`）匹配零个到无限数量的字符，但隐藏文件名开头的点（`.`）除外。请看下面的用法示例。

列出 `/etc` 目录下所有以字母“ma”开头并后跟任意字符的文件：
