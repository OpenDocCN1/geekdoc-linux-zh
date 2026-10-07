
由 C 语言定义。这些表达式主要用在 `if` 和 `while` 命令中，稍后将在本章的“条件语句”和“迭代语句”部分进行介绍。

`tcsh` 表达式支持与 `bash` 和 `pdksh` test 命令相同类型的运算符。这些包括整数、字符串、文件和逻辑表达式。`tcsh` 表达式支持的整数运算符列于表 14.6 中。

### 表 14.6. TCSH 表达式的整数运算符。

| 运算符 | 含义 |
| :--- | :--- |
| int1 <= int2 | 如果 int1 小于或等于 int2，则返回 True。 |
| int1 >= int2 | 如果 int1 大于或等于 int2，则返回 True。 |
| int1 < int2 | 如果 int1 小于 int2，则返回 True。 |
| int1 > int2 | 如果 int1 大于 int2，则返回 True。 |

`tcsh` 表达式支持的字符串运算符列于表 14.7 中。

### 表 14.7. TCSH 表达式的字符串运算符。

| 运算符 | 含义 |
| :--- | :--- |
| str1 == str2 | 如果 str1 等于 str2，则返回 True。 |
| str1 != str2 | 如果 str1 不等于 str2，则返回 True。 |

`tcsh` 表达式支持的文件运算符列于表 14.8 中。

### 表 14.8. TCSH 表达式的文件运算符。

| 运算符 | 含义 |
| :--- | :--- |
| -r file | 如果文件可读，则返回 True。 |
| -w file | 如果文件可写，则返回 True。 |
| -x file | 如果文件可执行，则返回 True。 |
| -e file | 如果文件存在，则返回 True。 |
| -o file | 如果文件归当前用户所有，则返回 True。 |
| -z file | 如果文件大小为 0，则返回 True。 |
| -f file | 如果文件是普通文件，则返回 True。 |
| -d file | 如果文件是目录文件，则返回 True。 |

`tcsh` 表达式支持的逻辑运算符列于表 14.9 中。

### 表 14.9. TCSH 表达式的逻辑运算符。

| 运算符 | 含义 |
| :--- | :--- |
| exp1 \|\| exp2 | 如果 exp1 为真或 exp2 为真，则返回 True。 |
| exp1 && exp2 | 如果 exp1 为真且 exp2 为真，则返回 True。 |
| ! exp | 如果 exp 不为真，则返回 True。 |

## 条件语句

`bash`、`pdksh` 和 `tcsh` 各有两种形式的条件语句。即 `if` 语句和 `case` 语句。这些语句用于根据特定条件是否为真来执行 shell 程序的不同部分。与大多数语句一样，这些语句在不同 shell 中的语法略有不同。

### if 语句

所有三种 shell 都支持嵌套的 `if-then-else` 语句。这些语句提供了一种在 shell 程序中执行复杂条件测试的方法。`if` 语句的语法在 `bash` 和 `pdksh` 中是相同的，如下所示：

```
if [ expression ]
then
    commands
elif [ expression2 ]
then
    commands
else
    commands
fi
```

> **注意**
>
> `elif` 和 `else` 子句都是 `if` 语句的可选项。另外请注意，`bash` 和 `pdksh` 在其大多数复杂语句中使用语句名称的反义词来标记语句的结束。在此语句中，使用 `fi` 关键字来标记 `if` 语句的结束。

`elif` 语句是 `else if` 的缩写。只有当与 `if` 语句或其之前的任何 `elif` 语句相关的表达式都不为真时，才会执行此语句。只有当与 `if` 语句或任何 `elif` 语句相关的表达式都不为真时，才会执行与 `else` 语句关联的命令。

在 `tcsh` 中，`if` 语句有两种不同的形式。第一种形式提供了与 `bash` 和 `pdksh` `if` 语句相同的功能。这种形式的 `if` 语句具有如下语法：

```
if (expression1) then
commands
else if (expression2) then
commands
else
commands
endif
```

`tcsh` 提供的第二种 `if` 语句形式是第一种 `if` 语句的简单版本。这种形式的 `if` 语句只评估单个表达式。如果表达式为真，它执行单个命令；如果表达式为假，则不执行任何操作。这种形式的 `if` 语句的语法如下：

