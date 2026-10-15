

## 示例 2.6（续）

```
13    if (( ${#foods[*]} == $n ))
        then
            set -A foods cheese crackers shrimp drinks "hot dogs"
                         sandwiches
        fi
    fi
15 done
print "Bye..."
```

## 解释

1 这行代码让内核知道你正在运行一个 Korn shell 脚本。

2 这是一个注释。它会被 shell 忽略，但对于任何试图理解脚本正在做什么的人来说都很重要。

3 变量 guestfile 被设置为名为 guests 的文件的完整路径名。

4 这行代码的意思是：如果文件 guests 不存在，则向屏幕打印 "guests non-existent" 并退出脚本。

5 一个环境变量被赋予一个值并导出（使其可供子 shell 使用）。

6 UNIX/Linux 命令的输出，即一天中的小时，被赋给名为 Time 的变量。变量被赋予值以对应地点和时间。

7 要带的食物列表被赋给一个名为 foods 的数组，使用 set -A 命令。列表中的每个项目都可以通过从 0 开始的索引访问。

8 typeset -i 命令用于创建整数值。

9 对于宾客名单上的每个人，将会创建一个邮件消息，邀请该人参加在指定地点和时间举行的聚会，并分配一份食物清单中的食物。

10 条件测试用户 root。如果用户是 root，控制将返回到循环顶部并将宾客名单中的下一个用户赋给变量 person。

11 邮件消息被发送。消息正文包含在一个 here 文档中。

12 变量 n 增加 1。

13 如果数组中的元素数等于变量的值，则表示已到达数组末尾。

14 这标志着循环语句的结束。

## 2.6 Bash Shell 构造

Korn 和 Bash shell 非常相似，但存在一些差异。Bash 构造列在表 2.4 中。

|  | Bash Shell Syntax and Constructs |
|---|---|
| **shbang 行** | “shbang” 行是脚本的第一行，让内核知道将解释脚本中各行的 shell 是什么。shbang 行由 #! 组成，后跟 shell 的完整路径名，并且可以跟随选项来控制 shell 的行为。**示例：** `#!/bin/bash` |
| **注释** | 注释是以 # 符号为前缀的描述性材料。它们一直有效到行尾，并且可以在行的任何位置开始。**示例：** `# This is a comment` |
| **通配符** | 有一些字符会被 shell 以特殊方式求值。它们被称为 shell 元字符或“通配符”。这些字符既不是数字也不是字母。例如，*, ?, 和 [] 用于文件名扩展。 <, >, >>, 和 | 符号用于标准 I/O 重定向和管道。为了防止这些字符被 shell 解释，它们必须被引用。**示例：** `rm *; ls ??; cat file[1-3];` `echo "How are you?"` |
| **显示输出** | 要将输出打印到屏幕，使用 echo 命令。通配符必须用反斜杠或匹配的引号转义。**示例：** `echo "How are you?"` |
| **局部变量** | 局部变量的作用域为当前 shell。当脚本结束时，它们不再可用；即，它们超出作用域。局部变量也可以使用内置的 declare 函数定义。局部变量被设置并赋予值。**示例：** `variable_name=value` `declare variable_name=value` `name="John Doe"` `x=5` |

## 表 2.4 Bash Shell Syntax and Constructs（续）

| 全局变量 | 全局变量称为环境变量，并使用 export 内置命令创建。它们为当前运行的 shell 以及从该 shell 启动的任何进程设置。脚本结束时它们超出作用域。

使用 -x 选项的内置 declare 函数也设置环境变量并将其标记为导出。

**示例**
```
export VARIABLE_NAME=value
declare -x VARIABLE_NAME=value
export PATH=/bin:/usr/bin:.
``` |
| 从变量中提取值 | 要从变量中提取值，使用美元符号。

**示例**
```
echo $variable_name
echo $name
echo $PATH
``` |
| 读取用户输入 | 将提示用户输入。read 命令用于接受一行输入。read 的多个参数会导致一行被拆分为单词，每个单词将被赋给指定的变量。

**示例**
```
echo "what is your name?"
read name
read name1 name2 ...
``` |
| 参数 | 参数可以从命令行传递给脚本。位置参数用于在脚本内部接收它们的值。

**示例**

在命令行：
$ scriptname arg1 arg2 arg3 ...

在脚本中：
```
echo $1 $2 $3        Positional parameters
echo $@             All the positional paramters
echo $#             The number of positional parameters
``` |
| 数组 | Bourne shell 利用位置参数创建单词列表。除了位置参数之外，Bash shell 还支持数组语法，其中元素通过从 0 开始的子脚本访问。Bash shell 数组使用 declare -a 命令创建 |

