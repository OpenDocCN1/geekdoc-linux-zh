
```
if (expression) command
```

在这种格式中，如果表达式求值为真，则只能执行单个命令。

## case 语句

`case`语句用于根据与指定变量匹配的离散值或值范围来执行语句。在大多数情况下，如果你有大量的条件，可以使用`case`语句代替`if`语句。

`pdksh`和`bash`中`case`语句的格式如下：

```
case str in
    str1 | str2
        语句;;
    str3[str4]
        语句;;
    *)
        语句;;
esac
```

你可以为每个条件指定多个离散值——例如`str1`、`str2`等，或者你可以使用通配符指定一个值。最后一个条件应该是`*`（星号），如果其他条件都不满足，则执行该条件。对于指定的每个条件，所有相关的语句直到双分号（`;`）都会执行。

你可以编写一个脚本，如果你提供月份编号作为参数，它将回显月份名称。如果你提供一个不在1到12之间的数字，你将得到一条错误消息。脚本如下：

```
#!/bin/sh
case $1 in
    01|1) echo "Month is January";;
    02|2) echo "Month is February";;
    03|3) echo "Month is March";;
    04|4) echo "Month is April";;
    05|5) echo "Month is May";;
    06|6) echo "Month is June";;
    07|7) echo "Month is July";;
    08|8) echo "Month is August";;
    09|9) echo "Month is September";;
    10) echo "Month is October";;
    11) echo "Month is November";;
    12) echo "Month is December";;
    *) echo "Invalid parameter";;
esac
```

你需要在每个条件下的语句末尾加上双分号（`;`）。否则，下一个条件下的语句也会被执行。

`tcsh`中`case`语句的格式如下：

```
switch ($str)
    case $str1|$str2:
        语句
        breaksw
    case $str3|$str4:
        语句
        breaksw
    default:
        语句
        breaksw
endsw
```

你可以为每个条件指定多个离散值——例如`str1`、`str2`等，或者你可以使用通配符指定一个值。最后一个条件应该是`default`，如果其他条件都不满足，则执行该条件。对于指定的每个条件，所有相关的语句直到`breaksw`都会执行。

前面给出的用于回显给定数字对应的月份的示例，在`pdksh`和`bash`中展示，可以用`tcsh`编写如下：

```
#! /bin/tcsh

set month = 5
switch ($month)
    case 1:
        echo "Month is January"
        breaksw
    case 2:
        echo "Month is February"
        breaksw
    case 3:
        echo "Month is March"
        breaksw
    case 4:
        echo "Month is April"
        breaksw
    case 5:
        echo "Month is May"
        breaksw
    case 6:
        echo "Month is June"
        breaksw
    case 7:
        echo "Month is July"
        breaksw
    case 8:
        echo "Month is August"
        breaksw
    case 9:
        echo "Month is September"
        breaksw
    case 10:
        echo "Month is October"
        breaksw
    case 11:
        echo "Month is November"
        breaksw
    case 12:
        echo "Month is December"
        breaksw
    default:
        echo "Oops! Month is October!!"
        breaksw
endsw
```

你需要在每个条件下的语句末尾加上`breaksw`。否则，下一个条件下的语句也会被执行。

## 其他语句

你应该了解另外两个语句：`break`语句和`exit`语句。

### break 语句

`break`语句可用于终止迭代循环，例如`for`、`until`或`repeat`命令。

### exit 语句

`exit`语句可用于退出 shell 程序。你可以选择性地在使用`exit`后使用一个数字。如果当前的 shell 程序是由另一个 shell 程序调用的，调用程序可以检查该代码并据此做出决策。

### 函数

与其他编程语言一样，shell 程序也支持*函数*。函数是 shell 程序的一部分，执行特定的过程，可以在 shell 程序中多次使用。编写函数有助于你编写 shell 程序而不重复代码。

以下是`pdksh`和`bash`中函数定义的格式：

```
func() {
	语句
}
```

你可以这样调用函数：

```
func param1 param2 param3
```

参数`param1`、`param2`等是可选的。你还可以将参数作为单个字符串传递——例如，`$0`。函数可以解析这些参数，就好像它们是传递给 shell 程序的位置参数一样。

以下示例是一个函数，如果你传递一个月份编号，它会显示月份名称或错误消息。以下是`pdksh`和`bash`中的示例：

```
#!/bin/sh
Displaymonth() {
case $1 in
01 | 1 ) echo "Month is January";;
02 | 2 ) echo "Month is February";;
03 | 3 ) echo "Month is March";;
04 | 4 ) echo "Month is April";;
05 | 5 ) echo "Month is May";;
06 | 6) echo "Month is June";;
07 | 7 ) echo "Month is July";;
08 | 8 ) echo "Month is August";;
09 | 9 ) echo "Month is September";;
10) echo "Month is October";;
11) echo "Month is November";;
12) echo "Month is December";;
*) echo "Invalid parameter";;
    esac
}

Displaymonth 8
```

前面的程序显示以下内容：

Month is August

## 摘要

本章向你介绍了 shell 编程的语法，你学习了如何编写 shell 程序。Shell 程序可用于编写执行简单任务（例如在你登录时设置许多别名）或复杂任务（例如自定义你的 shell 环境并执行系统管理任务）的程序。

# 第 26 章 任务自动化

### 本章内容

- 第一个示例——自动化数据录入 814
- 提高自动化技巧的技巧 817
- Shell 脚本 819
- 使用 cron 和 at 任务安排任务 823
- 其他机制：Expect、Perl 等 826
- 自动化人员的结论性挑战——解释价值 831

> “([程序员三大美德：*懒惰*、*急躁*和*自负*])”
> —Wall 和 Schwartz，见 *Programming Perl*
