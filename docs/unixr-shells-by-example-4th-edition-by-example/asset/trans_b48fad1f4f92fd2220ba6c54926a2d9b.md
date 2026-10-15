

## EXPLANATION (CONTINUED)

9 foreach 循环由一个列表组成，该列表是通过使用命令替换 `cat $guestfile` 创建的。cat 命令的输出将从文件中创建一个客人列表。对于客人名单上的每个人，除了 root 用户，将会创建一个邮件消息，邀请该人参加在指定地点和时间举行的聚会，并要求他或她带一份清单上的食物之一。

10 条件测试变量 person 的值是否与单词 root 匹配。如果匹配，continue 语句会使控制立即返回到循环顶部（而不是执行任何进一步的语句）。然后 foreach 将处理列表中的下一个单词。

11 邮件消息是在所谓的 here document 中创建的。从用户定义的单词 FINIS 到最后的 FINIS 的所有文本都将被发送到邮件程序。foreach 循环遍历名字列表，执行从 foreach 到关键字 end 的所有指令。

12 FINIS 是一个用户定义的终止符，用于结束 here document，该文档由电子邮件正文组成。

13 发送消息后，食物列表会通过 shift 命令向左移动，以便客人名单上的下一个人将获得列表中的下一个食物项目。

14 如果食物列表为空，它将被重置，以确保任何额外的客人都会被指示带一份食物。

15 这标志着循环语句的结束。

## 2.4 The Bourne Shell Syntax and Constructs

Bourne shell 的基本语法和结构列在表 2.2 中。

## Table 2.2 Bourne Shell Syntax and Constructs

| The shbang line | “shbang” 行是脚本的第一行，让内核知道将解释脚本中各行的 shell 是什么。shbang 行由 #! 加上 shell 的完整路径名组成，并且可以跟随选项来控制 shell 的行为。 |
| **EXAMPLE** | `#!/bin/sh` |
| Comments | 注释是以 # 号为前缀的描述性材料。它们一直有效到行尾，并且可以在行的任何位置开始。 |
| **EXAMPLE** | `# this text is not` `# interpreted by the shell` |

## Table 2.2 Bourne Shell Syntax and Constructs (continued)

| Wildcards | 有一些字符会被 shell 以特殊方式求值。它们被称为 shell 元字符或“通配符”。这些字符既不是数字也不是字母。例如，*, ?, 和 [ ] 用于文件名扩展。 <, >, 2>, >>, 和 | 符号用于标准 I/O 重定向和管道。为了防止这些字符被 shell 解释，它们必须被引用。 |
| **EXAMPLE** | 文件名扩展：rm *; ls ??; cat file[1-3]; 引号保护元字符：echo "How are you?" | |
| Displaying output | 要将输出打印到屏幕，使用 echo 命令。通配符必须使用反斜杠或匹配的引号进行转义。 |
| **EXAMPLE** | echo "what is your name?" | |
| Local variables | 局部变量在当前 shell 的作用域内。当脚本结束时，它们不再可用；即，它们超出作用域。局部变量会被设置并赋予值。 |
| **EXAMPLE** | variable_name=value name="John Doe" x=5 | |
| Global variables | 全局变量称为环境变量。它们为当前运行的 shell 以及从该 shell 启动的任何进程设置。它们在脚本结束时超出作用域。 |
| **EXAMPLE** | VARIABLE_NAME=value export VARIABLE_NAME PATH=/bin:/usr/bin:. export PATH | |
| Extracting values from variables | 要从变量中提取值，使用美元符号。 |
| **EXAMPLE** | echo $variable_name echo $name echo $PATH | |

## Table 2.2 Bourne Shell Syntax and Constructs (continued)

| Reading user input | read 命令从用户处读取一行输入并将其分配给右侧的变量。read 命令可以接受多个变量名。每个变量将被分配一个单词。 |
| **EXAMPLE** | ``` echo "What is your name?" read name read name1 name2 ... ``` |
| Arguments (positional parameters) | 参数可以从命令行传递给脚本。位置参数用于在脚本内部接收其值。 |
| **EXAMPLE** | 在命令行：$ scriptname arg1 arg2 arg3 ... 在脚本中：``` echo $1 $2 $3 Positional parameters echo $@ All the positional parameters echo $# The number of positional parameters ``` |
| Arrays (positional parameters) | Bourne shell 确实支持数组，但可以通过使用位置参数创建单词列表。单词列表跟在内置的 set 命令之后，并按位置访问。最多允许九个位置。内置的 shift 命令将列表左侧的第一个单词移出。各个单词通过从 1 开始的位置值访问。 |
| **EXAMPLE** | ``` set word1 word2 word3 echo $1 $2 $3 Displays word1, word2, and word3 set apples peaches plums shift echo $1 Displays first element of the list echo $2 Displays second element of the list echo $@ Displays all elements of the list ``` |
| Command substitution | 要将 UNIX/Linux 命令的输出分配给变量，或在字符串中使用命令的输出，使用反引号。 |
| **EXAMPLE** | ``` variable_name=`command` echo $variable_name now=`date` echo $now echo "Today is `date`" ``` |

