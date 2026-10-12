
**File Name**: `set_demo`
**Inode Number**: `16517945`

# 表 12.5
`test` 命令的操作符

| 文件测试 | | 整数测试 | | 字符串测试 | |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 表达式 | 返回值 | 表达式 | 返回值 | 表达式 | 返回值 |
| `-d file` | 如果文件是目录则为真 | `int1-eq int2` | 如果 `int1` 和 `int2` 相等则为真 | | 如果 `str` 不为空字符串为真 |
| `-f file` | 如果文件是普通文件则为真 | `int1-ge int2` | 如果 `int1` 大于等于 `int2` 则为真 | `str1=str2` | 如果 `str1` 和 `str2` 相同则为真 |
| `-r file` | 如果文件可读则为真 | `int1-gt int2` | 如果 `int1` 大于 `int2` 则为真 | `str1!=str2` | 如果 `str1` 和 `str2` 不同则为真 |
| `-s file` | 如果文件长度不为零则为真 | `int1-le int2` | 如果 `int1` 小于等于 `int2` 则为真 | `-n str` | 如果 `str` 的长度为零为真 |
| `-t [filedesc]` | 如果文件描述符对应终端则为真 | `int1-lt int2` | 如果 `int1` 小于 `int2` 则为真 | `-z str` | 如果 `str` 的长度为零为真 |
| `-w file` | 如果文件可写则为真 | `int1-ne int2` | 如果 `int1` 不大于等于 `int2` 则为真 | | |
| `-x file` | 如果文件可执行则为真 | | | | | |
| `-b file` | 如果文件是块设备则为真 | | | | | |
| `-c file` | 如果文件是特殊文件则为真 | | | | | |
| `-e file` | 如果文件存在则为真 | | | | | |
| `-L file` | 如果文件是符号链接则为真 | | | | | |

# 形成复杂表达式的操作符

- `!` 逻辑非操作符：`( 表达式 )` 括号用于分组，如果后续表达式为假则为真；每个括号前后至少有一个空格
- `-a` 或 `&&` 逻辑与操作符：`-o` 或 `||` 逻辑或操作符：如果上一个（左）和下一个（右）表达式均为真则为真；如果上一个（左）或下一个（右）表达式任一为真则为真

## 365
# Bash 编程入门

**Permissions**: `-rwx-xr-x`
**Size (bytes)**: `245`
$ 

在之前的脚本中，如果你在没有任何命令行参数的情况下运行脚本，第一个语句将显示错误消息并退出程序。如果在多个参数的情况下运行脚本，第二个语句将显示错误消息并退出程序。如果前两个条件都不成立，则执行第三条语句——即带有一个参数运行脚本。只有当命令行参数是一个普通文件时，此语句才会产生预期结果。如果传递的参数不是普通文件，则第三条语句的条件为假，并显示错误信息 `if_demo: argument must be an ordinary file`。`exit` 命令用于退出脚本。我们通常使用 `1` 作为参数（即退出状态），当脚本因错误条件终止时；退出状态 `0` 用于脚本正常终止。

我们可以使用 `test` 命令的替代语法和逻辑与操作符来重写 `if_demo` 脚本，如表 12.5 和 12.6 所示。

```bash
$ cat if_demo1

#!/bin/bash

if [ "$#" -eq 1 -a -f "$1" ]

then

    echo "$0: Specify exactly one line argument that"

    echo "must be an ordinary file."

    exit 1

fi
```

# 表 12.6
Bash 操作符优先级（从高到低）

| 操作符 | 优先级 |
| :--- | :--- |
| `var++ --var` | C 风格后递增 |
| `var-- --var` | C 风格前递减 |
| `!` | 逻辑/按位取反，反转操作符的方向 |
| `**` | 幂 |
| `* / %` | 乘法、除法、取模 |
| `+` | 加法、减法 |
| `<<` | 按位左移、位右移 |
| `-z` | 字符串的一元比较 |
| `-e -t` | 文件测试的一元比较 |
| `-lt >=` | 整数复合比较 |
| `-nt` | 字符串复合比较 |
| `== !=` | 相等/不相等测试 |
| `&` | 按位与 |
| `^` | 按位异或（互斥或） |
| `\|` | 按位或 |
| `&&` | 逻辑与 |
| `||` | 逻辑或 |
| `?:` | C 风格三元运算符（条件语句） |
| `=` | 赋值 |
| `*= += &=` | 复合赋值：乘赋值、除赋值、模赋值 |
| `|` | 用于操作 |

# Bash 编程入门

## 337

![](img/2a18e06cd9c6395e451f26126ecba1fd_367_0.png)

图 12.2 `if-then-else-fi` 语句的语义。

接下来，我们使用 `if-then-else-fi` 语句重写 `if_demo` 程序，并使用 `test` 命令的替代语法。生成的脚本位于 `if_demo2` 文件中，如下会话所示。注意程序看起来更加整洁且易于读。

```bash
$ cat if_demo2

#!/bin/bash

if [[ $# -eq 1 ]] && [[ -f "$1" ]]

then

    filename=$1

    set -- 'ls -l $filename'

    perms="$5"

    size="$6"

    set 'ls -i $filename'

    inode="$1"

    echo "File Name: $filename"

    echo "Inode Number: $inode"

    echo "Permissions: $perms"

    echo "Size (bytes): $size"

    exit 0

else

    echo "$0:          Specify exactly one command line argument"

    echo "             must be an ordinary file."

    exit 1

fi
```

最后，我们讨论语句的第三版本，用于实现多路分支。以下是该语句的概要描述：

```bash
Syntax:

if expression1

then

    then-commands

elif expression2

    elif1-commands

elif expression3

    elif2-commands

else

    else-commands

fi
```

# 实现多路分支

如果 `expression1` 为真，则执行 `then-commands` 中的命令。如果 `expression1` 为假，则评估 `expression2`，如果它为真，则执行 `elif1-commands` 中的命令。如果 `expression2` 也为假，则评估 `expression3`。如果 `expression3` 为真，则执行 `elif2-commands` 中的命令。如果 `expression3` 也为假，则执行 `else-commands` 中的命令。任何命令列表的执行后都会跟着 `fi`。你可以在 `if` 语句中使用任意数量的 `elif` 来实现多路分支。该语句的语义如图 12.3 所示。

我们修改了 `if_demo` 文件中的脚本，如果命令行参数是一个目录，程序将显示目录中的文件和子目录数量（排除隐藏文件）。此外，程序在处理之前会确保命令行参数是当前目录下存在的文件或目录。除了使用两个语句外，我们还可以可以使用 `if-then-elif-else-fi` 语句。结果脚本位于 `if_demo` 文件中，如下节所示。注意在 `if` 语句的条件使用了逻辑取反运算符 `!`。该运算符也可以用于按位取反，如表 12.5 和表 12.6 所示。

# `cat if_demo3`

```bash
#!/bin/bash

if [ ! $# -eq 1 ]

then

    echo "Usage: $0 file"

    exit 1

elif [ -d "$1" ]

then

    nfiles=$(ls "$1" | wc -w)

    echo "The number of files in the $1 directory is $nfiles"

    exit 0

else

    ls "$1" 2>/dev/null | grep "$1" 2>/dev/null 1>&2

    if [ $# -ne 0 ]

    then

        echo "$1: not found"

        exit 1

    fi

fi
```
