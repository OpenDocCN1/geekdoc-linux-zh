
- Shell 脚本内部可以使用决策结构，根据用户输入或某个命令的结果来执行特定的 Linux 命令。

## 核心术语

- 一种 shell 元字符，用于将一个命令的标准输出管道到另一个命令的标准输入。
- 一种 shell 元字符，用于从文件获取标准输入。
- 一种 shell 元字符，用于将标准输出和标准错误重定向到文件。
- `alias` `command` — 用于创建特殊变量的命令，这些变量是长命令字符串的快捷方式。
- `awk` `command` — 一种用于搜索和显示文本的过滤命令。
- `decision construct` 决策结构——shell 脚本中使用的特殊结构，根据命令的结果或变量的内容改变程序的执行流。常见的决策结构包括 `if`、`case`、`&&` 和 `|`。
- `echo` `command` — 用于在终端屏幕上显示或回显输出的命令。它可以使用转义序列。
- `env` `command` — 用于显示当前 shell 中存在的导出变量列表（特殊变量除外）的命令。
- `environment files`——环境变量文件——登录后立即加载以执行命令的文件；它们通常用于将变量加载到内存中。
- `environment variables`——环境变量——存储系统或在系统上运行的进程通常访问信息的变量——这些变量共同构成了用户环境。
- `escape sequences`——转义序列——在命令内部具有特殊含义的字符序列。它们以反斜杠 `\` 开头。
- `export` `command` 用于将变量发送到子 shell 的命令。
- `file descriptors` 文件描述符——用于定义命令输入和输出的数字标签。
- `filter command` 过滤命令——可以从标准输入接收并发送到标准输出的命令。换句话说，过滤器可以是管道中间的命令。
- `grep (Global Regular Expression Print)` `command`——用于在一个或多个文件中搜索所需的字符字符串的程序。
- `hashbang`——shell 脚本的第一行，定义了将用于解释脚本文件中命令的 shell。
- `pipe` 管道——由 `|` 元字符连接的命令字符串。
- `read` `command`——用于从用户处读取标准输入并存入变量的命令。
- `redirection` 重定向——改变输入、标准输出和标准错误默认位置的过程。
- `sed` `command`——用于搜索和处理文本的过滤命令。
- `set` `command`——用于查看 shell 中所有变量（特殊变量除外）的命令。
- `shell scripts` shell 脚本——包含 shell 按顺序执行的命令列表或结构的文件。
- `sort` `command` 用于对文件中的行排序的命令。
- `Standard Error (stderr)` 标准错误——代表命令生成的任何错误信息的文件描述符。

## 复习题 365

`Standard Input (stdin)` 标准输入——代表执行期间输入到命令中的信息的文件描述符。

`Standard Output (stdout)` 标准输出——代表命令的预期输出的文件描述符。

`subshell` 子 shell——由当前 shell 启动的 shell。

`tee` `command` 命令用于从标准输入接收内容并将其同时发送到标准输出和指定文件的命令。

`test` `statement` 测试语句——用于测试特定条件并生成真/假（True/False）值的语句。

`tr` `command` 用于转换或更改从标准输入接收的字符。

`user-defined variables` 用户定义变量——由用户创建且系统使用的变量。这些变量通常被导出到子 shell。

`variable` 变量——用于存储信息的内存区域。变量在环境变量文件中创建，并在注销时销毁。

`variable identifier` 变量标识符——变量名。

## 复习题

1. 标准错误和标准输出可以重定向到文件。对/错？

2. `alias` 命令可以用于创建命令字符串的快捷方式。对/错？

3. 以下哪个文件在登录后总是执行？

a. `/etc/profile`

b. `~/.bash_profile`

c. `~/.bash_login`

d. `~/.profile`

4. 使用什么命令可以查看环境变量列表及其值？

a. `/var`

b. `env`

c. `set`

d. `echo`

5. 如何在 shell 脚本中指示注释？

a. `!`

c. `!`

d. `#`

6. `if` 结构以什么开头并以什么结束？

a. `end`

b. `endif`

c. `stop`

d. `fi`

7. 以下哪个会在命令执行成功时显示消息？

a. `cd /home`

b. `echo "home"`

c. `cd ||`

8. 哪些可以显示 `HOME` 的当前值？（多选）

a. `echo=`

b. `echo ~`

c. `echo $HOME`

d.

9. 哪个文件描述符代表 `stdout`？

a. `2`

b. `0`

c. `1`

d. `3`

10. 以下哪个运算符可以反转 `test`？

a. `#!`

b. `-o`

c. `-a`

d. `!`

11. 使用 `alias` 命令为 `cat` 创建快捷方式会有什么影响？

a. There is already a variable with cat.

b. It cannot be done because there already is a command on the system.

c. When you use the cat command at the command prompt with the intention of viewing a text file, the date appears instead.

d. There is no effect until the alias is imported because it is a user-defined variable.

12. a. shell 脚本中的注释行。

b. `#!`

c. `!`

d. `#`

13. 你将标准错误重定向到一个名为 `Errors` 的文件。之后查看内容发现六个错误消息。重复操作后，你发现文件中只有两个。为什么？

a. 打开文件后内容丢失。

b. 系统产生了不同的标准输出。

c. 你没有将标准错误追加到 `Error` 文件，因此在第二次运行时它被覆盖了。

d. 你每次重定向都必须指定新文件。

14. `sed` 和 `awk` 命令是用于格式化管道中命令的过滤命令。

15. 命令字符串 `ls /etc/hosts >listoffile` 有什么问题？

a. 无问题。

b. 文件描述符未定义；除非指示 `1` 表示标准输出或 `2` 表示标准错误，否则命令将失败。

c. `ls` 是不可与重定向配合命令之一。你必须使用 `|` 管道。

d. 文件 `listoffile` 将始终包含标准错误，因为未定义文件描述符。

16. 以下哪些并非系统上每个命令都会生成？（多选）

a. 标准输入

b. 标准差

c. 标准输出

d. 标准错误

17. 在 shell 脚本可以使用哪种结构来读取标准输入（Standard Input）并将其放入变量？

- a. `read`
- b. `sum`
- c. `verify`
- d. `test`

18. 变量标识符必须____________________ ： 

a. 不以数字开头

b. 不以大写字母开头

c. 以数字开头

d. 以下划线 “_ ”开头

19. 在命令行执行命令后输入 `>>` 起什么作用？

a. 它将标准错误和标准输出都重定向到相同的位置。

b. 它没有起到任何作用。

c. 它将标准错误和标准输入重定向到相同的位置。

d. 它将标准输出追加到文件中。

20. 考虑以下 shell 脚本：

```bash
echo -e "What is your favorite color?--> \c"
read REPLY
if [ "$REPLY" = "red" -o "$REPLY" = "blue" ]
then
  echo "The answer is red or blue."
else
  echo "The answer is not red nor blue."
fi
```

21. 如果用户执行问题 20 中的程序并在收到提示时回答 Blue，会显示什么？

a. The answer is red or blue.

b. The answer is not red nor blue.

c. 代码会导致错误。

d. The answer is red or blue. The answer is not red nor blue.

## 动手项目

这些项目应该按照给出的顺序完成。本章介绍的动手项目总共需要三小时来完成。本实验的要求包括：

- 一台根据动手项目 7-2 安装了 Red Hat Fedora Core 2 的计算机。

# 项目 8-1
