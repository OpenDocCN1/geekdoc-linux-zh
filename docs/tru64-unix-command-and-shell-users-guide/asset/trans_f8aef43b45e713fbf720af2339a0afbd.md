

## 表 8-7：内置 C Shell 命令（续）

| 命令 | 描述 |
|---|---|
| unset | 删除已分配给变量的值。ᵈ |
| unsetenv | 删除已分配给环境变量的值。ᵈ |

ᵃ 有关 alias 和 unalias 命令的更多信息，请参见第 8.2.5 节。
ᵇ 有关 bg、fg 和 jobs 命令的更多信息，请参见第 6 章。
ᶜ 有关 history 命令的更多信息，请参见第 8.2.3 节。
ᵈ 有关 set、setenv、unset 和 unsetenv 命令的更多信息，请参见第 7 章。
ᵉ 有关 source 命令的更多信息，请参见第 8.2.5 节。

## 8.3 Bourne Shell 特性

本节描述以下 Bourne shell 特性：

- 示例 .profile 登录脚本
- 元字符
- 内置变量
- 内置命令

### 8.3.1 示例 .profile 登录脚本

如果你的登录 shell 是 Bourne shell，操作系统会执行 .profile 登录脚本来设置你的环境。

.profile 登录脚本中导出的变量会传递给创建的任何子 shell 和子进程。未导出的变量仅由登录 shell 使用。

在下面的 .profile 登录脚本中，shell 变量被设置并导出，为注销脚本设置了 trap，并指示系统显示信息。表 8-8 解释了脚本的每个部分。

```
# Set PATH
PATH=/usr/bin:/usr/local/bin:
# Export global variables
export PATH
# Set shell variables
PS1='$LOGNAME $ '
CDPATH=.:..:$HOME
# Set up for logout script
trap "echo logout; $HOME/.logout" 0
# Display status information
date
echo "Currently logged in users:" ; users
```

## 表 8-8：示例 Bourne Shell .profile 脚本

| 命令 | 描述 |
|---|---|
| 设置搜索路径 | |
| PATH=/usr/bin:/usr/local/bin: | 指定搜索路径。在此情况下，首先搜索 /usr/bin，其次搜索 /usr/local/bin。 |
| 导出搜索路径 | |
| export PATH | 指定搜索路径应传递给你执行的全部命令。 |
| 设置 Shell 变量 | |
| PS1='\$LOGNAME $ ' | PS1 变量指定 Bourne shell 提示符，其默认值是 $。然而，此变量赋值指定你的提示符应更改为以下内容：用户名 $。例如，如果你的用户名是 amy，你的提示符将如下所示：amy $。 |
| CDPATH=.:.:$HOME | CDPATH 变量设置 cd 命令的搜索路径。此变量赋值指定 cd 命令应首先在当前目录 (.) 中搜索命名目录，其次在父目录 (..) 中搜索，第三在主目录 ($HOME) 中搜索。 |
| 设置注销脚本 | |
| trap "echo logout; $HOME/.logout" 0 | 指定当 trap 命令捕获退出信号 (0) 时，你的 shell 应显示 logout 并执行你的 .logout 脚本。a |
| 显示状态信息 | |
| date | 显示日期和时间。 |
| a 有关 trap 命令的更多信息，请参见第 7.9.1 节。 |

### 8.3.2 元字符

表 8-9 描述了 Bourne shell 元字符（对 shell 具有特殊含义的字符）。这些元字符的含义按其在 shell 脚本中出现时的解释、在文件名规范中、在用于引用其他字符时、在输入/输出规范中，或在用于指示变量替换时进行分组。

## 表 8-9：Bourne Shell 元字符

| 元字符 | 描述 |
|---|---|
| 语法 | |
| | | 分隔管道的一部分的命令。 |
| && | 如果当前命令成功，则运行下一个命令。 |
| || | 如果当前命令失败，则运行下一个命令。 |
| : | 分隔应顺序执行的命令。 |
| ;; | 分隔 case 构造的元素。 |
| & | 在后台运行命令。 |
| ( ) | 将命令分组以在子 shell 中作为单独进程运行。 |
| 文件名 | |
| / | 分隔文件路径名的各部分。 |
| ? | 匹配除前导点 (.) 外的任意单个字符。 |
| * | 匹配除前导点 (.) 外的任意字符序列。 |
| [ ] | 匹配所包含的任意字符。 |
| 引用 | |
| \ | 指定以下字符应按字面解释；即，不具有 shell 的特殊含义。 |
| '...' | 指定所包含的任意字符（除 ' 引号字符外）应按字面解释；即，不具有 shell 的特殊含义。 |
| "..." | 提供一种特殊的引用形式。指定 $ （美元符号）、` （重音符）和 \ （反斜杠）字符保持其特殊含义，而所有其他所包含字符均按字面解释；即，不具有 shell 的特殊含义。双引号在进行变量赋值时很有用。 |
| 输入/输出 | |
| < | 重定向输入。 |
| > | 将输出重定向到指定文件。 |
| << | 重定向输入并指定 shell 应读取输入直到指定行。 |
| >> | 重定向输出并指定 shell 应将输出添加到文件末尾。 |
| 2> | 将诊断输出重定向到指定文件。 |
| 替换 | |

