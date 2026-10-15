

## ksh 历史导航命令

### 表 3.2

| COMMAND | FUNCTION |
|---|---|
| Ctrl P | 召回上一条命令 |
| Ctrl N | 召回下一条命令（仅在你已移动到上一条命令后才有效） |
| Ctrl R something | 获取包含 "something" 的上一条命令 |
| Ctrl B | 在命令内向后移动一个字符 |
| Ctrl F | 在命令内向前移动一个字符 |
| Ctrl A | 在命令内移至行首 |
| Ctrl E | 在命令内移至行尾 |
| Ctrl D | 删除当前字符 |

## 在 ksh shell 中查看会话历史：

- 1. set -o emacs
首先，你必须输入 set -o emacs。该命令启用历史重用和命令补全，并将 shell 设置为使用 emacs 命令。（Emacs 是一个编辑器，但目前你无需使用或熟悉它。）

- 2. 使用 shell 一段时间，切换目录、重定向输出或执行其他任务。

- 3. Ctrl P
使用 Ctrl P 召回上一条命令。表 3.2 显示了可用于在会话历史中导航的其他键盘组合。
在你完成召回并可选地编辑命令后，按 Enter（你不必位于行尾即可执行此操作）。

- 4. history
在 shell 提示符下输入 history 以查看你最近输入的命令列表（代码清单 3.13）。
注意每个命令旁边的命令编号。你可以输入 ! 空格键 和命令的编号来重新运行它。

### 提示

如果你使用 ksh，你可能希望将 set -o emacs 命令添加到你的个人配置文件中，这样你就不必在每个会话中手动输入该命令。有关编辑配置文件的具体信息，请参阅第 8 章。

## 在 csh Shell 中查看会话历史

如果你是 C 程序员（或有 C 程序员可以求助），csh 可能是一个不错的 shell，因为其语法与 C 编程语言非常相似。csh 不提供命令补全，但历史功能与 bash 或 zsh 相当相似（参见代码清单 3.14）。总体而言，csh 是一款功能强大的脚本 shell（也是可接受的交互式 shell），适合那些愿意花时间和精力熟悉它的人。

## 在 csh shell 中查看会话历史：

- 1. 如果尚未进行，请使用 shell 一段时间，切换目录、重定向输出或执行其他任务。
- 2. history
在 shell 提示符下输入 history 以查看你最近输入的命令列表。注意每条命令行的编号（代码清单 3.14）。
- 3. !10
输入 ! 后跟命令编号（中间无空格）以重新运行其中一条命令。在此示例中，我们重新运行命令 10。

### 提示

- 请参阅第 8 章，了解如何使 csh 更易用和更高效，特别是如果你没有其他 shell 选项可用。
- 你可以在会话历史中编辑命令。然而，对于 csh，重新输入命令远比编辑它们更容易。

```
xmision> history
1 ls
2 vi temp.info
3 ls
4 cd pub*
5 ls
6 cp *.pdf ..
7 cd ..
8 rm *.pdf
9 history
10 lynx
11 ftp ftp.wustl.edu
12 ls
13 vi .plan
14 finger ejr@roycomm.com
15 history
16 finger ejr@hobbes.roycomm.com
17 ls
18 pine
19 history
20 lynx
21 history
xmision> !10
```

代码清单 3.14 csh 也允许你按编号回收命令，尽管其他历史功能不可用。

- 如果你喜欢 csh，请检查你的系统上是否提供 tcsh。它与 csh 类似，但增加了命令补全和其他与 bash 相当的类似功能。
- 有时，历史长度默认设置为 0（不保留历史行）。如果你的历史似乎无法工作，请尝试 set history=100 以保存 100 行历史。将此添加到你的启动文件（下一章）中，如果你希望每次都可用。

## 使用 su 更改身份

偶尔，你可能需要使用除自己之外的用户 ID 登录，或需要重新使用自己的用户 ID 登录。例如，你可能想在注销前检查之前更改的配置设置是否有效。或者，如果你更改了 shell，你可能想在注销前检查它（顺便说一下，你应该这样做）。

你可以使用 su（substitute user）命令以其他用户身份登录（代码清单 3.15）或启动新的登录 shell。

```
[ejr@hobbes asr]$ ls
Projects testing
[ejr@hobbes asr]$ su asr
Password:
[asr@hobbes asr]$ ls
Projects testing
[asr@hobbes asr]$ su - ejr
Password:
[ejr@hobbes ejr]$ ls
Mail          editme        script2.sed
Projects      fortunes.copy scriptxtro.sed
Xrootenv.0    fortunes1.txt sedtest
above.htm     fortunes2.txt sorted_address.temp
address.book  groups        temp.htm
address.temp  history.txt   tempsport
axhome        html.htm      test
bogus         html.html     test2
chmod.txt     mail          testing.gif
clean         manipulate    testing.wp
compression   nsmail        typescript
[ejr@hobbes ejr]$ exit
[asr@hobbes asr]$ exit
[ejr@hobbes ejr]$ exit
```

代码清单 3.15 在一个用户和另一个用户之间来回切换（以及退出多个 shell）可能会有点令人困惑，但提示通常会告诉你你的身份和所在目录。

