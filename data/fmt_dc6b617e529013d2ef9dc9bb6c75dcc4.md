
```
if [ $X -gt $Y ]; then echo greater; X=0; fi
```

```
if [ $X -gt $Y ]
then
echo greater
X=0
fi
```

（后续内容翻译同上文，保持格式一致）

### 7.5 Case 语句

`case` 语句是另一种 n 路选择语句，在许多方面与 `if-then-else` 语句相似。指令将一个值与一系列枚举列表进行比较。一旦找到匹配项，就会执行相应的操作（`s`）。`case` 语句（在 `C`/`C++`/`Java` 中被称为 `switch`）在其他语言中比在 `Bash` 中更具局限性。

一个序数值是指具有特定的前驱和后继值的值，发现于整数和字符。例如，`5` 的前驱是 `4`，后继是 `6`，而 `'c'` 的前驱是 `'b'` 后继是 `'d'`。另一方面，像 `2.13513` 或字符串 `"Hello"` 这样的值并没有特定的前驱或后继。

要使用 `case` 语句实现之前的评分脚本，在大多数语言中，你必须列举出 `90` 到 `100` 之间、`80` 到 `89` 之间等所有值。但 `Bash` 版本为我们提供了了便利，我们可以使用通配符来缩小枚举列表的大小。

`Bash` 形式的 `case` 指令：

```bash
case expression in
  list1 action(s);
  list2 action(s);
  .*
  listn action(s);
esac
```

注意其语法。首先，每个 `case` 分支都以两个连续的分号结束。其次，枚举列表以右括号符号结束。最后，整个语句以 `esac` 语句结束。

该表达式可以是变量的值（例如 `$X`）、算术运算的结果（例如 `$($* 5))`），也可以是 Linux 命令的结果。枚举列表可以是一个或多个列表，并可以组合通配符。例如，`*` 本身会匹配所有内容，并可以作为默认子句代替最后的枚举列表。任何动作都可以包含多条指令，在这种情况下，指令之间用分号隔开。

使用 `case` 语句修改我们之前的计算器程序得到如下脚本：

```bash
#!/bin/bash
if [ $# -ne 3 ];
  then echo Illegal input, did not receive 3 parameters
  else case $2 in
    +) echo $((1+$3));
    -) echo $((1-$3));
    m) echo $((1*3));
    /) echo $((1/$3));
    %%) echo $((1%$3));
    *) echo Illegal arithmetic operator;
esac
```

我们看到最后一个枚举列表是 `(*)`，它是默认子句，因此如果其他任何列表都不匹配 `$2` 的值，就会执行此动作。因此，`*` 不是用于表示乘法，而是表示“其他所有内容”。

除了 `*` 通配符外，你还可以使用 `[...]` 和 `[!]` 在列表中指定模式，其中 `[...]` 分别匹配包含括号内任意字符的字符，而 `[!]` 匹配不包含括号内任意一个字符的字符。例如，`[Pp][Cc]` 会匹配 `PC`、`Pc`、`pc`、`pC`，而 `[A-Z[!A-Z]]` 会匹配两个字符，其中第一个是大写字母，第二个是大写字母以外的任何字符。我们还可以使用 `|` 来分隔完整的字符串，例如 `spring|summer|fall|winter`。

让我们考虑另一个例子。我们询问用户他们喜欢的颜色，并根据响应输出消息。

```bash
echo What is your favorite color?
read color
case $color in
red) echo Like red wine ;;
blue) echo Do you know there are no blue foods? ;;
green) echo The color of life ;;
purple) echo Mine too; ;;
*) echo That’s nice, my favorite color is purple ;;
esac
```

我们打算展示在 shell 脚本中控制系统服务的案例，如下所示的情况。在这里，我们有一个脚本将执行用户提交的操作来启动或停止脚本。

```bash
if [ $# -eq 0 ]; then echo Error, no command supplied
else
  case $1 in
    start())/sbin/someservice -s ;;
    stop())/sbin/someservice -k ;;
    restart())/sbin/someservice -s ;;
    status())/sbin/someservice -d ;;
    *) echo Usage:/etc/init.d/[start | stop | restart] ;;
  esac
fi
```

首先，我们假设用户执行了命令 `/etc/init.d/someservice`，其中 `someservice` 是服务名称。其次，我们假设服务程序本身存储在 `/sbin` 中，我们接收到的选项 `-s` 表示启动，`-d` 显示其状态。我们还假设用户输入了命令，在这种情况下应该是 `start`、`stop`、`restart` 或 `status` 之一。如果没有命令，脚本将响应“未提供命令”的错误消息；对于除了 `start`、`stop`、`restart` 或 `status` 以外的任何命令，脚本将响应默认用法说明，如何使用此脚本。

注意 `restart` 对应的动作有两个指令：调用 `/sbin/someservice -k` 然后调用 `/sbin/someservice -s`。这些可以放在同一行，在这种情况下，它们需要用分号隔开。枚举项是我们的默认情况，向用户输出如何使用该指令说明。我们将在第 11 章详细探讨其中一个服务脚本时研究这种风格的代码。

以下示例演示了通配符的进一步用法。在第一个情况下，我们正在测试用户可能的 `Yes`/`No` 回答。在第二种情况下，我们正在将文件名与可能的扩展名列表进行比较，以确定如何处理文件（在这种情况下，我们尝试编译程序）。

```bash
echo -n Do you agree to the licensing terms of the program?
read answer
case $answer in
  [yY] | [yE][sS]) ./program ;;
  [nN] | [nO]) echo I cannot run the program ;;
  *) echo Invalid ;;
esac

if [ $# ]; then echo Error, no directory provided
else
  for file in $1; do
    case $file in
      *.c) gcc $file ;;
      *.java) javac $file ;;
      *.sh) .$file ;;
      *) echo $file is of an unknown type ;;
      *) echo $file has no extension to match ;;
    esac
  done
fi
```

最后，你可以通过使用 `&` 代替 `;;` 来改变 `case` 语句的行为。使用 `;;` 终止动作，而使用 `&` 则在执行动作后继续执行 `case` 语句。如果发现匹配，则终止 `case` 语句。

- * [a-z]* ;

- * [A-Z]* ;

- * [0-9]*

- *

### 7.5.6 选择语句之外的条件

还有另一种可以探索的选择语句形式，即使用短路逻辑的 `if-then` 语句简写，通过使用 `&&` 或 `||` 实现。对于 `&&`，如果条件的前部分为假，则不需要计算后半部分；同样对于 `||`，如果条件的前部分为真，则不需要计算后半部分。例如，考虑

```
A>B B>C
```

如果 `A` 不大于 `B`，则不需要比较 `B` 和 `C`，因为整个表达式为假。相反，在

```
D>E || F>G
```

如果 `D` 大于 `E`，则不需要比较 `F` 和 `G`，因为整个表达式为真。在 Linux 中，我们将这种概念应用于配对可执行语句。

- `some condition ] && some action`

- `some condition ] || some action`

在第一情况下，如果条件为假，则不执行动作。在第二种情况下，如果条件为真，则不执行动作。我们如何将此用于呢？

最常见的情况是将测试文件是否可访问的条件与访问文件的指令结合起来。例如，我们预期找到 `myscript.sh` 脚本，它应该是一个普通文件。如果找到了文件并想执行它。我们可以使用如下形式的 `if-then` 语句：

```bash
-f myscript.sh ]; then ./myscript.sh; fi
```

或者使用短路方法：
