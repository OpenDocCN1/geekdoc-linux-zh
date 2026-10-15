
### EXPLANATION

+   1 将传递给此程序的第一个命令行参数 `$1` 分配给变量 `file`。
+   2 测试命令跟在 `if` 之后。如果 `$file`（变量替换后）是一个不存在的文件（注意 NOT 运算符 `!`），则执行 `then` 关键字下的命令。退出值为 1 表示程序以某种方式失败。（在本例中，测试失败。）
+   3 如果文件是目录，则打印它是目录。
+   4 如果文件不是目录，`else if` 文件是普通文件，则...

# 解释（续）

+   5 如果文件可读、可写且可执行，则……
+   6 `fi` 终止最内层的 `if` 命令。如果文件没有读、写和执行权限，程序将以 2 作为参数退出。
+   7 如果第 2 行和第 3 行失败，则执行 `else` 命令。程序将以 3 的值退出。
+   8 这个 `fi` 与示例中第 3 行的 `if` 对应。
+   9 名称为 `testing` 的文件不存在。
+   10 `$?` 变量保存退出状态，1。

## 12.5.15 空命令

空命令是一个冒号。它是一个内置的、无操作的命令，返回的退出状态为 0。它用作 `if` 命令之后的占位符，当你没有需要说的内容，但需要一个命令，否则程序会因 `then` 语句之后需要内容而产生错误信息。空命令常被用作循环命令的参数，使循环成为无限循环，或用于测试变量表达式修饰符，例如 `{EDITOR:=/bin/vi}`。

# 示例 12.25

```
(The Script)

1 name=Tom

2 if grep "$name" databasefile > /dev/null 2>&1

then

3 :

4 else

    print "$1 not found in databasefile"

    exit 1

fi
```

# 解释

+   1 字符串 `Tom` 被赋给变量 `name`。
+   2 `if` 命令测试 `grep` 命令的退出状态。如果在 `databasefile` 中找到 `Tom`，则执行空命令且不执行任何操作。
+   3 冒号是空命令。它总是以 0 退出状态退出。
+   4 我们真正想要做的是，如果未找到 `Tom`，则打印错误信息并退出。如果 `grep` 命令失败，则 `else` 之后 的命令将被执行。

# 示例 12.26

```
(The Script)

1 : ${EDITOR:=/bin/vi}

2 echo $EDITOR
```

# 解释

+   1. 冒号命令接受一个由 shell 求值的参数。表达式 `${EDITOR:=/bin/vi}` 被用作冒号命令的参数。如果变量 `EDITOR` 已被之前设置，其值不会被更改；如果未设置，则值 `/bin/vi` 将被赋给它。如果没有冒号命令在表达式之前，Korn shell 会响应类似 `ksh: /bin/vi: not found` 的错误。
+   2. 显示 `EDITOR` 变量的值。

## 12.5.16 case 命令

`case` 命令是一个多路分支命令，可用作 `if/elif` 命令的替代。`case` 变量的值与 `value1`、`value2` 等进行匹配，直到找到匹配项。当某个值与 `case` 变量匹配时，值之后的命令将被执行，直到遇到双分号。然后，`esac` 之后的指令将被执行（`esac` 是 `case` 反写）。

如果 `case` 变量未匹配，程序将执行 `*)` 之后的命令，即默认值，直到遇到双分号或 `esac`。`*` 值的作用与 `if/else` 条件中的 `else` 语句相同。`case` 值可以使用 shell 通配符和垂直线（管道符号）来对两个值进行 OR 操作。

# 格式

```
case variable in

value1)

    command(s);;

value2)

    command(s);;

*)

    command(s);;

esac
```

# 示例 12.21

```
(The Script)

#!/bin/ksh

# Scriptname: xtermcolor

# Sets the xterm foreground color (the color of the prompt and

# input typed for interactive windows)

1  read color?"Choose a foreground color for your terminal?"

2  case "$color" in

3  ${b|b|?}

4      xterm -fg blue -fn terminal &

5          ;;
```

