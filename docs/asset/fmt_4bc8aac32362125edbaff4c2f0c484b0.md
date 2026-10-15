
`set n=`echo "scale=3; 13 / 2" | bc``

`echo $n`

6.500

```

```

`set product=`nawk -v x=2.45 -v y=3.124 'BEGIN{\nprintf "%.2f\n", x + y }'``

% `echo $product`

7.65

```

# 说明

1 `echo`命令的输出通过管道传给`bc`程序。将`scale`设置为3，即要打印的小数点右侧的有效数字位数。计算是将13除以2。整个管道命令用反引号括起来。将执行命令替换，并将输出赋给变量`n`。

2 `awk`程序从命令行传入的参数列表中获取其值。传给`awk`的每个参数都以`-v`开关开头；例如，`-v x=2.45`和`-v y=3.124`。数字相乘后，`printf`函数格式化并打印结果，精度为小数点右侧2位。输出赋给变量`product`。

## 10.4 调试脚本

C/TC shell脚本常常会因为一些简单的语法错误或逻辑错误而失败。表10.3提供了`csh`命令的选项，可帮助你调试程序。

### 表10.3 echo(-x)和verbose(-v)

| 选项 | 作用 |
|---|---|
| 作为csh和tcsh的选项 | |
| `csh -x scriptname`<br>`tcsh -x scriptname` | 在变量替换之后、执行之前显示脚本的每一行。 |
| `csh -v scriptname`<br>`tcsh -v scriptname` | 在执行之前，按你输入的原始形式显示脚本的每一行。 |
| `csh -n scriptname`<br>`tcsh -n scriptname` | 解释但不执行命令。 |
| 作为`set`命令的参数 | |
| `set echo` | 在变量替换之后、执行之前显示脚本的每一行。 |
| `set verbose` | 在执行之前，按你输入的原始形式显示脚本的每一行。 |

### 表10.3 echo(-x)和verbose(-v)（续）

| 选项 | 作用 |
|---|---|
| 作为脚本的第一行 | |
| `#!/bin/csh -xv` | 同时打开`echo`和`verbose`。这些选项可以单独调用，也可以 |
| `#!/bin/tcsh -xv` | 与其他`csh`调用参数组合使用。 |

### 示例10.7

（-v和-x选项）

```
1

% cat practice

#!/bin/csh

echo Hello $LOGNAME

echo The date is `date`

echo Your home shell is $SHELL

echo Good-bye $LOGNAME
```

```
2

% csh -v practice

echo Hello $LOGNAME

Hello ellie

echo The date is `date`

The date is Sun May 23 12:24:97 PDT 2004

echo Your login shell is $SHELL

Your login shell is /bin/csh

echo Good-bye $LOGNAME

Good-bye ellie
```

```
3

% csh -x practice

echo Hello ellie

Hello ellie

echo The date is `date`

date

The date is Sun May 23 12:24:15 PDT 2004

echo Your login shell is /bin/csh

Your login shell is /bin/csh

echo Good-bye ellie

Good-bye ellie
```

# 说明

+ 1 显示了C shell脚本的内容。其中包含了变量和命令替换行，以便你了解`echo`和`verbose`之间的区别。
+ 2 `csh`命令的`-v`选项会启用`verbose`功能。脚本的每一行都按脚本中输入的原始形式显示，然后执行该行。
+ 3 `csh`命令的`-x`选项会启用`echo`功能。在完成变量和命令替换之后，脚本的每一行才会显示，然后执行该行。因为该功能让你可以检查命令和变量替换的结果是什么，所以它比`verbose`选项更常用。

# 示例 10.8

(Echo 和 Verbose)

```
1 % cat practice

#!/bin/csh

echo Hello $LOGNAME

echo The date is `date`

set echo

echo Your home shell is $SHELL

unset echo

echo Good-bye $LOGNAME

% chmod +x practice
```

```
2 % practice

Hello ellie

The date is Sun May 26 12:25:16 PDT 2004

---> echo Your login shell is /bin/csh

---> Your login shell is /bin/csh

---> unset echo

Good-bye ellie
```

# 解释

- 1 在脚本内部设置并取消了 `echo` 选项。这使你能够调试脚本中遇到瓶颈的某些部分，而不必回显整个脚本的每一行。
- 2 ---> 标记 `echo` 被打开的位置。每一行在变量和命令替换后打印，然后执行。

# 示例 10.9

```
1 % cat practice

#!/bin/csh

echo Hello $LOGNAME

echo The date is `date`

set verbose

echo Your home shell is $SHELL

unset verbose

echo Good-bye $LOGNAME
```

```
2 % practice

Hello ellie

The date is Sun May 23 12:30:09 PDT 2004

---> echo Your login shell is $SHELL

---> Your login shell is /bin/csh

---> unset verbose

Good-bye ellie
```

# 解释

- 1. 在脚本内部设置并取消了 `verbose` 选项。
- 2. --> 标记 `verbose` 被打开的位置。行按在脚本中输入的方式打印，然后执行。

# 10.5 命令行参数

Shell 脚本可以接受命令行参数。参数用于以某种方式修改程序的行为。C shell 将命令行参数分配给位置参数，并且不对可以分配的参数数量施加特定限制（Bourne shell 将位置参数限制为九个）。位置参数是编号变量。脚本名称分配给 `$0`，后跟脚本名称的任何单词都分配给 `$1`、`$2`、`$3` ... `${10}`、`${11}` 等。`$1` 是第一个命令行参数。除了使用位置参数外，C shell 还提供内置数组 `argv`。

### 10.5.1 位置参数和 argv

如果使用 `argv` 数组表示法，必须提供有效的下标以对应从命令行传入的参数，否则 C shell 会发送下标超出范围的错误消息。`argv` 数组不包括脚本名称。第一个参数是 `$argv[1]`，参数数量由 `$#argv` 表示。（没有其他方式表示参数数量。）参见表 10.4。

# 表 10.4 命令行参数

| Argument | Meaning |
|---|---|
| `$0` | 脚本的名称。 |
| `$1`, `$2`, ... `${10}` ... | 第一个和第二个位置参数由数字后加美元符号引用。大括号保护数字 10，以免它打印第一个位置参数后跟一个 0。 |
| `$*` | 所有位置参数。 |
| `$argv[0]` | 无效；不打印任何内容。C shell 数组下标从 1 开始。 |
| `$argv[1]` `$argv[2]`... | 第一个参数、第二个参数，等等。 |
| `$argv[*]` | 所有参数。 |
| `$argv` | 所有参数。 |
| `$#argv` | 参数的数量。 |
| `$argv[$#argv]` | 最后一个参数。 |

# 示例 10.10

(脚本)

```
#!/bin/csh -f

# The greetings script

# This script greets a user whose name is typed in at the command line.

echo $0 to you $1 $2 $3

echo Welcome to this day `date | awk '{print $1, $2, $3}'`

echo Hope you have a nice day, $argv[1]!

echo Good-bye $argv[1] $argv[2] $argv[3]
```

(命令行)

```
% chmod +x greetings

% greetings Guy Quigley

greetings to you Guy Quigley

Welcome to this day Fri Aug 28
```
