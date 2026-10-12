
```
Shell - Konsole
Session Edit View Bookmarks Help
user> read INT
5
user> read PI
3.1415926
user> read CHAR
M
user> read STR
Linux in easy steps
user> echo "Stored integer is" $INT
Stored integer is 5
user> echo "Pi is worth around" $PI
Pi is worth around 3.1415926
user> echo "Programming with" $CHAR
Programming with M
user> echo -e "\n\t$STR"
```

这种输入、存入变量、稍后输出存储值的能力创建了一种非常基础的 `shell` 交互，以简单的方式重复输入值。更有用的 `shell` 交互可以通过评估输入值并根据评估结果提供输出。

## 评估表达式

`expr` 命令允许你在 `shell` 提示符处执行简单的数学计算。它识别常用的算术运算符，但那些在 `shell` 中有其他含义的运算符需要用反斜杠转义。

算术运算符有：

- `+` 加法
- `-` 减法
- `/` 除法
- `%%` 取模

![](img/0494b98ec9ddc4515587e9808d73902e_213_0.png)

每个参数必须由空格分隔，较长的表达式可以使用括号建立运算符优先级——但每个括号字符都必须转义。

`expr` 命令还可以执行布尔评估并返回真 (`1`) 或假 (`0`)。在下面的示例中，`7` 不等于 (`!=`) `3` 是真的 (`1`)：

你可以使用 `xcalc` 命令从 `shell` 窗口快速启动图形计算器。

![](img/0494b98ec9ddc4515587e9808d73902e_213_1.png)

```
user expr 7 + 3
10
user expr 7 \* 3
21
user expr 7 \(3 + 1 \)
28
user expr 7 != 3
1
user expr length "Linux in easy steps"
19
user expr substr "Linux in easy steps" 7 13
in easy steps
user expr index "Linux in easy steps" "x"
5
user>
```

简单的字符串函数如 `length` 可以配合 `expr` 命令发现字符串的长度。`substr` 函数从给定位置开始提取指定长度的子字符串，`index` 函数给出指定字符在字符串中首次出现的位置。

表达式评估的结果可以使用 `if-then` 语句导致特定的输出。这包含两个部分：说明要评估的表达式，以及仅当结果为真时输出的文本。`if` 关键字开始语句，后面跟着一对括号内的测试表达式。整个语句的每个部分必须与后面空格分隔，以便 `shell` 评估表达式。`then` 关键字开始语句的第二部分，包含如果测试为真要执行的命令。以 `fi` 关键字结束，标记语句的结束。

![](img/0494b98ec9ddc4515587e9808d73902e_214_0.png)

在 `if` 关键字后留一个空格以避免错误。在 `[]` 括号后留一个空格以避免错误。在 `[]` 括号前留一个空格以避免错误。

![](img/0494b98ec9ddc4515587e9808d73902e_214_1.png)

字符串比较运算符有 `==` 等和 `!=` 不。数值比较运算符有 `eq` 等、`ne` 不等、`gt` 大于、`lt` 小于、`ge` 大于或等于、`le` 小于或等于。

输入语句的第一部分然后按回车键，提示输入语句的剩余部分。或者，输入整个语句并用分号分隔每个部分。此示例演示了这两种，并使用 `ne` 数值不等于运算符和 `=` 字符串相等运算符来评估表达式：

注意输出在结果为假的两种情况下是如何显示的。

| Session | Edit | View | Bookmarks | Settings | Help |

```
user if [ 7 -ne 3 ]
> then echo "true"
> fi
true
user if [ 7 -ne 3 ]; then echo "true"; fi
true
user if [ 7 -ne 7 ]; then echo "true"; fi
true
user if [ string = string ]
> then echo "correct"
> fi
correct
user if [ string = rope ]
> then echo "correct"
> fi
user>
```

## 分支语句

`if-then` 语句用于指定在表达式求为真时才执行的命令，它可以扩展为指定在表达式求为假时执行的备用命令。备用命令指定在 `else` 关键字之后，该关键字被插入在 `if-then` 语句的 `then` 部分之后：

这些表达式使用了 `gt`（大于）和 `lt`（小于）这些数值比较运算符

```bash
Shell - Konsole
会话 编译 视图 签签 设置
user> if [ 7 -gt 3 ]
> then echo "greater"
> else echo "less"
> fi
greater
user> if [ 7 -lt 3 ]
> then echo "greater"
> else echo "less"
> fi
less
user>
```

这个过程被称为“条件分支”——使语句“分支”并仅执行求为真的“条件”。你可以使用 `elif` 关键字添加后续的评估。这结合了 `else` 和 `if`，允许进行复杂的条件分支：

此示例中 `whoami` 周围的引号符号使结果与该命令的结果进行比较——它们出现在第 148 页用于自定义 `shell` 提示符的代码中。

```bash
Shell - Konsole
会话 编译 视图 签签 设置 帮助
user> if [ `whoami` = "root" ]
> then echo "Hello SuperUser"
elif [ `whoami` = "mike" ]
> then echo "Hello Mike"
> else echo "Hello Guest"
> fi
Hello Mike
user>
```

最后一个示例可以创建为脚本并扩展以识别当前目录。`Bash` `shell` 脚本仅仅是包含系列命令的文本文件，就像最后几个示例在 `shell` 提示符处使用的命令一样。第一行的开头必须是 `#!/bin/bash`，以指定执行脚本的程序的位置——在这种情况下，它是 `/bin` 中的 `bash` 这种壳程序：

![](img/0494b98ec9ddc4515587e9808d73902e_216_0.png)

`bash` 脚本的第一行在 `#!` bang 字符之后被称为 `#sh-bang` 行。

```bash
#!/bin/bash
if [ whoami = "root" ]
then echo "Hello SuperUser at $(pwd)"
elif [ whoami = "mike" ]
then echo "Hello Mike at $(pwd)"
else echo "Hello Guest at $(pwd)"

:w hello
```

将脚本保存在当前目录后，只需通过 `chmod 711` 使其变为可执行——这样所有者可以读取、写入和执行，但所有其他人只能执行。输入 `/` 命令和文件名来运行脚本：

![](img/0494b98ec9ddc4515587e9808d73902e_216_1.png)

记住登录 `root` 账户将你处于 `root` 目录——超级用户必须指定脚本的完整路径才能执行。

```bash
user chmod 711 hello
user> ls -lo hello
-rw-r--x 1 mike 171 2005-10-14 19:25 hello
user> ./hello
Hello Mike at /home/mike
user> su -l
Password: *****
root> /home/mike/hello
Hello SuperUser at /root
root> 
```

`case-in` 语句提供了另一种执行条件分支的方法，作为 `if-then-else` 语句的替代。它将单个值匹配到一个分支并执行其命令/多个命令。提供的值指定在 `case` 关键字之后，然后 `in` 关键字开始一个分支列表。每个分支指定一个可能的匹配值，后跟一个 `\)` 括号、要执行的代码和一个分号终止符。最后，`esac` 关键字标记整个 `case` 语句的结束。

`case` 语句通常用于评估存储在变量中的值（通常来自用户输入）并提供许多分支。在下面的脚本中正是这种方式使用的：

![](img/0494b98ec9ddc4515587e9808d73902e_217_0.png)
