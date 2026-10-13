
这个命令会在 `$file` 指定的文件名末尾加上一个 x。它不能写成

```
mv $file $filex
```

因为 shell 会尝试用名为 `filex` 的变量的值来替换第二个参数，而不是 `file` 加字母 `x`。

正如第 6 章所提到的，要访问 10 及以上的位置参数，你也必须使用相同的表示格式将数字括在花括号中：`${11}`。

但事实证明，一旦你用花括号将变量名括起来，你还能做更多事情……

```
${parameter:-value}
```

这种结构的意思是：如果 *参数* 不为空，就使用它的值；否则，替换为 *值*。例如，在命令行中

```
echo Using editor ${EDITOR:-/bin/vi}
```

shell 会使用 `EDITOR` 的值（如果它不为空），否则使用 `/bin/vi`。它的效果与编写以下代码相同：

```
if [ -n "$EDITOR" ]
then
        echo Using editor $EDITOR
else
        echo Using editor /bin/vi
fi
```

命令行

```
${EDITOR:-/bin/ed} /tmp/edfile
```

会启动存储在变量 `EDITOR` 中的程序（通常是一个文本编辑器），如果 `EDITOR` 为空，则启动 `/bin/ed`。

需要注意的重要一点是，这不会改变变量的值，所以即使执行了上述语句，如果 `EDITOR` 一开始为空，它仍将保持为空值。

下面是这种结构的一个简单演示：

```sh
$ EDITOR=/bin/ed
$ echo ${EDITOR:-/bin/vi}
/bin/ed
$ EDITOR=                         # Set it null
$ echo ${EDITOR:-/bin/vi}
/bin/vi
$
```

## `${parameter:=value}`

这个版本与上一个类似，但如果 `parameter` 为空，不仅会使用 `value`，而且还会将其赋值给 `parameter`（注意结构中的 `=`）。但是，你不能用这种方式给位置参数赋值，因此这意味着 `parameter` 不能是数字。

这种结构的一个典型用途是测试一个已导出的变量是否已被设置，如果没有，则为其分配一个默认值：

```
${PHONEBOOK:=$HOME/phonebook}
```

它的意思是，如果 `PHONEBOOK` 已经有赋值，则保持不变；否则将其设置为 `$HOME/phonebook`。

请注意，前面的示例不能单独作为命令使用，因为执行替换后，shell 会尝试执行替换结果：

```sh
$ PHONEBOOK=
$ ${PHONEBOOK:=$HOME/phonebook}
sh: /users/steve/phonebook: cannot execute
$
```

要将这种结构作为独立命令使用，可以使用空命令。如果你编写

```
: ${PHONEBOOK:=$HOME/phonebook}
```

shell 仍然会进行替换（它会计算命令行的其余部分），但不会执行任何操作（即空命令）。

```sh
$ PHONEBOOK=
$ : ${PHONEBOOK:=$HOME/phonebook}    # See if it got assigned
$ echo $PHONEBOOK
/users/steve/phonebook
$ : ${PHONEBOOK:=foobar}             # Shouldn’t change
$ echo $PHONEBOOK
/users/steve/phonebook               # It didn’t
$
```

然而，同样常见的是，shell 程序会在条件或 `echo` 语句中首次引用变量时使用 `:=` 记号。效果相同，但不需要空命令。

## `${parameter:?value}`

如果 `parameter` 不为空，shell 会替换为其值；否则，shell 会将 `value` 写入标准错误，然后退出（不用担心——如果是在你的登录 shell 中执行，你不会被注销）。如果省略 `value`，shell 会写入默认错误消息：

```
prog: parameter: parameter null or not set
```

下面是一个例子：

```sh
$ PHONEBOOK=
$ : ${PHONEBOOK:?"No PHONEBOOK file"}
No PHONEBOOK file
$ : ${PHONEBOOK:?}
sh: PHONEBOOK: parameter null or not set
$
```

使用这种结构，你可以轻松检查程序所需的变量是否都已设置且不为空：

```sh
: ${TOOLS:?}  ${EXPTOOLS:?}  ${TOOLBIN:?}
```

## `${parameter:+value}`

如果 *参数* 不为空，则替换为 `value`；否则不替换任何内容。当然，它与 `-` 相反。

```sh
$ traceopt=T
$ echo options: ${traceopt:+"trace mode"}
options: trace mode
$ traceopt=
$ echo options: ${traceopt:+"trace mode"}
options:
$
```

本节中任何结构的 *值* 部分都可以是命令替换，因为它只在需要其值时才执行。这也会变得有点复杂。考虑以下示例：

```
WORKDIR=${DBDIR:-$(pwd)}
```

这里，如果 `DBDIR` 不为空，则将 `DBDIR` 的值赋给 `WORKDIR`；否则执行 `pwd` 命令，并将结果赋给 `WORKDIR`。`pwd` *仅当* `DBDIR` 为空时才执行。

## 模式匹配结构

POSIX shell 提供了四种执行模式匹配的参数替换结构。一些很老的 shell 不支持这个特性，但如果你使用的是现代 Unix、Linux 或 Mac 系统，你不太可能遇到这种情况。

该结构接受两个参数：变量名（或参数编号）和一个模式。shell 会在指定变量的内容中搜索与所提供的模式相匹配的部分。如果匹配，shell 会在命令行中使用该变量的值，并删除*与模式匹配的部分*。如果模式不匹配，则在命令行中使用变量的全部内容。在这两种情况下，变量的内容都保持不变。

这里使用术语 *模式*，是因为 shell 允许你使用与文件名替换和 case 值中相同的模式匹配字符：`*` 匹配零个或多个字符，`?` 匹配任意单个字符，`[...]` 匹配指定集合中的任意单个字符，`[!...]` 匹配不在指定集合中的任意单个字符。

当你编写结构

`${variable%pattern}`

时，shell 会查看 `variable` 的内容，看它是否以指定的 `pattern` 结尾。如果是，则使用 `variable` 的内容，并从右侧删除最短的匹配 `pattern`。

如果你使用结构

`${variable%%pattern}`

shell 会再次查看 `variable` 的内容，看它是否以 `pattern` 结尾。不过，这一次它会从右侧删除最长的匹配模式。只有当结构中使用 `*` 时，这才有意义。否则，`%` 和 `%%` 的行为相同。

`#` 以类似的方式使用，用于强制模式匹配从左侧而不是右侧开始。因此，结构

`${variable#pattern}`

告诉 shell 在命令行中使用 `variable` 的值，并从左侧删除 `pattern`。

最后，shell 结构

`${variable##pattern}`

的工作方式与 `#` 形式类似，不同之处在于从左侧删除最长的 `pattern` 匹配。

请记住，在所有四种情况下，都不会改变变量本身。你只影响命令行中使用的内容。另外，请记住，模式匹配是锚定的。对于 `%` 和 `%%` 结构，变量的值必须以指定模式结尾；对于 `#` 和 `##` 结构，变量必须以该模式开头。

下面是一些简单的例子，演示这些结构的工作原理：
