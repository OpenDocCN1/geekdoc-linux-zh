
`rem` 程序收集所有匹配条目到一个临时文件中。如果文件大小为零，则未找到匹配项，并会发出相应的消息。否则，对于每个匹配项，程序会显示该条目并询问用户是否删除该条目。这为用户提供了保障，确保用户想要删除的条目与程序想要删除的条目，即使在特殊情况下也是如此。

在输入 `y` 后，执行 `break` 命令退出循环。在循环外部，程序测试 `answer` 的值以确定退出循环的方式。如果其值不等于 `y`，则由于某种原因，用户并不想删除该条目。否则，程序将通过 `grep` 排除所需行以外的所有行来执行删除（在这里，`grep` 指定的模式通过锚定行首和行尾来仅匹配整行）。

# change

```bash
#
# 修改电话簿中的条目
#
name=$
#
# 获取匹配条目并保存到临时文件
#
grep "$name" PHONEBOOK > /tmp/matches
if [ ! -s /tmp/matches ];
then
  echo "I can't find name in the phone book"
  exit 1
fi
#
# 逐个显示匹配条目并确认修改
#
while read line
do
  display "$line"
  echo "Change this entry (y/n)? \"
  read answer < /dev/tty
  if [ "$answer" = y ];\nthen
    break
  fi
done < /tmp/matches
rm /tmp/matches
if [ "$answer" != y ];
then
  exit
fi
#
# 在确认的条目上启动编辑器
```

```bash
#
echo "$line" | tr ' ' '\012' > /tmp/ed$$
```

```bash
echo "Enter changes with ${EDITOR:-/bin/ed"
trap '' SIG 2  # 如果编辑时按了 DELETE，则不终止
EDITOR=/tmp/ed$$
```

```bash
#
# 删除旧条目并插入新条目
```

```bash
grep -v "$line" > /tmp/phonebook$$
tr '\012' < /tmp/ed$$; echo >> /tmp/phonebook$$
# 最后一次 echo是为了恢复被 tr 丢失的末尾换行
```

```bash
sort /tmp/phonebook$$ -o PHONEBOOK
rm /tmp/ed$$ /tmp/phonebook$$
```

`change` 程序允许用户编辑电话簿中的条目。内部字段分隔符被设置为 `^`，因为这是我们想要修改的一个项（使用默认编辑器——记住变量 `EDITOR` 可以设置为不同的编辑器）。由 `2` 生成的信号被忽略，这样如果用户按下 Delete 键，程序就不会退出。

## Rolo 重复习

你是否想：
...
请选择上述选项之一 (1-6): 2

输入你的新条目
完成后，只需在行尾按一次回车键。
>> YMCA
>> 973-555-2344

YMCA 已添加到电话簿
你是否想：
...
请选择上述选项之一 (1-6): 2

输入你的新条目
完成后，只需在行尾按一次回车键。
>> Maureen Connelly
>> 10 Mainland Drive
>> Hashbrook Heights, N.J. 07604
>> 201-555-6008

Maureen Connelly 已添加到电话簿
你是否想：
...
请选择上述选项之一 (1-6): 2

输入你的新条目
完成后，只需在行尾按一次回车键。
>> Teri Zak
>> (地址请参见 Maureen Connelly)
>> 201-555-6060

Teri Zak 已添加到电话簿
你是否想：
...
请选择上述选项之一 (1-6): 5

Maureen Connelly 201-555-6000
Steve's Ice Cream 212-555-3021
Teri Zak 201-555-6060
YMCA 973-555-2344

你是否想：
...
请选择上述选项之一 (1-6): 1
输入要查询的名字: Maureen Connelly

Maureen Connelly
Hayden Book Company
10 Mainland Drive
Hashbrook Heights, N.J. 07604
201-555-6008

Teri Zak

Unix® Shell Programming, 第三版. Unix® Shell Programming, 第三版, ISBN: 0-672-32490-3
由 O'Reilly Media 为架构师准备。此下载文件仅供个人使用，并受服务条款的约束。任何使用均需事先书面许可，版权所有 © 2003 O'Reilly Media。严禁未经授权的使用、复制和/或分发，这些行为违反了适用法律。保留所有权利。

