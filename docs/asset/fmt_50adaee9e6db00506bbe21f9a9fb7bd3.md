
如果 `echo -n` 没有被正确解析，它将直接输出文本 `-n`，在这种情况下 `$n` 被设置为空字符串，而 `$c` 被设置为 `\c`。否则，执行相反操作，将 `$n` 设置为 `-n`，而 `$c` 设置为空字符串。

我们在上面已经展示了简单但有效的 `cut` 命令的用法。我们在这里将讨论一些更常用的外部程序的示例。

`grep` 是 shell 脚本程序员一个极其有用的工具。`grep` 的示例如下：

```sh
#!/bin/sh

grep "pattern" file
```

`sed s/eth0/eth1/g file1 > file2` 将 `file1` 中所有的 `eth0` 更改为 `eth1`。如果我们只更改一个单独字符，`tr` 会是更合适的工具，因为它体积更小，加载速度更快。`tr` 无法做的另一件事是：从文件中删除字符：

```
echo ${SOMETHING} | sed s/"bad word"//g
```

这会从变量 `${SOMETHING}` 中删除短语 `"bad word"`。你可能会想：“但是 `grep` 也能做到这一点！”——`grep` 只处理整行。请考虑以下文件：

This line is okay.
This line contains a bad word. Treat with care.
This line is fine, too.

`grep` 会删除整个第二行，只留下一个两行的文件；而 `sed` 则会将文件内容更改为：

This line is okay.
This line contains a . Treat with care.
This line is fine, too.

## Telnet 提示

这是我从 Sun 的 Explorer 工具中学会的一个实用技巧。虽然服务器上不再使用 telnet，但某些网络设备（如终端集中器等）仍在使用它。通过创建一个像这样的脚本（你自己的脚本，或从命令行），你可以运行：

```
$ ./telnet.sh | telnet
```

我曾几个人问过我这个问题，我倾向于引导他们使用 `expect` 代码包，那套代码非常复杂且臃肿；这段代码在不同系统之间具有很好的移植性（只要它们支持 `egrep`）。如果它在你的系统上不起作用，请尝试使用带有 `-q` 参数的 `grep`，或者使用特定的 `grep` 并重定向到 `/dev/null`。尽管这比安装 `expect` 要简单得多。

### telnet1.sh²⁸

```bash
#!/bin/sh

host=127.0.0.1

port=23

login=steve

asswd=hellothere

cmd="ls /tmp"

echo ${host} ${port}

sleep 1

echo ${login}

sleep 1

echo ${passwd}

sleep 1

echo ${cmd}

sleep 1

echo exit
```

然而，Sun 添加了一些巧妙的错误检查代码（注意：你可以从当前的 shell 或脚本中设置并导出变量，以避免将密码存储在明文文件中）：

```
$ ./telnet2.sh | telnet > file
```

### telnet2.sh²⁹

- 28 telnet1.txt
- 29 telnet2.txt

```bash
#!/bin/sh

## telnet2.sh | telnet > FILE1

host=127.0.0.1

port=23

login=steve

passwd=hellothere

cmd="ls /tmp"

timeout=3

file=file1
```

```bash
echo open ${host} ${port}

sleep 1

tout=${timeout} 2

while [ "${tout}" -ge 0 ]

do

  if tail -1 "${file}" 2>/dev/null | \
    egrep -e "${login}" > /dev/null

    then

      echo "${login}"

      sleep 1

      tout=-5

      continue

  else

    sleep 1

    tout=`expr ${tout} - 1`

  fi

done
```

```bash
if [ "${tout}" -ne "-5" ]; then

  exit 1

fi

out=${timeout}

while [ "${tout}" -ge 0 ]

do

  if tail -1 "${file}" 2>/dev/null | \
    egrep -e "Password:" > /dev/null

    then

      echo "${password}"

      sleep 1

      tout=-5

      continue

  else

if tail -1 "${file}" 2>/dev/null | \
eegrep -e "${prompt}" > /dev/null

then

    tout=-5

else

    sleep 1

    tout=`expr ${tout} - 1`

fi

done

if [ "${tout}" -ne "5" ]; then

    exit 1

fi

> ${file}

echo ${cmd}

sleep 1

echo exit
```

