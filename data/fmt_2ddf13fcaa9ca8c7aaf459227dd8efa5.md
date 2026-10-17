
(The Script)

```
#!/bin/bash
# Scriptname: wholenm
# Purpose: The expr command tests that the user enters an integer

1 echo "Enter an integer."
read number
2 if expr "$number" + 0 >/dev/null
then
3 :
4 else
    echo "You did not enter an integer value."
    exit 1
5 fi
```

#### 解释

1. 用户被要求输入一个整数。`number` 被赋给变量 `number`。
2. `expr` 命令计算表达式。如果可以执行加法，则该数字为整数且 `expr` 返回成功的退出状态。所有输出都被重定向到位桶 `/dev/null`。
3. 如果 `expr` 成功，它返回 0 的退出状态，而 `:` 命令什么也不做。
4. 如果 `expr` 命令失败，它返回非零退出状态，`echo` 命令显示消息，程序退出。
5. `fi` 结束 `if` 块。

## 14.5.8 `case` 命令

`case` 命令是一个多路分支命令，可用作 `if`/`elif` 命令的替代。`case` 变量的值与 `value1`、`value2` 等进行匹配，直到找到匹配项。当某个值与 `case` 变量匹配时，值之后的命令将被执行，直到遇到双分号 `;;`。随后执行从单词 `esac` 开始之后的部分（`case` 反写）。

如果 `case` 变量不匹配，程序将执行 `*)` 之后的命令，即默认值，直到 `;;` 或 `esac`。`*)` 值的功能与 `if`/`else` 条件中的 `else` 语句相同。`case` 值允许使用 shell 通配符和竖线 `|`（管道符号）来对两个值进行 OR 操作。

### 格式

```
case variable in
value1)
  command(s)
  ;;
value2)
  command(s)
  ;;
*)
command(s)
;;
esac
```

### 示例 14.30

(The Script)

```
#!/bin/bash
# Scriptname: xcolors

+   1 echo -n "Choose a foreground color for your xterm window: "
+   read color

2 case "$color" in

3 [Bb]1???

4 xterm -fg blue -fn terminal &

5 ;;

6 [Gg]ree*

7 xterm -fg darkgreen -fn terminal &

8 red | orange)    # The vertical bar means "or"

   xterm -fg "$color" -fn terminal &

   ;;

*) xterm -fn terminal

;;

9 esac

10 echo "Out of case command"
```

#### 解释

1. 用户被要求输入。输入被赋给变量 `color`。
2. `case` 命令计算表达式 `$color`。
3. 如果颜色以 B 或 b 开头，其后是字母 l 和任意两个字符，例如 blah、blue、blip 等，`case` 表达式将匹配第一个值（通配符是 shell 元字符）。该值以单个右括号 `)` 终止。`xterm` 命令将前景色设置为蓝色。
4. 如果第 3 行的值与 `case` 表达式匹配，则执行该语句。
5. 在此命令块的最后一个命令之后需要双分号 `;;`。当到达分号时，控制分支到第 10 行。如果分号单独占一行，脚本更易于调试。
6. 如果 `case` 表达式匹配 G 或 g，其后是字母 ree 并以零个或多个任意其他字符结尾，则执行 `xterm` 命令。双分号 `;;` 终止语句块，控制分支到第 10 行。
7. 竖线 `|` 用作 OR 条件运算符。如果 `case` 表达式匹配 red 或 orange，则执行 `xterm` 命令。
8. 这是默认值。如果上述任何值都不匹配 `case` 表达式，则执行 `*)` 之后的命令。
9. `esac` 语句终止 `case` 命令。
10. 在匹配其中一个 `case` 值后，执行继续到此处。

### 使用 here 文档和 `case` 命令创建菜单

here 文档和 `case` 命令经常一起使用。here 文档用于创建将显示到屏幕上的选项菜单。用户将被要求选择其中一个菜单项，而 `case` 命令将针对一组选择进行测试以执行适当的命令。

