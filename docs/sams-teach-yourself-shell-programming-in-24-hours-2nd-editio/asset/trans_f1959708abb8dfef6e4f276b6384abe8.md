
```
if [ "$VERBOSE" = "true" ] ; then
    MSG="Failed"
    if [ $RET -eq 0 ] ; then
        MSG="Done."
    fi
    echo $MSG
fi
exit 0
```

假设此脚本名为 uu，你可以用以下所有方式对其文件进行 uuencode 编码：

uu ch13.doc
uu -f ch13.doc
uu -f ch13.doc -o ch13.uu

在上述每个命令中，文件 ch13.doc 都会被 uuencode 编码。最后一个命令将结果放入文件 ch13.uu 而不是默认的 ch13.doc.uu；如果文档需要在 DOS 或 Windows 系统上使用，则可能需要这样做。

由于此脚本使用了 getopts，只需指定 -v 选项，之前给出的任何命令都可以在详细模式下运行。

## 摘要

本章中，你研究了如何在 shell 脚本中处理参数和选项。

具体来说，你研究了以下方法：

- 使用 case 语句手动处理参数和选项
- 使用 getopts 处理选项

你通过了两个示例来说明每种方法的实现原理和 rationale。 此外，你还看到了几个与参数和命令执行相关的特殊变量。

正如你在后面的章节中会看到的，使用选项大大提高了 shell 脚本的灵活性和可重用性。

## 问题

1. 向 nytar 脚本添加 tar 文件提取功能。
假设 -x 选项表示用户想要提取 tar 文件，并且用于提取 tar 文件的 TARGS 的正确值是 -xvf。

2. 向 uu 脚本添加提取选项。假设 -x 选项表示应提取文件，并且使用命令 `uudecode $INFILE` 来提取 uuencode 文件。

## 术语

**用法说明** 脚本输出的一条简短消息，用以告知用户脚本的正确调用语法。

![](img/3def70414996f811615f713b2077a154_228_0.png)

## 第14小时

## 函数

Shell 函数提供了一种将名称映射到命令列表的方法。函数类似于其他编程语言中的子程序和过程。你也可以将它们视为迷你 shell 脚本，包含退出代码和参数。脚本与函数的主要区别在于，执行 shell 脚本时会启动一个新的 shell 实例，而函数则在当前 shell 实例中运行。

本章分为以下两个部分：

- 使用函数
- 理解作用域、递归、返回代码和数据共享

第一部分介绍了定义函数的语法并说明了其用法，而第二部分则涵盖了与脚本和函数交互相关的更高级主题。

## 使用函数

函数定义如下：

```
name () { list ; }
```

这里，name 是函数名，list 是命令列表。命令列表 list 被称为函数体。name 后面的括号 { 和 } 是必需的。

函数的工作是将 name 绑定到 list，以便每当指定 name 时就会执行 list。在定义函数时，list 不会被执行：shell 会解析 list 以确保没有语法错误，并将 name 存储在其命令列表中。以下示例说明了基本的函数定义：

```
ls1() { ls -l ; }
```

这里你定义了函数 ls1 并将 list 指定为 ls -l。

在 ksh、bash 和 zsh 中有一种可用的替代函数定义形式：

```
function name { list ; }
```

这里，name 是函数名，list 是要执行的命令列表。

这种函数定义形式在 Bourne shell 中不可用。需要移植到旧系统的脚本不应使用这种形式来定义函数。

## 执行函数

你可以通过指定其名称来执行或调用已定义的函数。例如，你可以按如下方式执行前面示例中定义的函数 ls1：

```
$ ls1
```

这会导致 shell 执行函数体，在本例中为命令 ls -l，并输出结果。输出将类似于以下内容：

```
total 6
drwxr-xr-x  3 root  wheel  512 Oct 29 08:59  ./
drwxr-xr-x 25 root  wheel  512 Oct 29 08:02  ../
drwxr-xr-t  2 root  wheel  512 Nov  3 17:49  vi.recover/
```

函数通常在命令行或脚本内定义。一旦定义，函数在该 shell 或脚本启动的所有子 shell 中都作为有效命令。例如，如果你输入以下命令：

```
$ ls1() { ls -l ; }
```

函数 ls1 成为一个有效的命令名，可以通过指定 ls1 来访问。它在子 shell 中也同样可访问：