## Rolo 重复习

Hayden Book Company
(地址请参见 Maureen Connelly)
201-555-0260

你是否想：
请选择上述选项之一 (1-6): 
输入要修改的名字: Maureen

Maureen Connelly
Hayden Book Company
10 Midland Drive
Hambrouck Heights, NJ 07604
201-555-0260

修改此人 (y/n)? yn
使用 /bin/ed 输入更改内容
101
Maureen Connelly
Hayden Book Company
10 Midland Drive
Hambrouck Heights, NJ 07604
201-555-0260

修改拼写错误
Hayden Book Company
101

你是否想：
请选择上述选项之一 (1-6): $

这里没有测试的函数是删除条目。
希望这个示例能让你对如何开发更大的 shell 以及如何使用系统提供的许多编程工具有所见解。除了内置命令外，rolo 依赖 `tr`、`grep`、编辑器、`sort` 以及 `mv` 和 `cm` 等标准文件系统命令来完成工作。这种让你能够轻松连接所有这些工具的简单与优雅，构成了 Unix 系统所需的极性。

关于下载 rolo 程序的更多信息，请参见附录 B。

第 15 章“交互与非标准 shell 特性”向你介绍了 shell 的交互式功能以及两个在 POSIX 标准 shell 中未发现的优秀功能的 shell。

## 练习

- 1: 修改 rolo，使得在查询电话簿时不区分字母大小写。

Unix® Shell Programming, 第三版. Unix® Shell Programming, 第三版, ISBN: 0-672-32490-3
为学术目的准备，Terry Young
版权所有 © 2003 Wiley Publishing。此下载文件仅供个人使用，并受服务条款的约束。任何其他使用均需事先书面许可版权 © 2003 Wiley。严禁未经授权的使用、复制和/或分发，这些行为违反了适用法律。保留所有权利。

## Rolo 重复习

- 2: 为 rolo 添加一个 `-m` 命令行选项，用于向命令行后跟随的人员发送邮件。让 rolo 在电话簿中查找该人员，并在匹配的条目中寻找字符串 `mail-ladder`，其中地址是该人的邮件地址。启动编辑器（进入更改模式）允许用户输入邮件地址。编辑完成后，将消息发送给用户。如果在电话簿中未找到邮件地址，则提示输入。

在菜单中也添加一个邮件选项，以便可以交互式选择。提示要发送邮件的人名。

- 3: 在添加 `-m` 选项后，添加一个 `-f` 选项，指定邮件内容来自命令行后跟随的文件。

```bash
rolo -n tony memo
```

应该查找 tony 并向他发送文件 memo 内容。

- 4: 你能想出其他使用 rolo 的方法吗？例如，它可以被用作小型通用数据库程序（例如用于存储食谱或员工数据）？

- 5: 修改 rolo，使用命令行后跟随的文件而不是导出的 `PHONEBOOK` 变量来指定邮件内容来自该文件。rolo 在每个用户的家目录下包含该用户的路径，例如：

```bash
$ HOME/rolo
/steve
```

然后向 rolo 中添加一个选项，允许用户交互式查找其他用户。该选项应位于菜单中。提示要发送邮件的人名。例如：

```bash
-u Pizza
```

让 rolo 在电话簿中查找 Pizza，无论谁在运行 rolo。程序通过查看家目录下的 `.rolo` 就能找到它。

- 7: 为 rolo 添加一个 `-s` (send) 选项，向指定的用户发送邮件。所以

```bash
-s tom
```

应该查找 tom 并将 rolodex 条目发送给用户。

Unix® Shell Programming, 第三版. Unix® Shell Programming, 第三版, ISBN: 0-672-32490-3
由 O'Reilly Media 为架构师准备。© 2003 Wiley Publishing。此下载文件仅供个人使用，并受服务条款的约束。任何其他使用均需事先书面许可。版权所有 © 2003 Wiley。

## 交互交互式与非标准 shell 特性

- 1: 修改 rolo，使得在查询电话簿时不区分字母大小写。

