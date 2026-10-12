
只要 `<test-com>` 返回真状态，结构就会执行命令。如果状态为假，则通过 `done` 命令退出并将控制权传递给脚本中的下一条命令。图 18.4 展示了 while 流程图。

![](img/256e02a6afce528d264a8d911fa0ff20_727_0.png)

## `until` 结构

`until` 结构与 `while` 结构类似，因为 `until` 继续循环直到 `<test-com>` 返回真条件。`while` 结构在 `<test-com>` 继续返回真条件时循环。如果结果为假，则控制权传递给 `do` 命令。图 18.5 展示了 until 流程图，以下示例演示了 `until` 结构的语法：

```
until <test-com>
do
	commands
done
```

![](img/256e02a6afce528d264a8d911fa0ff20_727_1.png)

以下脚本使用了 `until` 结构：

```
$ cat toolcrib
```

```
toolname=pliers
tool=' '
echo 'Guess the missing tool:'
echo
until [ "$tool" = "$toolname" ]
do
    echo 'which tool: \\c'
    read tool
    echo "Looking for: $tool"
done
echo "That's it! The $tool is the missing tool!"
$ ./toolcrib
Guess the missing tool:
which tool: wrench
Looking for: wrench
which tool: hammer
Looking for: hammer
which tool: pliers
Looking for: pliers
That's it! The pliers is the missing tool!
```

`for..while` 或 `until` 结构可以通过 `break` 或 `continue` 语句中断。`break` 语句通过将控制权转移到 `done` 语句之后的语句来终止循环执行。`continue` 命令通过将控制权转移到 `done` 语句来继续循环执行。

以下脚本说明了如何使用 `break` 和 `continue`：

```
$ cat filedrawers
```

```
for file in 1 2 3 4 5 6 7 8
do
    if [ $file -lt 4 ] ; then
        echo 'continue'
        continue
    fi
    #
        echo $file
    #
    if [ $file -ge 6 ] ; then
        echo 'break'
        break
    fi
done
$ filedrawers
```

## 案例结构

`case` 结构用于查找用户提示后输入的字符串（字符串搜索）。这是一个高级命令，它会在执行其他命令之前做出多个决策。该结构常用于创建菜单，因为它依赖于用户输入。以下示例展示了 `case` 的工作方式：

```bash
$ cat testpattern
echo 'Enter YES, NO or MAYBE: \c'
read answer
case "$answer" in
        'YES')
                echo 'You answered YES'
                ;;
        'NO')
                echo 'You answered NO'
                ;;
        'MAYBE')
                echo 'You answered MAYBE'
                ;;
        *)
                echo 'You did not answer YES, NO or MAYBE'
                ;;
esac
$ testpattern
Enter YES, NO, or MAYBE:  NO
You entered NO
$ testpattern
Enter YES, NO, or MAYBE:  no
You did not enter YES, NO, or MAYBE
```

图 18.6 中的流程图说明了 `case` 命令的使用。

### 图 18.6

*图 18.6：case 命令流程图*

![](img/256e02a6afce528d264a8d911fa0ff20_729_0.png)

![](img/256e02a6afce528d264a8d911fa0ff20_730_0.png)

`*` 在字符串模式中表示通配符。它可以表示任意字符串，并在没有匹配项时作为兜底选项。如果没有找到匹配测试模式的字符串，则控制权将传递给 `esac` 语句之后的命令，而 `case` 结构不执行任何操作。

若要脚本接受大写或小写的响应，你需要列出参数，例如 `a|A, b|B`，等等。

字符串搜索模式包括以下内容：

- `*` 匹配任意字符串，默认情况。
- `?` 匹配单个字符。
- `|` 分隔可选选择。
- `[ ]` 依次尝试括号内的字符，以寻找匹配项。

`case` 结构用于创建菜单。以下是一个简单菜单的示例：

```bash
$ cat <magic-menu>
#!/bin/sh
# menu commands
echo '\n MAGIC MENU \n'
echo ' a. Current date and time'
echo ' b. Department number'
echo ' c. Department name'
echo ' d. Department Budget'
echo 'Enter a, b, c, or d: \c'
read answer
echo
case $answer in
a) date ;;
b) dnum ;;
c) dname ;;
d) dbud ;;
*) echo 'Nothing selected: $answer' ;;
esac
$ magic-menu

MAGIC MENU

a. Current date and time
b. Department number
c. Department name
d. Department budget
Enter a, b, b, c, or d: a
Fri Feb 05 12:17:07 EST 2001
```

第一个 `echo` 语句中的 `\n` 字符串被解释为换行符。这是可供你使用的格式字符之一。为了使菜单更易读，包含格式字符会有所帮助。在创建菜单时可能还有其他有用的字符：`\b`（退格）、`\c`（抑制尾部换行）、`\f`（换页）、`\n`（换行）、`\r`（回车）、`\t`（水平制表符）和 `\v`（垂直制表符）。

`case` 控制结构会根据命令行中参数的数量分支到不同的操作。以下示例展示了 `case` 如何处理带有多个参数的 `vi` 编辑器文件：