```
$ ( ls1 )
total 6
drwxr-xr-x  3 root  wheel  512 Oct 29 08:59  ./
drwxr-xr-x 25 root  wheel  512 Oct 29 08:02  ../
drwxr-xr-t  2 root  wheel  512 Nov  3 17:49  vi.recover/
```

在脚本中定义的函数可在该脚本及其启动的任何子 shell 中访问。例如，考虑以下脚本：

```sh
#!/bin/sh
lsl () { ls -l ; }
cd "$1" && lsl
```

函数 lsl 仅在该脚本中可用。

## 参数

就像你可以用参数执行命令一样，你也可以用参数执行函数。调用函数的一般语法如下：

```
name arg1 ... argN
```

这里，name 是函数名，arg1 ... argN 是函数的参数。指定给函数的参数与指定给 shell 脚本的参数以相同的方式访问；各个参数可作为 $1、$2 等访问，而所有参数的集合可作为 $0 访问。

以下函数说明了单个参数的使用：

```sh
printMsg () { echo "$1: $2" ; }
```

此函数使用 echo 打印一条消息，其中包含冒号 :，它在执行时分隔前两个参数，如下所示：

```
printMsg Error Failed
```

输出为

```
Error: Failed
```

按定义，此函数只能处理两个参数；它会忽略其他所有参数。为了使函数更有用一些，它需要能够处理任意数量的参数。由于指定给函数的所有参数都可在变量 $* 中获得，你可以按如下方式使用它：

```sh
printMsg() {
PREFIX="$1"
shift
echo "$PREFIX: $*"
}
```

这里，你重新定义了函数 printMsg。它将第一个参数保存在 $PREFIX 中，然后使用 echo 以所需格式打印消息。你使用 shift 在调用 echo 之前从 $0 中移除第一个参数。现在你可以用任意数量的参数执行该函数，消息将被正确打印。例如，如果按如下方式执行 printMsg：

```
printMsg Info All Quiet on the Western Front
```

输出为

```
Info: All Quiet on the Western Front
```

## 函数链

函数链是调用另一个函数的过程。以下脚本说明了函数链：

```
#!/bin/sh
orange () {
echo "Now in orange"
banana      # call func2()
}
banana () {
echo "Now in banana"
}
orange
```

此脚本定义了两个函数 orange 和 banana，然后执行 orange。第一个函数 orange 输出一条消息然后调用函数 banana。第二个函数 banana 仅输出一条消息。此脚本的输出为

```
Now in orange
Now in banana
```

## 常见错误

声明和使用函数时常见的两个错误是

- 在函数定义中省略括号 ()。
- 在函数调用中指定括号 ()。

以下示例说明了第一种错误：

```
ls1 { ls -l ; }
```

这里，ls1 后缺少括号。这是一个无效的函数定义，将导致类似以下内容的错误消息：

```
sh: syntax error: ')' unexpected
```

以下命令说明了第二种错误：

```
$ ls1()
```

这里，函数 ls1 连同括号 () 一起被执行。这将不起作用，因为 shell 会将其解释为使用名称 ls1 重新定义函数。通常此类调用会导致类似以下内容的提示：

```
>
```

这是 shell 在期望你提供更多输入时产生的提示。它期望的输入是函数 ls1 的主体。

## 别名与函数

别名是命令的缩写或替代名称，通常具有助记性。别名最初是在 csh 中引入的，后来被 ksh、bash 和 zsh 采用。它们在 Bourne shell 中不受支持。

别名使用 alias 命令定义：

```
alias name='cmd'
```

这里 name 是别名名称，cmd 是在指定 name 时要执行的命令。别名与函数相似，因为它们将命令与名称关联起来。两个主要区别是

- 在别名中，cmd 不能是复合命令或列表。
- 在别名中，没有办法操作参数列表 ($0)。

由于其功能有限，别名在 shell 程序中并不常用。这里讨论它们是为了完整性。

例如，以下命令定义了别名 ls1 并指定当指定命令 ls1 时应执行命令 ls -l：

`alias ls1='ls -l'`

此别名等同于函数：

`ls1 () { ls -l $0 ; }`

别名的常见用途是为命令指定一组默认选项。例如，假设你有以下别名：

`alias ls*='ls -a'`

当给出 ls 命令时，shell 执行 ls -a 而不是不带选项的 plain ls。可以使用如下函数来模拟此行为：

`name () { path $0* ; }`