- 2: 为 rolo 添加一个 `-m` 命令行选项，用于向命令行后跟随的人员发送邮件。让 rolo 在电话簿中查找该人员，并在匹配的条目中寻找字符串 `mail-ladder`，其中地址是该人的邮件地址。启动编辑器（进入更改模式）允许用户输入邮件地址。编辑完成后，将消息发送给用户。如果在电话簿中未找到邮件地址，则提示输入。

在菜单中也添加一个邮件选项，以便可以交互式选择。提示要发送邮件的人名。

- 3: 在添加 `-m` 选项后，添加一个 `-f` 选项，指定邮件内容来自命令行后跟随的文件。

```bash
rolo -n tony memo
```

应该查找 tony 并向他发送文件 memo 内容。

- 4: 你能想出其他使用 rolo 的方法吗？例如，它可以被用作小型通用数据库程序（例如用于存储食谱或员工数据）？

- 5: 修改 rolo，使用命令行后跟随的文件而不是导出的 `PHONEBOOK` 变量来指定邮件内容来自该文件。rolo 在每个用户的家目录下包含该用户的路径，例如：

```bash
$ HOME/rolo
/steve
```

然后向 rolo 中添加一个选项，允许用户交互式查找其他用户。该选项应位于菜单中。例如：

```bash
-u Pizza
```

让 rolo 在电话簿中查找 Pizza，无论谁在运行 rolo。程序通过查看家目录下的 `.rolo`就能找到它。

- 7: 为 rolo 添加一个 `-s` (send) 选项，向指定的用户发送邮件。所以

```bash
-s tom
```

应该查找 tom 并将 rolodex 条目发送给用户。

### 获取正确的 shell

大多数 shell 都遵循一种允许你选择程序运行文件的约定。如果文件的第一行两个字符是 `#!`，该行的剩余部分指定了解释器。所以

```bash
#!/usr/bin/ksh
```

指定 Korn shell 

```bash
#!/usr/bin/bash
```

指定 Bash。注意你可以在这里放置任何你想要的程序，作为一个 Perl 程序开头以

```bash
#!/usr/bin/perl
```

强制 shell 执行此功能时要谨慎，因为许多程序（如 Perl）在每个 Unix 上并没有存放在标准位置。此外，这不是 POSIX 标准指定的功能。

### ENV 文件

当你启动 shell 时，它执行的操作之一是在你的环境中查找一个名为 `ENV` 的变量。如果找到，`ENV` 指定的文件将被执行，就像登录时执行 profile 一样。

如果你决定拥有 ENV 文件，你应该在你的 `.profile` 文件中导出 `ENV` 变量：

```bash
$ cat profile
ENVPATH=/alias
export ENV
```

对于 Bash，ENV 文件只有当 Bash 以 sh 名称调用或带有 posix 命令行选项时，或者在执行 `set -posix` 之后才会读取。默认情况下，当非交互 Bash shell 启动时（例如当你运行一个 shell 程序时），它从 `BASH_ENV` 环境变量指定的文件读取命令，而当交互 Bash shell 启动时（例如通过在命令行提示符输入 bash），它不这样做。

## 交互式与非标准 Shell 特性

```bash
cat .profile
SHELL=/usr/bin/ksh
export SHELL
```

该变量被某些应用程序（如 vi）用于确定在执行 shell 转义字符（shell escape）时启动哪个 shell。在这种情况下，你希望确保每次启动新 shell 时，获取的是你想要的 shell，而不是旧版本的 Bourne shell。

## 命令行编辑

行编辑模式（Line edit mode）是 shell 的一项功能，允许你使用内置命令来编辑命令行，这些命令模拟了两种流行编辑器中的操作命令。POSIX 标准提供了模拟 vi 的能力；然而，Bash 和 Korn shell 也支持 emacs 行编辑模式。我们在附录 A “总结”中的表 A.4 中列出了完整的 vi 命令集。

如果你曾使用过过这些编辑器中的任何一个，你会发现 shell 内置的编辑器是它们全屏版本的忠实复刻。如果你从未用过屏幕编辑器，不要被吓到。这是 shell 中最有用的功能之一。事实上，在学习如何使用 shell 的内置编辑器之后，你将能够很费力地学会 vi 或 emacs。