注意，在这个版本中，输出被捕获到 `file1` 中，并且脚本实际上使用了该文件来检查进度。我添加了 `> ${file}`，以便进入文件的输出仅为命令的输出，而不包含登录过程。

## 15. 快速参考

这是一个关于某些不太容易猜的命令和代码含义的快速参考指南。

| 命令 / 变量 / 语法结构 | 说明 | 示例 |
| --- | --- | --- |
| & | 在后台运行上一个命令 | ls & |
| && | 逻辑与 | if [ "$foo" -ge "0" ] && [ "$foo" -le "9" ] |
| \| | 逻辑或 | if [ "$foo" -lt "0" ] \| [ "$foo" -gt "9" ] (在 Bourne shell 中不支持) |
| ^ | 行首 | grep "^foo" |
| $ | 行尾 | grep "foo$" |
| = | 字符串相等（对比 -eq） | if [ "$foo" = "bar" ] |

| 命令 / 变量 / 语法结构 | 说明 | 示例 |
| --- | --- | --- |
| ! | 逻辑非 | if [ "$foo" != = "bar" ] |
| $$ | 当前 shell 的进程 ID (PID) | echo "my PID = $$" |
| \|$ | 上一个后台命令的 PID | ls & echo "PID of ls = \$!" |
| $? | 上一个命令的退出状态 | ls ; echo "ls returned code \$?" |
| $0 | 当前命令的名称（按调用方式） | echo "I am \$0" |
| $1 | 当前命令的第一个参数 | echo "My first argument is \$1" |
| $9 | 当前命令的第九个参数 | echo "My ninth argument is \$9" |
| $@ | 当前命令的所有参数（保留空格） | echo "My arguments are \$@" |

| 命令 / 变量 / 语法结构 | 说明 | 示例 |
| * | 引用) | | |
| $* | 当前命令的所有参数（不保留空格和引号） | echo "My arguments are $*" |
| -eq | 数值相等 | if [ "$foo" -eq "9" ] |
| -ne | 数值不相等 | if [ "$foo" -ne "9" ] |
| -lt | 小于 | if [ "$foo" -lt "9" ] |
| -le | 小于或等于 | if [ "$foo" -le "9" ] |
| -gt | 大于 | if [ "$foo" -gt "9" ] |
| -ge | 大于或等于 | if [ "$foo" -ge "9" ] |
| -z | 字符串为空 | if [ -z "$foo" ] |
| -n | 字符串不空 | if [ -n "$foo" ] |

## 16. 交互式 Shell

这里是关于交互式使用的一些快速提示。我个人在大多数情况下推荐 `bash` shell。你可以通过添加历史记录来让 `ksh` 更好用，可以使用 `vi` 或 `emacs`。有多种方法可以实现，取决于具体情况：`set -o vi`、`ksh -o vi`，或者 `exec ksh -o vi`（如果你更喜欢 emacs 模式，可以将 "vi" 替换为 "emacs"）。

如果你想从另一个交互式 shell 启动 `ksh`，可以像这样调用 `ksh`：

```
csh% # 噢，那是 csh！
csh% ksh
ksh$ 噢，那好多了
ksh$ # 在 ksh 下操作
ksh$ # 回到 csh 提示符：
ksh$ exit
```

这将启动一个新的 `ksh` 会话，你可以退出并返回到之前的 shell。或者，你可以使用 `exec` 命令将 `csh`（或任何 shell）替换为 `ksh` shell：

```csh% # 噢，那是 csh！
csh% exec ksh
ksh$ # 在 ksh 下操作
ksh$ exit
```

这里的区别在于你无法找回 `csh` 会话。

好用的地方是历史记录：

```
csh% ksh
ksh$ set -o vi
ksh$ # 现在你可以用 vi 编辑历史记录了
```

如果你按下 `ESC` 然后按 `k`，通过重复按 `k` 就可以回溯命令历史。你可以使用 `vi` 命令模式和输入模式命令来编辑命令，例如：

```
ksh$ touch foo
ESC-k (进入 vi 模式，显示上一个命令)
w (跳到下一个单词，从 "touch" 跳到 "foo")nww (修改单词)bar (将 "foo" 改为 "bar")
ksh$ touch bar
```

## 17. 练习

我认为这个简单的练习可能对衡量你的 Shell 脚本编写水平很有帮助……

- 通讯录
- 目录遍历

### 通讯录