```
if (expression) command
```

该语句可以通过编写没有 `else` 或 `else if` 子句的 `if` 语句来使用第一种 `if` 语句形式来编写。这种形式只是节省了一些打字工作。

以下是一个 `bash` 或 `pdksh` `if` 语句的示例。该语句检查当前目录中是否存在 `.profile` 文件：

```
if [ -f .profile ]
then
    echo "There is a .profile file in the current directory."
else
    echo "Could not find the .profile file."
fi
```

使用 `tcsh` 语法编写的相同语句如下所示：

```
#
if ( { -f .profile } ) then
    echo "There is a .profile file in the current directory."
else
    echo "Could not find the .profile file."
endif
```

> **注意**
>
> 请注意，在 `tcsh` 示例中，第一行以 `#` 开头。这是为了让 `tcsh` 识别包含命令的文件为 `tcsh` 脚本文件所必需的。

### case 语句

`case` 语句允许你将一个模式与多个其他模式进行比较，并在找到匹配项时执行一段代码。shell 中的 `case` 语句比 Pascal 中的 `case` 语句或 C 语言中的 `switch` 语句强大得多。这是因为在 shell 的 `case` 语句中，你可以比较包含通配符的字符串，而在 Pascal 和 C 的对应语句中，你只能比较枚举类型或整数值。

再次强调，`case` 语句的语法在 `bash` 和 `pdksh` 中是相同的，而在 `tcsh` 中是不同的。`bash` 和 `pdksh` 的语法如下：

```
case string1 in
    str1)
        commands;;
    str2)
        commands;;
    *)
        commands;;
esac
```

`string1` 与 `str1` 和 `str2` 进行比较。如果这些字符串之一与 `string1` 匹配，则执行直到双分号（`;;`）之前的所有命令。如果 `str1` 和 `str2` 都不与 `string1` 匹配，则执行与星号关联的命令。这是默认的 case 条件，因为星号匹配所有字符串。

`bash` 和 `pdksh` `case` 语句的 `tcsh` 等价物被称为 `switch` 语句。该语句的语法紧密遵循 C 语言 `switch` 语句的语法。如下所示：

```
switch (string1)
    case str1:
        statements
    breaksw
    case str2:
        statements
    breaksw
    default:
        statements
    breaksw
endsw
```

其工作方式与 `bash` 和 `pdksh` `case` 语句相同。关键字 `case` 后的每个字符串都与 `string1` 进行比较。如果这些字符串中有任何一个与 `string1` 匹配，则代码执行直到遇到 `breaksw` 关键字。如果没有字符串匹配，则代码执行直到遇到 `default` 关键字后的 `breaksw` 关键字。

以下代码是一个 `bash` 或 `pdksh` `case` 语句的示例。该代码检查第一个命令行选项是否是 `-i` 或 `-e`。如果是 `-i`，程序将统计由第二个命令行选项指定的文件中以字母 `i` 开头的行数。如果第一个选项是 `-e`，程序将统计由第二个命令行选项指定的文件中以字母 `e` 开头的行数。如果第一个命令行选项不是 `-i` 或 `-e`，程序将在屏幕上打印一条简短的错误消息。

```
sh
case $1 in
    -i)
        count=`grep '^i' $2 | wc -l`
        echo "The number of lines in $2 that start with an i is $count"
        ;;
    -e)
        count=`grep '^e' $2 | wc -l`
        echo "The number of lines in $2 that start with an e is $count"
        ;;
    *)
        echo "That option is not recognized"
        ;;
esac
```

使用 `tcsh` 语法编写的相同示例如下所示：

```
sh
# remember that the first line must start with a # when using tcsh
switch ($1)
    case -i | i:
        set count = `grep '^i' $2 | wc -l`
        echo "The number of lines in $2 that begin with i is $count"
        breaksw
    case -e | e:
        set count = `grep '^e' $2 | wc -l`
        echo "The number of lines in $2 that begin with e is $count"
        breaksw
    default:
        echo "That option is not recognized"
        breaksw
endsw
```

![](img/e8e6b47ac20475e23d48b4c476f5d891_312_0.png)

