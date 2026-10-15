

```
% echo "The name $name sounds familiar!"
The name John* sounds familiar!
% echo \$name
$name
% echo '$name'
$name
```

前面的会话表明，如果包含空格的值没有用引号括起来，shell 会将第一个单词赋给该变量，并将剩余部分作为初始化为空的变量。换句话说，命令 `set name = John Doe II` 将 `name` 变量初始化为 `John`，并声明 `Doe` 和 `II` 为初始化为空的字符串变量。当你显示一个初始化为空的变量时，shell 会显示一个空行。此外，在执行 `set name=John*` 命令后，如果 `$name` 在 `echo` 命令中没有用引号括起来，shell 会列出当前工作目录中与 `John*` 匹配的文件名，其中 `*` 被视为 shell 元字符——也就是说，文件以字符串 `John` 开头，后跟 0 个或多个字符。如果你的当前目录中没有任何以字符串 `John` 开头的文件，`set name = John*` 命令会返回错误消息 `set: No match.`，随后执行的 `echo $name` 命令会显示 `name` 变量以前的值，在本例中为 `John Doe`。运行 `echo *` 命令会显示当前目录中所有文件的名称。前面的会话还表明，可以使用单引号来按字面意义处理 `name` 变量的值。事实上，你可以使用单引号来按字面意义处理整个字符串。反斜杠字符可用于转义任意单个字符（包括 `$`）的特殊含义，并按字面意义处理它。在 C shell 中，为了转义 `!` 的特殊含义，如果 `!` 后面紧跟除空格外任意字符，则必须在 `!` 符号前使用反斜杠（\）。

仅由 `$variable` 组成的命令会导致该变量的值作为 shell 命令被执行。如果 `variable` 的值包含有效命令，则会产生预期结果。如果 `variable` 不包含有效命令，shell 会（如预期那样）显示相应的错误消息。以下会话通过示例说明了这一点。本会话中使用的变量是 `command`。

```
% set command = pwd
% $command
/usr/home/sarwar/unix3e/ch14
% set command = hello
% $command
hello: Command not found.
%
```

## 14.4.1 命令替换

当命令用反引号（也称为重音符）括起来时，shell 会执行该命令，并用命令的输出替换该命令（包括反引号）。这个过程称为命令替换。下面是对命令替换的简要描述。

```
'syntax'
'command'

Purpose: Execute command and substitute its output for 'command'
```

下一个会话将说明这一概念。在第一个赋值语句中，名为 `command` 的变量被赋值为 `pwd`。在第二个赋值语句中，`pwd` 命令的输出被赋值给 `command` 变量。

```
% set command = pwd
% echo "The value of command is: $command."
The value of command is: pwd
```

命令替换可以在任何命令中指定。例如，在下面的命令行中，`date` 命令的输出会在 `echo` 命令执行之前替换掉 `'date'`。

```
% echo "The date and time are 'date'."
The date and time are Sun Sep 7 14:12:13 PKT 2014.
```

## 练习 14.3

将你的全名赋给一个 shell 变量 `myname`，并输出它的值。你是如何完成这个任务的？请展示你的操作。

## 练习 14.4

将命令 `echo "Hello, world!"` 的输出赋给 `myname` 变量，然后显示 `myname` 的值。列出你为完成此任务所执行的命令。

## 14.2 导出环境

当创建一个变量时，它不会自动被后续的 shell 所知。`setenv` 命令会将变量的值传递给后续的 shell。因此，当一个 shell 脚本将变量的值传递给后续的 shell 时，当一个 shell 脚本……