要开启行编辑模式，请使用带有 `-o` 模式选项的 `set` 命令，模式可以是 vi 或 emacs：

```bash
set -o vi
```

注意，你可以将此内容放入你的 `.profile` 或 ENV 文件中，以便自动启动开启了你所选编辑模式的 shell。

## Command Shell 历史记录

如前所述，shell 会保留之前输入过的命令的历史记录。每当你按下 Enter 键执行命令时，该命令就会添加到此历史列表的末尾。命令列表实际上存储在一个文件中，这意味着你可以在登录会话之间访问之前输入的命令。默认情况下，历史列表保存在你的主目录中，名为 `.sh_history`（除非以 `--POSIX` 选项开头，否则 Bash 为 `.bash_history`）。你可以通过设置 `HISTFILE` 变量为任何你名称来更改它。该变量可以在 `.profile` 文件中设置并导出。

自然地，shell 回忆的命令数量是有限制的。此限制的默认值随实现而异，但 POSIX 标准要求其至少为 128；Korn shell 的默认值为 128；Bash 的默认值为 500。每次登录时，shell 都会自动将你的历史截断到该长度。

你可以通过 `HISTFILE` 变量控制历史记录的大小。你可能会发现默认大小无法满足你的需求，这时你可能希望将 `HISTSIZE` 变量设置为较大的值，例如 500 或 1000。你分配给 `HISTSIZE` 的值可以在 `.profile` 中设置并导出：

```bash
cat .profile
HISTSIZE=500
export HISTSIZE
```

对于分配给 `HISTSIZE` 的值要合理。值越大，越更多的磁盘空间来存储历史文件，shell 搜索整个历史文件的时间也越长。

## vi 行编辑模式

在开启 vi 行编辑器后，你将处于输入模式。你可能不会察觉输入模式有任何不同，因为你输入和执行命令的方式与在启动 vi 行编辑器之前几乎完全一样：

```bash
$ set -o vi
echo hello
bell
pwd
/users/pat
```

要使用行编辑器，你必须按下 ESCAPE 或 Esc 键进入命令模式，该按键通常在键盘的左上角。当你进入命令模式时，光标会向左移动到最后一个输入的字符。当前字符就是光标所处的字符；稍后我们会详细说明当前字符。进入模式后，你可以使用 vi 命令。注意，vi 命令后面不需要跟点号。

在输入长命令时遇到的一个问题是，你可能会在输入后发现命令行中存在错误。无例外，错误位于行开头。在命令模式下，你可以自由移动光标而不干扰命令。当你将光标移动到错误位置后，可以将该字母或多个字母改为任何你字符。

在下面的示例中，下划线 (\_) 代表一个字符。命令行将通过一次或多次按键，显示为应用按键后的行状态：

| 按键前 | 按键后 |
| :--- | :--- |
| mary had a little lab | $ mary had a little lab |
| mary had a little la | $ mary had a little la |
| h | $ mary had a little la |
| l | $ mary had a little lab |
| mary had a little lab | $ mary had a little lab |

当光标位于你想更改的字符之后时，可以使用 `x` 删除当前字符（“X”掉它）。

```bash
$ mary had a little lab x $ mary had a little lab
```

注意，当 `r` 被删除时，`b` 向左移动了并且现在是当前字符。

要向命令行添加字符，可以使用 `i` 和 `a` 命令。`i` 命令在当前字符之前插入字符，`a` 命令在当前字符之后添加字符。这两个命令都会将你带入输入模式。返回命令模式，必须按下 Esc。

首先，让我们看看如何移动光标。`H` 键让光标向左移动，`L` 键让它向右移动。尝试进入命令模式并按几次 `H` 和 `L`。光标会在行内移动。如果你尝试将光标移出行的左侧或右侧，它会向你发出“哔”声。

# 交互式与非标准 Shell 特性

```bash
$ echo this is a test
```

每次使用 k 命令时，当前行都会被命令历史中的上一行替换。
