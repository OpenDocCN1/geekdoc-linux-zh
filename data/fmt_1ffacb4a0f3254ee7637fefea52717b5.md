
```
alias diff='/local/bin/diff -L -e'
alias info='echo "connecting..."'
alias sunworld='echo SunWorld: taylor;ssh sunworld.com'
```

记得这些别名都源于我的 `.bashrc`：

```
% grep .bashrc
alias diff='/usr/bin/diff -w'
alias from='rm -n'
alias info='ssinfo'
alias ls='/usr/bin/ls -F'
alias mail='mail'
alias mailq='/usr/lib/sendmail -bp'
alias sunworld='echo SunWorld: taylor;ssh sunworld.com'
alias aliases='echo mean aliases...'
alias diff='/local/bin/diff -L -e'
```

此外注意 `Shell` 会按字母顺序排序别名列表，无论定义的顺序如何。

### 2. 大多数别名都很容易理解
例如，第一个 `diff` 确保命令始终带有 `-c` 和 `-w` 标志。如果我输入 `from`，我希望系统调用 `rm -n`；如果我输入 `ls`，我希望系统调用 `ls -F` 等。

如果输入了某些命令可能会引起麻烦，为每个命令创建别名是避免麻烦的好方法。例如，我有一个 `aliases` 别名；如果我不小心输入了 `aliases`，系统通常会提醒我可能想用 `alias` 命令：

```
% aliases
```

### 3. 我创建了连接其他系统的别名
我喜欢根据连接的系统来命名每个别名（例如 `sunworld`）：

```
% alias sunworld
alias sunworld='echo SunWorld: taylor;ssh sunworld.com'
```

你不能输入 `alias sunworld` 来列出别名，因为该命令会将 `alias` 替换为 `sunworld` 命令。

![](img/9187b56a3187f4de32441e7ff5d7a5_308.png)

## 第 14 小节：高级 Shell 交互

用分号分隔命令是 Unix 单行中运行多个命令的方法，所以当我输入别名 `sunworld` 时，就像我一个一个输入了这些命令一样：

```
echo Sunworld: taylor
ssh sunworld.com
```

别名让 `Shell` 变成了一个非常强大的命令界面。我可以并且轻松地自定义命令集和默认标志（看我为 `ls` 命令设置的所有默认值）。我甚至禁用了一些我不想输入的命令。让你的想象力在别名上发挥吧。如果你喜欢其中一个并且正在使用 `bash`，将别名添加到 `.bashrc` 中使其永久生效（如果你愿意，也可以将这些放入 `.profile` 中）。如果你想关闭一个别名，可以使用 `alias` 命令，它在下次登录前都会消失。例如，`unalias sunworld` 会临时从 `Shell` 中移除之前显示的 `sunworld` 别名。

## 任务 14.5：设置自定义提示符

到为止，我看到的命令提示符是 `$`。事实证明 `bash` 允许将提示符设置为任何可能的值，格式为 `PS1="value"`。注意，`PS1` 必须全大写才能生效。

### 1. 我厌倦了 Unix 如此不友好
坦率地说，我可以轻松地改变它对我的响应方式：

```
% PS1=Yes, master?
Yes, master?
```

那更有趣了！

### 2. 在提示符中可以隐藏很多非常有帮助的东西，它们都以 `\X` 的形式出现
第一个有用变量是 `\w`，它包含当前工作目录：

```
Yes, master? PS1="In \w, oh master:
In /users/taylor, oh, master:
```

如果我切换了目录会发生什么？

```
In /users/taylor, oh master: cd /
In / , oh master:
```

很酷，对吧？

### 3. 你可以添加许多种不同的变量，其中最有用的如表 14.2 所示

## 哪种 Shell 是哪个

## 表 14.2 系统提示符（System Prompt）的特殊值