好了，虽然这看起来很无聊，但这是你今天的练习题：使用 `bourne` 或 `bourne-again` shell 创建一个通讯录程序。它应该使用函数来执行所需的任务。该程序应该是基于菜单的，允许提供以下选项：

- 搜索通讯录
- 添加条目
- 删除 / 编辑条目

你还需要一个“显示”函数，在选择时显示单条或多条记录。

#### 搜索

当用户搜索“Smith”时，脚本应该识别并显示所有包含“Smith”的记录。搜索是仅针对姓氏还是整条记录，由你决定。

#### 添加

输入数据（姓名、姓氏、电子邮件、电话等）。如果看起来是重复的，为了获得加分，可以提供编辑现有记录`get`。在用户确认后将记录保存到数据文件中。

#### 删除

输入搜索标准，将其缩小到一条，确认，然后删除该记录。

#### 编辑

操作与删除相似，但使用现有记录作为默认输入。例如，如果你只想更改 John Smith 的电话号码，界面可能像这样：

```
Name [ John Smith ]
Phone [ 12345 ] 54321
Email [ joe@smith.org.uk ]
```

删除旧记录并添加新记录。或者，直接编辑现有记录，尽管这可能更困难。

#### 加分项

- 允许取消选项（使用“特殊”条目如 `^d`, `CR`, `^c` 等）
- 添加“确认”选项。
- 提供交互式/非交互式模式（即基于菜单的版本和基于命令行 (CLI)的版本）。
- 在 CLI 版本中尝试 `getopt`。

#### 提示 / 需要思考的问题

我提供了一个答案在下方；除非你卡住了否则不要看！主文件：`addressbook/addr.sh.txt` 库文件：`addressbook/addr_libs.sh.txt`

### 目录遍历

创建一个 Shell 脚本来遍历文件系统树。

示例答案在此：

`directories`

Shell 脚本教程
第 95 页

## 其他资源链接

这些是互联网上可以找到的许多有用资源中的极少数：

Steve Bourne 的《Unix Shell 简介》。
https://steve-parker.org/sh/bourne.shtml

关于引号和转义字符的非常权威文档
http://www.mpi-inf.mpg.de/departments/rg1/teaching/unixffb-ss98/quoting-guide.html

编写可移植 Shell 脚本时需要注意什么。
http://archive09.linux.com/articles/34658

Unix 罗塔石：
http://bhami.com/rosetta.html

## 感谢！

感谢你购买这本书并一直读到最后！我希望这本书对你是有用的、信息丰富的且有帮助的。

书籍需要评价来让潜在读者了解他们将获得什么。请考虑花五秒钟在 Amazon 上为本电子书打分，甚至撰写一段评论——无论长短随意，一句话或几个段落都可以。

你可能想提到的点：

- 这本书适合什么人群，
- 你从书中收获了什么，
- 你觉得写作风格如何，
- 你预计未来会再次重阅书的某些部分，
- 这对你来说是否是有效的时间利用，

http://amzn.com/B0C2EGNSA – 或直接在 Amazon 上搜索“Shell Scripting Tutorial”

## 600 页的书

本教程的作者 Steve Parker 编写编写了一本完整的书；由 Wrox 出版，书籍《Shell Scripting: Expert Recipes for Linux, Bash and more》在所有优质零售商处买到。ISBN 1118024486。建议零售价 $49.99。Kindle 同样可用：

http://steve-parker.org/book/ 包含详情；书籍可以在在线和实体店购买。

Steve Parker 还写了《How to Build a LAMP Server》，详细介绍了 LAMP 栈的安装以及在其之上构建运行的应用程序，包括 MySQL 配置、phpMyAdmin 的使用和 PHP 开发。该书目前仅在 Amazon 以电子书形式出售；搜索“B00DAI6IATO”或“How to Build a LAMP Server”。

请访问 http://steve-parker.org/publications/ 获取最新信息。

这是一门学习使用 Unix shell 的 Bourne Shell 编程/脚本教程。通过示例结合理论来学习 Linux / Unix shell 脚本。我们将让你很快掌握 Unix shell 脚本编写！

这本详尽且实用的教程贯穿了示例，是根据该内数百名学生和专业人士的广泛反馈编写的，无论他们是否具有 Unix 或 Linux 背景。

![](img/84a50f94dfcd1da09f623b014d3ee18c_103_0.png)
