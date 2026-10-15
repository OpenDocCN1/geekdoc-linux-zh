

## 示例 8.38（续）

（命令行和输出）

```
2 $ sh -x todebug
+ name=Joe Blow
+ [ Joe Blow = Joe Blow ]
+ echo Hi Joe Blow

Hi Joe Blow
num=1
+ [ 1 -lt 5 ]
+ expr 1 + 1
num=2
+ [ 2 -lt 5 ]
+ expr 2 + 1
num=3
+ [ 3 -lt 5 ]
+ expr 3 + 1
num=4
+ [ 4 -lt 5 ]
+ expr 4 + 1
num=5
+ [ 5 -lt 5 ]
+ echo The grand total is 5
The grand total is 5
```

## 解释

1 脚本名为 todebug。你可以使用打开的 -x 开关来观察脚本的运行情况。循环的每次迭代都会显示出来，变量的值在设置时以及更改时都会打印出来。

2 sh 命令使用 -x 选项启动 Bourne shell。回显已打开。脚本的每一行都将显示到屏幕上，并在前面加上加号（+）。在显示行之前会执行变量替换。命令执行的结果会在行显示后出现。

## 8.9 命令行

### 8.9.1 使用 getopts 处理命令行选项

如果你正在编写需要大量命令行选项的脚本，位置参数并不总是最高效的。例如，UNIX ls 命令接受多个命令行选项和参数。（选项需要以连字符开头；参数不需要。）选项可以通过多种方式传递给程序：ls -laF1、ls -l -a -l -F ls -la -F 等等。如果你有一个需要参数的脚本，位置参数可能用于单独处理参数，例如 ls -l -a -F。每个

连字符选项将分别存储在 $1、$2 和 $3 中。但如果用户将所有选项列为一个连字符选项，如 ls -1f 呢？现在 -1f 将全部分配给脚本中的 $1。getopts 函数使得可以像 ls 程序处理它们一样处理命令行选项和参数。getopts 函数将允许 runit 程序使用各种组合来处理其参数。

## 示例 8.59

（命令行）

```
1  $ runit -x -n 200 filex
2  $ runit -xn200 filex
3  $ runit -xy
4  $ runit -yx -n 30
5  $ runit -n250 -xy filey
```

（这些参数的任何其他组合）

## 解释

- 1. 程序 runit 接受四个参数：x 是一个选项，n 是一个需要其后跟数字参数的选项，filex 是一个独立的参数。
- 2. 程序 runit 将选项 x 和 n 以及数字参数 200 组合在一起；filex 也是一个参数。
- 3. 程序 runit 使用组合的 x 和 y 选项调用。
- 4. 程序 runit 使用组合的 y 和 x 选项调用；n 选项单独传递，数字参数 30 也是如此。
- 5. 程序 runit 使用与数字参数组合的 n 选项调用，x 和 y 选项组合，filey 单独。

在详细介绍 runit 程序之前，我们先检查程序中 getopts 用到的那一行，看看它是如何处理参数的。

## 示例 8.60

（来自名为 "runit" 的脚本的一行）

```
while getopts :xyn: name
```

## 解释

- - x、y 和 n 是选项。选项是可以从命令行传递给此脚本的允许参数；例如，runit -x -y -n。
- - 命令行中输入的选项以连字符开头：-x -y -z、-xyz、-x -yz 等等。如果选项后有一个冒号，则表示该选项需要一个命名参数，例如 -x filename，其中 -x 是选项，filename 是命名参数。
- - 任何不包含连字符的选项都会告诉 getopts 选项列表已结束。
- - 每次调用 getopts 时，它都会将找到的下一个选项放入变量 name 中。（你可以在此处使用任何变量名。）如果给出非法参数，name 将被分配一个问号。
- - OPTIND 是一个特殊变量，初始化为 1，并且每次 getopts 完成对命令行参数的处理时都会递增到 getopts 将处理的下一个参数的编号。
- - 如果选项需要参数，getopts 会将其放入 OPTARG 变量中。如果选项列表中的第一个字符是冒号，shell 变量 name 将被设置为冒号字符，并且 OPTARG 变量将被设置为非法选项的值。

getopts 脚本。以下示例说明 getopts 如何处理参数。

## 示例 8.61

（脚本）

```
#!/bin/sh
# Program opts1
# Using getopts -- First try --
1 while getopts xy options
do
2   case $options in
3   x) echo "you entered -x as an option";;
    y) echo "you entered -y as an option";;
    esac
done
```

（命令行）

```
4 $ opts1 -x
you entered -x as an option
5 $ opts1 -xy
you entered -x as an option
you entered -y as an option
6 $ opts1 -y
you entered -y as an option
7 $ opts1 -b
opts1: illegal option -- b
8 $ opts1 b
```
