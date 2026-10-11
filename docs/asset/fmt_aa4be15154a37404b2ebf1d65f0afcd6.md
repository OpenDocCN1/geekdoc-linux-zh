
| `zsh/mathfunc` | 额外的科学函数 |
| `zsh/pcre` | 扩展正则表达式库 |
| `zsh/net/socket` | Unix Domain套字支持 |
| `zsh/stat` | 访问 `stat` 系统调用以提供系统统计 |
| `zsh/system` | 各种底层系统功能的接口 |
| `zsh/net/tcp` | 访问 TCP 套字 |
| `zsh/zftp` | 特定的 FTP 客户端命令 |
| `zsh/zselect` | 文件描述符就绪时阻塞并返回 |
| `zsh/zutil` | 各种 shell 工具 |

`zsh` 模块涵盖了广泛的主题，从提供简单的命令行编辑功能到高级网络功能。`zsh` shell 的设计理念是提供一个基础的最小 shell 环境，让你根据需要添加完成编程任务所需的组件。

## 查看、添加和删除模块

`zmodload` 命令是 `zsh` 模块的接口。你使用此命令在 `zsh` shell 会话中查看、添加和删除模块。

不带任何命令行参数的情况下使用 `zmodload` 命令会显示当前 `zsh` shell 中已安装的模块：

```
% zmodload
zsh/zutil
zsh/complete
zsh/main
zsh/terminfo
zsh/zle
zsh/parameter
%
```

不同的 `zsh` shell 实现默认包含不同的模块。要添加新模块，只需在 `zmodload` 命令行指定模块名称即可：

```
% zmodload zsh/zftp
%
```

没有任何输出表示模块已加载。你可以执行执行 `zmodload` 命令，新模块应该会出现在已安装模块的列表中。

加载模块后，与该模块关联的命令将作为内置命令可用：

```
% zftp open myhost.com rich testing1
Welcome to the myhost FTP server.
% zftp cd test
% zftp dir
01-21-11 12:21PM 120823 test1
01-21-11 12:23PM 118432 test2
% zftp get test1 > test1.txt
% zftp close
%
```

`zftp` 命令允许你直接从 `zsh` shell 命令行进行完整的 FTP 会话！你可以将这些命令整合到 `zsh` shell 脚本中，直接从脚本执行文件传输。

要删除已安装的模块，请使用 `-u` 参数配合模块名：

```
% zmodload -u zsh/zftp
% zftp
zsh: command not found: zftp
%
```

## 注意事项

将 `zmodload` 命令放置在 `$HOME/.zshrc` 启动文件中是一个常见做法，这样你喜欢的函数就会在 `zsh` shell 启动时自动加载。

## 使用 zsh 脚本

`zsh` shell 的主要目的是为 shell 程序员提供一个高级的编程环境。考虑到这一点，`zsh` shell 提供了许多让 shell 脚本编写变得更容易的功能，这并不意外。

### 数学运算

正如你预期的，`zsh` shell 允许你轻松地执行数学函数。Korn shell 通过提供浮点数在支持数学运算方面一直处于地位。而 `zsh` shell 在所有的数学运算中都完全支持浮点数！

#### 执行计算

`zsh` shell 支持两种执行数学运算的方法：

- `let` 命令
- 双括号

当你使用 `let` 命令时，你应该将操作括括在双引号中以允许空格的存在：

```
% let value1="4 * 5.1 / 3.2 "
% echo $value1
6.375000000
%
```

注意，使用浮点数可能会引入精度问题。始终使用 `printf` 命令并指定显示答案所需的十进制精度是比较好的：

```
% printf "%6.3f\n" $value1
6.375
%
```

现在这样好多了！

第二种方法是使用双括号。这种方法结合了两种定义数学运算的技术：

```
% value1=$(( 4 * 5.1 ))
% (( value2 = 4 * 5.1 ))
% printf "%6.3f\n" $value2
20.400
20.400
%
```

