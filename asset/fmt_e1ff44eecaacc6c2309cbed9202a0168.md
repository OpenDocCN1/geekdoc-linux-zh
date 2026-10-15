
#!/bin/csh

# Script: ifNull.scr

# 确保参数 1 为有效文件

if (-e $argv[1]) then

else
  echo $argv[1] does not exist and cannot be found
endif
# Rest of script here
$ ifNull.scr noFile

Output:

noFile does not exist and cannot be found

```
## 嵌套 if 语句

`if-then-else`语句中的每个分支可以是任何命令，包括另一个`if-then-else`语句。当在`if-then-else`语句的真分支或假分支中发现`if-then-else`语句时，它被称为嵌套`if`。这种设计如图 17.12 所示。

![](img/6e4cdc423ec40606ea72b32fdafff220_753_0.png)

图 17.12 嵌套 if-then-else

让我们用此来解决一个相当常见的学术问题：将数字成绩（0 到 100 之间）转换为字母等级（A, B, C, D 或 F）。我们首先从设计该问题的解决方案开始。流程图设计如图 17.12 所示。图中还显示了解决方案的代码。在学习代码示例时，请脚本代码在每个嵌套格式下都进行了缩进。

## 多路选择

C shell 使用 `switch` 语句实现了多路选择。给定一个字符串和一个模式备选列表，`switch` 语句会按顺序将字符串与每个模式进行匹配。第一个匹配到字符串的模式将执行相应的操作。如果没有模式匹配，`switch` 语句将执行下一个命令。多路语句的决策逻辑如图 17.13 所示，并带有设计流程图。

## switch 语法

`switch` 语法格式如图 17.14 所示。命令以括号括起来的待评估字符串开始，以 `endsw` 结束。在开始和结束 `switch` 之间是模式列表。

![](img/6e4cdc423ec40606ea72b32fdafff220_754_0.png)

图 17.13 switch 决策逻辑

```
switch ($digit)
case 0:
echo Zero
breaksw
case 1:
echo One
breaksw
case 9:
echo Nine
breaksw
case Not a Digit:
default:
echo Not a digit
breaksw
endsw
```

![](img/6e4cdc423ec40606ea72b32fdafff220_754_1.png)

图 17.14 输出数字文本

## case 语法

对于每个需要测试的模式，在模式列表中定义一个单独的模式。模式通过关键字 `case` 识别，后跟模式并以冒号结束：`case` 语法为：

```
case string_const:
```

## 第 17 章 · C SHELL 编程

每个模式关联着一个或多个命令。这些命令必须在 `case` 语句之后单独成行，并遵循命令的常规规则。通常，它们每行编码一个。模式列表中的最后一个操作通常是当其他所有 `case` 都不匹配时执行的默认命令。

`switch` 是一个必须仔细解决以避免混淆的谜题。把它想象成一系列闸桥，每个模式对应一个桥。根据模式评估的结果，第一个匹配的闸桥将被关闭，从而为脚本的流通过提供路径。一旦闸桥关闭，其后的任何模式都将无法被匹配。在执行完来自关闭闸桥的匹配命令后，路径将继续向下。如果没有模式匹配（即没有闸桥被关闭），则 `switch` 语句继续执行下一个命令。`switch` 流如图 17.14 所示。

为了看到从一个语句到下一个语句的连续流，请检查脚本 17.11 中的代码。

## 脚本 17.11 展示 switch 流

```
# !/bin/bash/
# Script: default.scr
# 演示 case default 操作。
echo "Enter a character: \c"
set char = $
switch ($char)
  case A
    echo You entered $char
  case B
    echo You entered $char
  default:
    echo You did not enter A or B.
endsw
% default.scr
Output:
Enter a character: A
You entered A
You entered A
You did not enter A or B.
```

**脚本 17.11 分析：** 当我们运行脚本时，输入了 A，它匹配了第一个模式。在执行 `echo` 命令后，控制进入第二个 `case`。由于流是连续的，输入并没有匹配第二个 `case` 或默认项。三个语句都执行了。

## break 语法

一旦进入 `case` 语句，命令流将持续直到 `break` 命令或 `switch` 结束。`break` 语句中断流并跳转到 `switch` 命令之后的语句。由于这种无条件的跳转，`break` 命令之后不应有语句。

另一个典型的 `switch` 语句示例是给定一个数字，输出其文本。脚本和示例执行在脚本 17.12 中。

## 脚本 17.12 展示 switch 语句

| | |
|---|---|
| 1 | #!bin/bash |
| 2 | # Script: switchDigit.scr |
| 3 | # 展示 switch 语句 |
| 4 | |
| 5 | echo -n "Enter a digit and I'll spell it for you: " |
| 6 | |
| 7 | set digit = $ |
| 8 | echo -n "\nYou entered $digit. It is spelled " |
| 9 | |
| 10 | switch ($digit) |
| 11 | case 0: |
| 12 | echo Zero. |
| 13 | breaksw |
| 14 | case 1: |
| 15 | echo One. |
| 16 | breaksw |
| 17 | case 2: |
| 18 | echo Two. |
| 19 | breaksw |
| 20 | case 3: |
| 21 | echo Three. |
| 22 | breaksw |
| 23 | case 4: |
| 24 | echo Four. |
| 25 | breaksw |
| 26 | |
| 27 | case 5: |
| 28 | echo Five. |
| 29 | breaksw |
| 30 | |
| 31 | case 6: |
| 32 | echo Six. |
| 33 | breaksw |
| 34 | |
| 35 | case 7: |
| 36 | echo Seventh. |
| 37 | breaksw |
| 38 | |
| 39 | case 8: |
| 40 | echo Eight. |
| 41 | breaksw |
| 42 | |
| 43 | case 9: |
| 44 | echo Nine. |
| 45 | breaksw |
| 46 | |
| 47 | default: |

**脚本 17.12 展示 switch 语句——续**

```
42 echo Not a digit.
43 breaksw
44 endsw
$ switchDigit.scr
Output:
Enter a digit and I'll spell it for you: 1
You entered 1. It is spelled One
```