# 示例 12.27（续）

```
6  *\(G\green)

    xterm -fg darkgreen -fn terminal &

    ;;

7  red | orange)        # The vertical bar means "OR"

    xterm -fg "$color" -fn terminal &

    ;;

8  *) xterm -fn terminal &   # default

    ;;

9  esac

10 print "Out of case..."
```

# 解释

+   1 用户被要求输入。输入被赋给变量 `color`。
+   2 `case` 命令计算表达式 `$color`。
+   3 如果 `color` 以 `B` 或 `b` 开头，后跟字母 `l` 和任意两个字符，则 `case` 表达式匹配第一个值。值以单个右括号终止。通配符是 shell 元字符。
+   4 如果第 3 行的值与 `case` 表达式匹配，则执行该语句。`xterm` 命令将前景色设置为蓝色。
+   5 在此命令块的最后一个命令之后需要双分号。控制转移到第 10 行，在分号处结束。
+   6 如果 `case` 表达式匹配 `G` 或 `g`，后跟字母 `r-e-e-n`，则 `xterm` 窗口前景色被设置为深绿色。双分号终止语句块，控制转移到第 10 行。
+   7 垂直线用作 OR 条件运算符。如果 `case` 表达式匹配 `red` 或 `orange`，则执行 `xterm` 命令。
+   8 这是默认值。如果上述值都不匹配 `case` 表达式，则执行 `*)` 值之后的命令(s)。终端前景的默认颜色为黑色。
+   9 `esac` 语句（`case` 反写）终止 `case` 命令。
+   10 在匹配其中一个值后，执行继续到此处。

`case` 命令和 here 文档。经常，here 文档被用来创建菜单。在用户从菜单中选择一个选项后，`case` 命令被用来与其中一个选项进行匹配。Korn shell 还提供 `select` 循环来创建菜单。

# 示例 12.28

（`.profile` 文件）

```
print "Select a terminal type."

1 cat << EOF

    1) vt120

    2) wyse50

    3) ansi

    4) sun

2 EOF

3 read TERM

4 case "$TERM" in

1) export TERM=vt120

    ;;

2) export TERM=wyse50

    ;;

3) export TERM=ansi

    ;;

*) export TERM=sun

    ;;

5 esac

print "TERM is $TERM"
```

# 说明

- 1. 此处文档（here document）用于显示一个选项菜单。
- 2. `EOF` 是用户自定义的终止符。此处文档的输入到此为止。
- 3. `read` 命令等待用户输入，并将其赋给 `TERM` 变量。
- 4. `case` 命令对变量 `TERM` 求值，并将其与列表中的某个数字进行匹配。如果找到匹配项，就设置终端类型。
- 5. `case` 命令以 `esac` 结束。

## 12.6 循环命令

循环命令用于按指定次数执行一条或一组命令，或者一直执行到满足某个条件为止。Korn shell 有四种循环类型：`for`、`while`、`until` 和 `select`。

### 12.6.1 for 命令

`for` 循环命令用于对一组参数中的每个成员执行命令。你可以用该循环对文件列表或用户名列表执行相同的命令。`for` 命令后面跟着一个用户自定义变量、关键字 `in` 和一个单词列表。第一次进入循环时，将单词列表中的第一个单词赋给该变量，然后将其移出列表。下一次进入循环时，将第二个单词赋给该变量，依此类推。循环体从 `do` 关键字开始，到 `done` 关键字结束。当列表中的所有单词都被移出后，循环结束，程序控制流从 `done` 关键字之后继续执行。

# 格式

```
for variable in wordlist

do

    command(s)

done
```

# 示例 12.29

（脚本）

```
1  for pal in Tom Dick Harry Joe

2  do

3      print "Hi $pal"

4  done

5  print "Out of loop"
```

（输出）

```
Hi Tom

Hi Dick

Hi Harry
```