注意，你可以将双括号放在操作周围（前面加一个美元符号 `$`），也可以放在整个赋值语句周围。两种方法产生相同的结果。

如果你没有预先使用 `typeset` 命令声明变量的数据类型，`zsh` shell 会尝试自动分配数据类型。当在同时处理整数和浮点数时，这可能是危险的。看这个示例：

```bash
% value1=10
% value2=$(( $value1 / 3 ))
% echo $value2
3
%
```

现在，这可能不是你想要计算出的结果。当你指定不带小数点的数字时，`zsh` shell 将其解释为整数值并执行整数计算。为了确保结果是浮点数：

```
% value1=10
% value2=$(( $value1 / 3 ))
% echo $value2
3.333333333
%
```

现在这样好多了！`zsh` shell 支持两种执行数学运算的方法：结果是 3.333333333。

## 注意事项

`zsh` 支持大量的函数。要查看所有函数的列表，请参阅 `zsh` 模块的手页。

### 结构命令

`zsh` shell 提供了常用的结构命令：

- `if-then-else` 语句
- `for` 循环（包括 C 风格）
- `while` 循环
- `until` 循环
- `select` 语句
- `case` 语句

`zsh` shell 还包含一个不同的命令 `repeat`。`repeat` 命令使用以下格式：

```
repeat param
do
  commands
done
```

`param` 参数必须是一个数字或计算为次数的数学运算。`repeat` 命令按指定的次数执行命令：

```
% cat test1
#!/bin/zsh
# using repeat command
value=$(( 10 / 2 ))
repeat $value
do
  echo "This is a test"
done
$ ./test1
This is a test
This is a test
This is a test
This is a test
%
```

该命令允许你根据计算重复代码段。

### 函数

`zsh` shell 支持使用 `function` 命令或通过带括号定义函数名来创建自己的函数：

```
% function funct1 {
> echo "This is the test1 function"
}
% funct2() {
> echo "This is the test2 function"
}
% funct1
This is the test1 function
% funct2
This is the test2 function
%
```

与 `bash` shell 函数（见第 17 章）一样，你可以在 shell 脚本中定义函数，然后使用全局变量或向函数传递参数。

# 第四部分

# 创建实用的脚本

## 本部分内容

- 1. 第 24 章 编写简单的脚本工具
- 2. 第 25 章为数据库、网页和电子邮件制作脚本
- 3. 第 26 章 创建有趣的 Shell 脚本

# 第 24 章

编写简单的脚本工具

## 本章内容

- 1. 自动化备份
- 2. 管理用户账户
- 3. 监控磁盘空间

没有什么比为 Linux 系统管理员编写脚本工具更能让 shell 脚本编程发挥价值了。典型的 Linux 系统管理员每天都有许多各种工作要处理，从监控磁盘空间到备份重要文件，再到管理用户账户。Shell 脚本工具可以让这些任务变得简单得多！本章将演示你在 `bash` shell 中编写脚本工具的一些能力。

# 执行归档

无论你是负责商业环境中的 Linux 系统，还是只是在家里使用，数据丢失都可能是灾难性的。为了防止坏事的发生，定期进行备份（或归档）总是一个好主意。

然而，好主意和可行性是两回事。尝试安排一个备份计划来存储重要文件可能是一项挑战。这是 shell 脚本经常派上用场的地方。

本节演示了使用 shell 脚本在你的 Linux 系统上归档数据的两种方法。

# 归档数据文件

如果你在使用 Linux 系统处理某个重要项目，可以创建一个 shell 脚本来自动对特定目录创建快照。在配置文件中指定这些目录允许你在特定项目发生变化时更改它们。这有助于避免从主归档中进行耗时的恢复过程。

本节将展示如何创建一个自动化的 shell 脚本，它可以对指定的目录创建快照，并保留你的数据历史版本的归档。

# 获取所需的函数

Linux 世界中归档的主力是 `tar` 命令（见第 4 章）。`tar` 命令用于将整个目录归档为一个文件。这里使用 `tar` 命令创建工作目录归档文件的示例：