| 值 | 展开为 |
| :--- | :--- |
| `\d` | 星期 月 日 格式的日期（例如：Thu Feb 1）。 |
| `\H` | 完整的系统主机名（例如：limbo.intuitive.com） |
| `\h` | 系统名（例如：limbo） |
| `\n` | 回车序列（是的，如果你愿意，你可以有一个双行的提示符！） |
| `\s` | shell 的名称（例如：bash2.4） |
| `\T` | HH:MM:SS 格式的当前时间（例如：04:23:28） |
| `\t` | 与 `\T` 相同，但采用24 小时制（例如：16:23:28） |
| `\@` | am/pm 格式的当前时间（例如：04:23pm） |
| `\u` | 当前用户的用户名（例如：taylor） |
| `\w` | 当前工作目录（例如：/home/taylor/bin） |
| `\B` | 当前目录的基名（例如：bin） |

还记得之前我们学过通过命令数字来重复命令吗（比如用 `!37` 重复第 37 号命令）？事实有一个环境变量 `HISTCDMD` 包含了当前的命令数字。它在提示符中可以证明非常有价值：

在 /, oh master: `PS1="\($HISTCMD) \$ "`

(132) \$

`ksh` 的等效写法是 `PS1="\(! ) \$ "` 。

括号中的数字是 shell 历史记录机制中使用的命令数字：

```
(132) $ echo hi
hi
(133) $ ls News
mailing.lists.usenet usenet.alt
(134) $ !132
echo hi
hi
(135) $
```

这里另一个你可能觉得很有用的例子：

(135) % `PS1="\h (\$HISTCMD) % %`

limbo (136) $

这与我自己使用的很像，但我喜欢包含当前目录的基名（basename）。basename 意味着最最近的目录名，所以 basename 是

例如，`/home/taylor` 是 `taylor`。此外，我把美元符号替换成了冒号，这样读起来容易一点。

```
limbo (136) PS1="\h (\W) \$HISTCMD : 
limbo (taylor) 137 :
```

尝试并找到一组可以帮助你自定义 Unix 提示符的变量。我强烈建议你使用命令数字来熟悉历史记录机制。

命令别名（command-alias）功能是减少重复输入命令有用方法，但如果你有一系列经常顺序执行的 5 或 10 个命令呢？这就是 shell 脚本可以派用场的地方。

## 总结

这一小时向你介绍了 Unix 命令 shell 的许多最强大的方面。练习创建别名和处理历史列表，以尽可能地减少你的打字量。此外，找一个你喜欢的提示符并将其设置在 `.bashrc` 或 `.profile` 中，使其成为你的默认设置。

# 工作坊

工作坊总结了你学到的关键术语，并对本章介绍的主题提出了问题。它还让你预览了下个小时将学习的内容。

## 关键术语

- **basename**: 最最近的目录名。例如，`/usr/home/taylor` 的 basename 是 `taylor`。

- **command number**: shell 索引所有命令的唯一数字。你可以通过使用 `$HISTCMD` 将此数字放在提示符中，并使用 `!command-number` 与历史机制配合使用。

## 练习

- 1. 你如何告诉 `bash` 你希望它在会话期间记住最后 30 条命令，并在登录会话之间记住最后 10 条命令？

- 2. 假设你输入 `history` 得到以下输出：

```
ls -CF
who | grep andrews
wc -l test
cat test
history
```

输入以下每个历史命令的结果是什么？

```
!2 !w lwh echo !1
```

- 3. 某些 Unix 系统不会允许你执行以下操作。你认为这个别名潜伏着什么危险？

```
alias who -a
```

- 4. 你认为以下哪些别名是有有用的？

```
alias ls='cp'
alias copy='cp -'
alias logout='vi'
alias vi='logout'
alias bye='logout'
```

- 5. 将你的提示符设置为以下值。记住每次都要将 33 替换为相应的命令数字。

```
#33 - I know lots about Unix. For example:
```

## 下一小时预览

在下一小时中，你将学习如何更进一步利用你的 shell。你将学习 shell 编程以及如何动态创建 shell 程序。

## 第 15 小时

## 作业控制
