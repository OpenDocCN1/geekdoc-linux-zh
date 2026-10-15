
`) echo "Usage:opts3 -dq filename ... " 1>&2;;`

`esac`

`done`

```
# EXAMPLE 8.63 (CONTINUED)

(The Command Line)
```

```
4 $ opts3 -d

-d is a valid switch
```

```
5 $ opts3 -q foo

The argument for -q is foo
```

```
6 $ opts3 -q

Usage: opts3 -dq filename ...
```

```
7 $ opts3 -e

Usage: opts3 -dq filename ...
```

```
8 $ opts3 e
```

### EXPLANATION

1 `while` 命令测试 `getopts` 的退出状态。如果 `getopts` 能成功处理一个参数，它返回 `0` 退出状态，`while` 循环的主体将被进入。附加到参数列表的冒号意味着 `q` 选项需要一个参数。该参数将存储在特殊变量 `OPTARG` 中。

2 合法的选项之一是 `d`。如果 `d` 作为选项输入，则 `d`（不带连字符）存储在 `options` 变量中。

3 合法的选项之一是 `q`。`q` 选项需要一个参数。`q` 选项与其参数之间必须有空格。如果 `q` 作为选项后跟参数输入，则 `q`，不带连字符，存储在 `options` 变量中，参数存储在 `OPTARG` 变量中。如果 `q` 选项后没有参数，则问号存储在 `options` 变量中。

4 `d` 选项是 `opts3` 的合法选项。

5 带参数的 `q` 选项也是 `opts3` 的合法选项。

6 没有参数的 `q` 选项是一个错误。

7 `e` 选项无效。如果选项非法，则问号存储在 `options` 变量中。

8 选项前面既没有连字符也没有加号。`getopts` 命令不会将其处理为选项并返回非零退出状态。`while` 循环终止。

# 示例 8-4

```
（The Script）

#!/bin/sh

# Program opts4

# Using getopts - Fourth try

while getopts xyz: arguments 2>/dev/null

do

    case $arguments in

        x) echo "you entered -x as an option.";;

        y) echo "you entered -y as an option.";;

        z) echo "you entered -z as an option.";;

           echo "\$OPTARG is \$OPTARG,";;

        \?) echo "Usage: opts4 [-xy] [-z argument]"

            exit 1;;

    esac

done

echo "The initial value of \$OPTIND is 1.

The final value of \$OPTIND is \$OPTIND.

Since this reflects the number of the next command-line argument,

the number of arguments passed was `expr \$OPTIND - 1`."
```

```
（The Command Line）

$ opts4 -xyz foo

you entered -x as an option.

you entered -y as an option.

you entered -z as an option.

\$OPTARG is foo.

The initial value of OPTIND is 1.

The final value of OPTIND is 3.

Since this reflects the number of the next command-line argument, the number of arguments passed was 2.

$ opts4 -x -y -z boo

you entered -x as an option.

you entered -y as an option.

you entered -z as an option.

\$OPTARG is boo.

The initial value of OPTIND is 1.

The final value of OPTIND is 5.

Since this reflects the number of the next command-line argument, the number of arguments passed was 4.

$ opts4 -d

Usage: opts4 [-xy] [-z argument]
```

# 解释

- 1. `while` 命令测试 `getopts` 的退出状态。如果 `getopts` 能成功处理一个参数，则返回 `0` 退出状态，`while` 循环体将被进入。附加在 `z` 选项后的冒号告诉 `getopts` 必须在 `-z` 选项后跟一个参数。如果选项需要参数，则该参数会存储在 `getopts` 内建变量 `OPTARG` 中。
- 2. 如果 `x` 作为选项给出，则它会被存储在变量 `arguments` 中。
- 3. 如果 `z` 作为选项并带参数给出，则参数会被存储在内建变量 `OPTARG` 中。
- 4. 如果输入了无效选项，则问号会被存储在变量 `arguments` 中，并显示错误信息。
- 5. 特殊的 `getopts` 变量 `OPTIND` 保存下一个要处理的选项的编号。其值始终比实际命令行参数的数量多一。

#### 8.9.2 eval 命令和解析命令行

`eval` 命令会评估命令行，执行所有 shell 替换，然后执行命令行。本质上，它会将命令行解析两次。当正常的命令行解析不足时，就会使用它。

# 示例 8.63

```
1 $ set a b c d

2 $ echo The last argument is \$#

   The last argument is $4

3 $ echo The last argument is $4

   The last argument is d

4 $ eval echo The last argument is \$#

   The last argument is d

5 $ set -x

$ echo The last argument is \$#

+ eval echo the last argument is $4

+ echo the last argument is d

   The last argument is d
```

# 解释

- 1. 设置了四个位置参数。
- 2. 期望的结果是打印最后一个位置参数的值。`\$` 会打印字面量的美元符号。`$#` 会求值为 `4`，即位置参数的数量。shell 在求值 `$4` 之后，不会再次解析该行以获取 `$4` 的值。
- 3. 打印的是 `$4` 而不是最后一个参数。
- 4. 在 shell 执行变量替换后，`eval` 命令会执行变量替换然后执行 `echo` 命令。
- 5. 打开回显以观察解析的顺序。

# 示例 8.66

```
(From SVR4 Shutdown Program)

1 eval `/usr/bin/id | /usr/bin/sed 's/[^a-z0-9=].*/'"

2 if [ "$uid"-0 -ne 0 ]

3 then

    echo $0: Only root can run $0

    exit 2

fi
```
