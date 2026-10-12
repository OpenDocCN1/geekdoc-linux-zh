
| -x | 存在的可执行文件 |

使用选项来测试参数，如下例所示：

```bash
$ cat checker
#!/bin/sh
# checker - 检查是否有参数传递给 checker
if [ $# -gt 0 ]
then
    echo "You put $# arguments on my command line."
    exit 1
fi
echo "You did not put any arguments on my command line."
```

$ ./checker

你未在我的命令行中提供任何参数。

$ ./checker foo bar bat

你在我的命令行中提供了 3 个参数。

熟悉所有选项是个好主意。这样你调试脚本会更容易，并且你的参数也将被常规验证。

测试工具可以检查两个文件，查看它们之间的关系，以及其中一个是否比另一个更新。如前所述，你也可以选择在方括号中放入参数，这与使用 `test` 同义。方括号前后必须有空格或制表符，如下例所示（在此脚本中，−eq 等于 0）：

$ cat checker

if [ $# −eq 0 ]

then

	echo "usage: checker args" 1>&2

	exit 1

fi

echo "aokay"

$ checker

usage: checker args

$ checker abc

aokay

usage 消息显示并使用 `1>&2` 符号将其输出重定向到标准错误。许多 Solaris 实用程序提供的 usage 消息与 `checker` 中的类似。如果你调用程序或实用程序时参数或数量错误，你将看到 usage 消息。

`if...then` 语句的另一个组成部分是 `...else`。通过向控制结构添加 `...else`，你使该结构分支为两个片段。如果 `if` 条件为真，则执行命令；如果为假，则执行另一组命令。图 18.2 展示了 `if...then...else` 流程图。

`if...then...else` 控制结构的正确语法如下：

If `<test−command>`

then

	commands

else

	commands

fi

## 图 18.2

*if...then...else 流程图*

![](img/256e02a6afce528d264a8d911fa0ff20_722_0.png)

为了节省空间，你可以用分号将 *then* 放在与 *if* 相同的行上。由于它们是独立的内置命令，如果未使用换行符，它们需要分号：

if `<test-command>`; then

    commands

else

    commands

fi

你可以通过运行带有文件名参数的 *out* 命令在终端上显示文件。当第一个参数是 *-v*（或选项）时，*out* 使用 *pg*（类似于 *more*）来显示文件。*out* 命令测试第一个参数以查看它是否是 *-v*。如果为真，*out* 命令移位参数以删除 *-v*，并使用 *pg* 显示文件。每页之后按下 Return 键可以查看新页面。脚本如下：

$ cat out

if [ $# -eq 0 ]

then

    echo ‘usage: out [-v] file ...’ >&2

    exit 1

fi

if [ ‘$1‘ = “-v” ]

then

    shift

    pg -- $@

else

    cat -- $@

fi

`cat` 和 `pg` 的 `--` 参数告知实用程序不再跟随选项。实用程序不会将前导连字符视为选项，因此你可能会看到带有前导连字符的文件名。你也可以使用命令 `cat > -filename` 创建这样的文件。`--` 参数不适用于 `more`，但适用于其他 Solaris 实用程序。使用双连字符和 `rm` 命令可以删除以连字符开头的不需要的文件。

## if...then...elif 结构

向 `if...then` 语句添加另一个参数可以构建“嵌套”控制结构集。通过用 `elif`（意为 else if）替换 `else`，你可以构建包含多个嵌套语句的命令行，只需一个 `fi` 即可关闭。该语句测试两个条件，如果两个条件均未满足，则向下执行到 `else`。以下示例展示了 `elif <test-command>` 语法：

if `<test-command>`

then

    commands

elif `<test-command>`

then

    commands

.

.

.

else

    commands

fi

以下示例演示了 `elif` 命令结构及其输出：

$ cat ify3

    echo 'case 1: \c'

    read case1

    echo 'case 2: \c'

    read case2

    echo 'case 3: \c'

    read case3

    if [ "$case1" = "$case2" -a "$case2" = "$case3" ]

    then

        echo "Same: case 1 & 2 & 3"

elif [ "$case1" = "$case2" ]

then

    echo 'Same: case 1 & 2'

elif [ "$case1" = "$case3" ]

then

    echo 'Same: case 1 & 3'

elif [ "$case2" = "$case3" ]

then

    echo 'Same: case 2 & 3'

else

    echo 'nada'

fi

$ ify3

case 1: letter

case 2: number

case 3: symbol

nada

$ ify3

case 1:    letter

case 2:    number

case 3: letter

Same: case 1 & 3

$ ify3

case 1: letter

case 2: letter

case 3: letter

Same: case 1 & 2 & 3

如果三个案例不相同，第一个 `elif` 测试任何一对词是否相同。如果任何 `if` 语句为真，则结构将控制权传递给 `next...then` 语句，最终传递给 `fi`。`ify3` 参数中的双引号告诉 shell 不要将特殊字符按字面意思解释。图 18.3 展示了 `if...then...elif` 流程图。

## for...in 结构

`for...in` 结构还有两个其他组成部分：`do` 和 `done`。其语法如下：

for `<loop-var>` in `<args-list>`

do

    `<commands>`

done

## 图 18.3

*if...then...elif 流程图*

![](img/256e02a6afce528d264a8d911fa0ff20_725_0.png)

第一个参数的值被赋予 `loop-var`，并执行 `do` 和 `done` 语句之间的命令。`do` 和 `done` 标记 `for` 循环的开始和结束。将控制权传递给 `done` 语句后，结构将 `args-list` 中第二个参数的值赋予 `loop-index` 并重复命令。它将为 `<args-list>` 中的每个参数重复执行 `do` 和 `done` 语句之间的命令。

以下示例展示了由 `for..in` 控制结构启动的序列：

$ cat dogs

for dogs in schnauser poodle dachshund spaniel

do

    echo "$dogs"

done

echo 'Finished.'

$ dogs

schnauser

poodle

 dachshund

 spaniel

 Finished.

前面的示例将 schnauzer 赋给变量 dogs，然后显示 dogs 的值，即 schnauzer。然后将 poodle 赋给 dogs 并重复该过程。当完成 `<args-list>` 时，结构将控制权转移到 `done` 之后的语句，该语句显示一条消息。

## for 结构

`for` 控制结构可用于自动依次获取每个参数的值。它将依次执行涉及每个参数的命令。以下示例展示了 shell 如何扩展隐含的 `$@` 为命令行参数列表：

$ cat args_list

 for args

 do

     echo "$args"

 done

 $ args_list china plastic stoneware china

 china

 plastic

 stoneware

 china

## while 结构

`while` 控制结构具有以下语法：

while `<test-com>`

 do

     commands

 done