#### 示例 14.31

（来自 .bash_profile 文件）

```
echo "Select a terminal type: "

1 cat << ENDIT

1) unix

2) xterm

3) sun

2 ENDIT

3 read choice

4 case "$choice" in

5 1) TERM=unix

export TERM

;;

2) TERM=xterm

export TERM

;;

6 3) TERM=sun

export TERM

;;

7 esac

8 echo "TERM is $TERM."
```

（命令行和输出）

```
5 .bash_profile

Select a terminal type:

1) unix

2) xterm

3) sun

2      <-- User input

TERM is xterm.
```

##### 解释

1. 如果将这段脚本放入 `.bash_profile` 中，登录时你将有机会选择合适的终端类型。这里文档用于显示选项菜单。
2. 用户定义的 `ENDIT` 终止符标记这里文档的结束。
3. `read` 命令将用户输入存储在变量 `TERM` 中。
4. `case` 命令评估变量 `TERM` 并将该值与右括号前的其中一个值进行比较：1、2 或 3。
5. 第一个被测试的值是 1。如果匹配，终端将被设置为 unix。`TERM` 变量被导出，以便子 shell 可以继承它。
6. 不需要默认值。`TERM` 变量通常在登录时在 `/etc/profile` 中分配。如果选择为 3，则终端将被设置为 sun。
7. `esac` 终止 `case` 命令。
8. `case` 命令完成后，此行被执行。

## 14.6 循环命令

循环命令用于执行命令或一组命令固定次数或直到满足特定条件。`bash` shell 有三种类型的循环：`for`、`while` 和 `until`。

### 14.6.1 `for` 命令

`for` 循环命令用于对一组项目执行命令有限次数。例如，你可能会使用此循环对一组文件或用户名执行相同的命令。`for` 命令后面跟着用户定义的变量、关键字 `in` 和一个词列表。循环第一次执行时，词列表中的第一个词被分配给变量，然后从列表中移出。一旦词被分配给变量，就会进入循环体，并在 `do` 和 `done` 关键字之间的命令被执行。循环下一次执行时，第二个词被分配给变量，以此类推。循环体从 `do` 关键字开始，到 `done` 关键字结束。当列表中的所有词都被移出后，循环结束，程序控制继续在 `done` 关键字之后。

#### 格式

```
for variable in word_list

 do

   command(s)

 done
```

#### 示例 14.32

```
（脚本）

#!/bin/bash
# Scriptname: forloop

1  for pal in Tom Dick Harry Joe
2  do
3      echo "Hi $pal"
4  done
5  echo "Out of loop"

（输出）

Hi Tom
Hi Dick
Hi Harry
Hi Joe
Out of loop
```

##### 解释

1. 此 `for` 循环将遍历名字列表 Tom、Dick、Harry 和 Joe，将每个名字从左移出并将其值分配给用户定义的变量 `pal`，使用后即分配。一旦所有词都被移出且词列表为空，循环结束，执行从 `done` 关键字之后开始。循环第一次执行时，变量 `pal` 将被分配单词 Tom。第二次循环时，`pal` 将被分配 Dick，下一次 `pal` 将被分配 Harry，最后一次 `pal` 将被分配 Joe。
2. 在词列表之后需要 `do` 关键字。如果它与同一行使用，列表必须以分号终止。例如：`for pal in Tom Dick Harry Joe; do`
3. 这是循环体。Tom 被分配给变量 `pal` 后，循环体中的命令（即 `do` 和 `done` 关键字之间的所有命令）将被执行。
4. `done` 关键字结束循环。一旦列表中最后一个词（Joe）被分配并移出，循环退出，执行从第 2 行开始。
5. 循环退出时控制在此恢复。

#### 示例 14.33

（命令行）

```
1 $ cat mylist

tom

patty

ann

jake
```

（脚本）

```
#!/bin/bash

# Scriptname: mailer
```
