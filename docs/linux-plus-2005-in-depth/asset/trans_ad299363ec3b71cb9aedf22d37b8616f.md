

```bash
u | U ) echo -e "\nThe people logged into the system include:"
    who
    ;;
    r | R ) echo -e "\nThe contents of the / directory are:"
    ls -F /
    ;;
    * ) echo -e "Invalid choice! \n"
    ;;
esac
```

```text
[root@server1 root]$ ./myscript
What would you like to see?
Todays date (d)
Currently logged in users (u)
The contents of the / directory (r)

Enter your choice(d/u/r)- > d
Today's date is: Sat Jun 4 11:33:23 EDT 2005
[root@server1 root]$ _
```

前述示例通过菜单提示用户，并允许用户选择一项，该项随后被放入 ANSWER 变量中。如果 ANSWER 变量等于字母 "d" 或 "D"，则执行 date 命令；但是，如果 ANSWER 变量等于字母 "u" 或 "U"，则执行 who 命令，如果 ANSWER 变量等于字母 "r" 或 "R"，则执行 ls 命令。如果 ANSWER 变量包含上述字母以外的内容，则 * 通配元字符会匹配它并向屏幕打印错误消息。与 if 结构一样，shell 脚本中位于 case 结构之后的任何语句都会在 case 结构执行完毕后执行。

## && 和 || 结构

虽然 if 和 case 结构非常灵活，但当在执行程序过程中只需要做一个决定时，有一些快捷结构可以节省时间；这些结构就是 `&&` 和 `||`。这些结构的语法如下所示：

```bash
command && command

command || command
```

对于前述 `&&` 语法，`&&` 结构右侧的命令仅当左侧命令成功完成时才执行。对于 `||` 语法则相反；`||` 结构右侧的命令仅当左侧命令未成功完成时才执行。

考虑之前使用过的 `testmkmkdir` 示例：

```bash
[root@server1 root]# cat testmkmkdir
#!/bin/bash
if mkdir /etc/sample
then
    cp /etc/hosts /etc/sample
    echo "The hosts file was successfully copied to /etc/sample"
else
    echo "The /etc/sample directory could not be created."
fi
[root@server1 root]# _
```

你可以考虑使用 `&&` 结构重写上述 shell 脚本如下：

```bash
[root@server1 root]# cat testmkmkdir
#!/bin/bash
mkdir /etc/sample && cp /etc/hosts /etc/sample
[root@server1 root]# _
```

上述 shell 脚本创建目录 `/etc/sample`，并且只有当 `mkdir /etc/sample` 命令成功时才将 `/etc/hosts` 文件复制到其中。相反，你可以使用 `||` 结构来生成错误消息，以防其中某个命令未能正确执行：

```bash
[root@server1 root]# cat testmkmkdir
#!/bin/bash
mkdir /etc/sample || echo "Could not create /etc/sample"
cp /etc/hosts /etc/sample || echo "Could not copy /etc/hosts"
[root@server1 root]# _
```

## 章节总结

- 命令有三个可用组件：标准输入、标准输出和标准错误。并非所有命令都使用每个组件。
- 标准输入通常是从键盘获取的用户输入，而标准输出和标准错误默认发送到终端屏幕。
- 你可以使用重定向符号将命令的标准输出和标准错误重定向到文件。同样，你也可以使用重定向符号将文件重定向到命令的标准输入。
- 要将一个命令的标准输出重定向到另一个命令的标准输入，你必须使用管道符号。
- BASH shell 中可用的大多数变量都是在登录后从环境文件加载到内存中的环境变量。
- 你可以在 BASH shell 中创建自己的变量并导出它们，使它们可用于由 shell 启动的程序。这些变量也可以放置在环境文件中，以便在每次 shell 登录时加载到内存中。
- UMASK 变量和命令别名是使用特定命令设置的特殊变量。
- shell 脚本可用于执行多个 Linux 命令。
- 决策结构可用于 shell 脚本中，根据用户输入或某个命令的结果来执行特定的 Linux 命令。

## 关键词

| 术语 | 定义 |
| :--- | :--- |
| `\|` | 用于将一个命令的标准输出管道传输到另一个命令的标准输入的 shell 元字符。 |
| `<` | 用于从文件获取标准输入的 shell 元字符。 |
| `>` | 用于将标准输出和标准错误重定向到文件的 shell 元字符。 |
| **alias 命令** | 用于创建作为较长命令字符串快捷方式的特殊变量的命令。 |
| **awk 命令** | 用于搜索和显示文本的过滤命令。 |
| **decision 结构** | 在 shell 脚本中使用的特殊结构，根据命令结果或变量内容改变程序流程。常见的决策结构包括 if、case、&& 和 ||。 |
| **echo 命令** | 用于在终端屏幕上显示或回显输出的命令。它可能会使用转义序列。 |
| **env 命令** | 用于显示当前 shell 中存在的已导出变量列表（不包括特殊变量）的命令。 |
| **环境文件** | 登录后立即用于执行命令的文件；通常用于将变量加载到内存中。 |
| **环境变量** | 存储系统或系统上运行的程序通常访问的信息的变量——这些变量共同构成用户环境。 |
| **转义序列** | 在 echo 命令中具有特殊含义的字符序列。它们以 \ 字符作为前缀。 |
| **export 命令** | 用于将变量发送到子 shell 的命令。 |
| **文件描述符** | 用于定义命令输入和命令输出的数字标签。 |
| **filter 命令** | 可以从标准输入获取数据并发送到标准输出的命令。换句话说，过滤命令是可以存在于管道中间的命令。 |
| **grep (全局正则表达式打印) 命令** | 用于在一个或多个文本文件中搜索所需字符字符串的程序。 |
| **哈希** | shell 脚本的第一行，定义了将用于解释脚本文件中命令的 shell。 |
| **管道** | 由 `\|` 元字符连接起来的命令字符串。 |
| **read 命令** | 用于从用户读取标准输入到变量中的命令。 |
| **重定向** | 更改标准输入、标准输出和标准错误的默认位置的过程。 |
| **sed 命令** | 用于搜索和处理文本的过滤命令。 |
| **set 命令** | 用于查看 shell 中所有变量（不包括特殊变量）的命令。 |
| **shell 脚本** | 包含 shell 按顺序执行的命令或结构列表的文本文件。 |
| **sort 命令** | 用于对文件中行进行排序的命令。 |
| **标准错误 (stderr)** | 表示命令生成的任何错误消息的文件描述符。 |
| **标准输入 (stdin)** | 表示执行过程中输入到命令的信息的文件描述符。 |
| **标准输出 (stdout)** | 表示命令所需输出的文件描述符。 |
| **子 shell** | 由当前 shell 启动的 shell。 |
| **tee 命令** | 用于从标准输入获取数据并发送到标准输出和指定文件的命令。 |
| **test 语句** | 用于测试特定条件并生成 True/False 值的语句。 |
| **tr 命令** | 用于转换或更改从标准输入接收的字符的命令。 |
| **用户定义变量** | 由用户创建且不被系统使用的变量。这些变量通常导出到子 shell 中。 |
| **变量** | 用于存储信息的内存区域。变量在登录后创建 shell 时从环境文件中的条目创建，并在登出时 shell 销毁时被销毁。 |
| **变量标识符** | 变量的名称。 |

