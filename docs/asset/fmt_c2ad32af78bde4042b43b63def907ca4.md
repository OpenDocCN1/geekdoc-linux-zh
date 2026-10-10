
列表 22.13 脚本中另一个值得注意的点是使用的算术表达式。在外部循环中，发现使用 `let` 将 `outer` 赋值为一。内部循环使用了 `expr`，它是一个表达式评估器。

# 第 22 章 Bourne-Shell (bash) 439

## for 循环

bash 中的 `for/in/do/done` 允许允许遍历变量范围。这与 C 等高级语言中经典的 for 循环不同，但 bash 的视角非常有用，并提供了 C 中没有的功能。列表 22.14 提供了一个非常简单的 for 循环。

列表 22.14 简单的 for 循环示例（位于 CD-ROM 的）`/source/ch22/forloop.sh`

```
1: #!/bin/bash

2:

3: echo Counting from 1 to 5

4:

5: for val in 1 2 3 4

6: do

7: echo -n $val

8: done

9: echo

10: exit
```

该脚本的结果是：

```
# test.sh

Counting from 1 to 5

1 2 3 4 5
```

当然，你可以像列表 22.15 所示简单地模拟 C 的 for 循环机制。

列表 22.15 类 C for 循环示例（位于 CD-ROM 的）`/source/ch22/forloop2.sh`

```
1: #!/bin/bash

2:

3: for ((var=1; var <= 5; var++))

4: do

5: echo -n $var

6: done

7: echo

8: exit
```

# 440 GNU/Linux 应用程序

列表 22.15 中的代码与列表 22.14 所示的原始 for-in 循环相同。你也可以在循环范围内使用字符串，如列表 22.16 所示。该脚本遍历提供的字符串范围。

列表 22.16 说明范围的另一个 for 循环（位于 CD-ROM 的 `./source/ch22/forloop3.sh`）

```
1: #!/bin/bash

2:

3: echo The first planets

4: for planet in venus mars; do

5: echo -n $planet

6: done

7: echo

8: exit
```

bash 优于传统高级语言的地方在于可以使用命令的结果替换范围的能力。看一个使用通配符 `*` 的更复杂的 for-in 循环（列表 22.17）。

列表 22.17 使用通配符列出系统子目录（位于 CD-ROM 的 `./source/ch22/forloop4.sh`）

```
1: #!/bin/bash

2:

3: # Save the current directory

4: curwd=$PWD

5:

6: # Change the directory to /home

7: cd /home

8:

9: echo -n Users on the system are:

10:

11: # Loop through each file (via the wildcard)

12: for user in *; do

13: echo -n $user

14: done

15: echo

16:
```

# 第 22 章 Bourne-Shell (bash) 441

```
17: # Return to the previous directory

18: cd $curwd

19:

20: exit
```

## 输入与输出

你已经看到了一些使用 `echo` 命令输出的示例。该命令只需将提供的字符串显示。你还看到了使用 `-n` 选项抑制换行符。`echo` 命令还提供了通过二进制接口输出数据。例如，为了输出水平制表，可以使用 `\t` 选项，如下：

```
echo -e \t\t\ttented text.
```

其他选项如表 22.5 所示。为了解释这些字符串，必须在字符串之前指定 `-e` 选项。

# 表 22.5 输出字符串中的特殊序列

| 序列 | 解释 |
| :--- | :--- |
| \b | 退格 |
| \f | 换页 |
| \n | 换行 |
| \r | 回车 |
| \t | 水平制表符 |
| \v | 垂直制表符 |
| \ | 反斜杠 |
| \NNN | 进制值的 ASCII 代码 |

你可以使用 `read` 命令从用户接受输入。`read` 命令提供了许多选项，这里研究了其中几个。首先，看看通过交互式 bash shell 使用 `read` 命令的基本形式：

```
# read var

test string

# echo $var

test string

# read -s var
```

# 442 GNU/Linux 应用程序

```
# echo $var

silent input
```

在第一种形式中，你从用户处读取字符串并将其存储在变量 `var` 中。在 `read` 的第二种形式中，你指定了 `-s` 标志。`-s` 标志表示静默输入，这意味着响应 `read` 的输入的字符不会回显到屏幕上。在这种情况下，你输入了 `silent input`，在变量回显后你会看到这个。

`read` 命令的其他可用选项如表 22.6 所示。

# 表 22.6 read 命令的其他选项

| 选项 | 描述 |
| :--- | :--- |
| -a | 输入被赋值给数组，从索引 0 开始 |
| -d | 用于终止输入的字符（而不是换行符） |
| -n | 读取的最大字符数 |
| -p | 用于提示输入的显示的提示字符串 |
| -s | 静默模式（不回显输入的的字符） |
| -t | read 的超时时间（秒） |
| -u | 用于读取的文件描述符而不是终端 |

## 函数

Bash 允许通过创建函数将脚本拆分为更易管理的部分。函数可以非常简单，例如：

```
function <name> () {

  命令序列

}
```

与 C 语言一样，函数在调用之前必须声明。现在来看一个简单的函数示例，该函数对从调用者处传递的两个数字求和（见列表 22.18）。

## 第 22 章 Bourne-Again Shell (bash) 443

列表 22.18 创建一个利用参数的函数（位于 CD-ROM 的 `/source/ch22/func.sh` 中）

```
1: #!/bin/bash

2:

3: function sum ()

4: {

5:

6:   echo $(( $1 + $2 ))

7:

8:   }

9:

10:  sum 5 10
```

在这个示例中，你声明了一个新函数 `sum`（第 3–8 行），它会输出传递它的两个参数之和。请记住 `$1` 代表第一个参数，`$2` 代表第二个参数。那么 `$0` 代表什么呢？就像在 C 语言中一样，从主程序的角度来看，第一个参数是被调用的程序本身的名称。在这种情况下，这个名称就是脚本文件本身。如果调用者没有提供所有必要的参数（只传递了一个参数而不是两个）会发生什么呢？这时是进行一些错误检查的好时机，你可以像列表 22.19 所示更新脚本。

列表 22.19 为我们之前的函数添加错误检查（位于 CD-ROM 的 `/source/ch22/func2.sh` 中）

```
1: #!/bin/bash

2:

3: function sum ()

4: {

5:

6:   if [ $# -ne 2 ]; then

7:     echo usage is sum <param1> <param2>

8:     exit

9:   fi

10:

11:  echo $(( $1 + $2 ))

12:

13:  }

14:

15:  sum 5 10
```
