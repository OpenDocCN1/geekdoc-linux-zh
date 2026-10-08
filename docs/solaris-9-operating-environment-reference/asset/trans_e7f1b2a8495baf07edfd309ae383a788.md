
## ulimit, unlimited

默认情况下，ul 会退化为 cat(1)。如果终端不支持下划线，则忽略下划线。

## Bugs

nroff 通常会在文本中混杂一系列退格符和下划线来表示下划线。ul 尝试优化向后移动。

## Options

- -i 使用包含适当短划线（-）的单独行来指示下划线；此选项在你想在 CRT 终端上查看 nroff(1) 输出流中的下划线时非常有用。
- -t terminal 覆盖环境变量指定的终端。如果终端不支持下划线，则忽略下划线。如果找不到终端名称，则不进行下划线。

## Exit Status

如果未找到文件，ul 返回退出代码 1。

## Files

/usr/share/lib/terminfo/*

## Attributes

参见 attributes(5) 获取以下属性的描述：

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNdoc |

## See Also

cat(1), man(1), nroff(1), attributes(5)

## # ulimit, unlimit — 设置或获取 Shell 资源限制

# Synopsis

```
/usr/bin/ulimit [-f] [blocks]
sh
ulimit -[HS] [a | cdfnstv]
ulimit -[HS] [c | d | f | n | s | t | v] limit
csh
ulimit -[h] [resource]
```

## umask

ksh

```
ulimit [-HSacdfnstv] [limit]
```

# Description

设置 limit(1)。

## umask — 获取或设置文件模式掩码

# Synopsis

```
/usr/bin/umask [-S] [mask]
```

```
sh, csh
```

```
umask [ooo]
```

```
ksh
```

```
umask [-S] [mask]
```

# Description

当你创建一个文件或目录时，分配给文件或目录的默认文件权限由用户掩码（user mask）控制。你可以在用户初始化文件（如 /etc/profile 或 .cshrc）中使用 umask 命令设置用户掩码。通过输入 umask 并按回车可以显示用户掩码的当前值。

你使用三位八进制值（如 022）设置用户掩码。第一位是用户权限，第二位是组权限，第三位是其他权限。要将 umask 设置为022，请输入

666 的文件权限赋予用户、组和其它读写权限。777 的目录权限赋予用户、组和其它读、写、执行权限。分配的值会从这些值中减去。要确定你想设置的 umask 值，请从 666（文件）或 777（目录）中减去你想要的权限。剩余值即为在 umask 命令中使用的值。例如：假设你想将文件的默认模式改为 644 (rw-r----)。666 和 644 之间的差值是 022，这就是作为 umask 命令参数使用的值。

设置 umask 值的拒绝权限的方式与 chmod 命令授予权限的方式相同。例如，chmod 022 授予组和可能的写权限，而 umask 022 则拒绝组和和其他的权限。

```
/usr/bin/umask
```

umask 命令将当前 Shell 执行环境的文件模式创建掩码设置为由 umask 操作指定的值。此掩码影响随后创建的文件的权限位初始值。如果 umask 在子壳或单独的命令执行环境中调用（如下所示任意一种），

(umask 002)
nohup umask...
find . -exec umask...

它不会影响调用者环境的文件模式创建掩码。由于此原因，你无法通过 /usr/bin/umask 更改进行会话中的 umask。它的用性限于检查调用者的 umask。要更改进行会话的 umask，请使用 Shell 内建命令。

如果你没有指定 umask 顺序，umask 命令将向标准输出调用进程的文件模式创建掩码的值。

## Bourne and C Shells

为 ooo 设置文件模式创建掩码。三位八进制数字代表所有者、组和其他的读/写/执行权限（参见 chmod(1), chmod(2) 和 umask(2)）。每个数字的值都会从系统为创建文件指定的相应数字中减去（参见 create(2)）。例如，umask 022 移除了组和其他的写权限（用 777 创建的文件变为 775；用 666 创建的文件变为 644）。

- - 如果你省略 ooo，则显示掩码的当前值。
- umask 被 Shell 识别并执行。
- 要自动设置创建的文件或目录的权限，你可以将 umask 包含在 Bourne shell 的 .profile（参见 profile(4)）或 C shell 的 .shrc 文件中。这些初始化文件在登录时被调用。

## Korn Shell

为 mask 设置文件模式创建掩码。mask 可以是八进制数，也可以是 chmod(1) 描述的符号值。如果省略 umask，则打印掩码的当前值。

## Options

- -S 将 umask 作为符号参数处理。

默认输出样式未指定，但在同一系统上后续调用 umask 时会被识别。

## Operands

mask 指定新文件模式创建掩码的字符串。该字符串的处理方式与 chmod(1) 手页中的 mode 参数相同。

对于符号值，新文件模式创建掩码是符号字符串指定的模式权限位的逻辑取反。

对于符号模式值，+ 和 - 是相对于当前文件模式创建掩码解释的；+清除掩码中的指定权限；- 设置掩码中的指定权限位。

指定文件权限位以外的模式值的解释未定义。

文件模式创建掩设置为结果数值值。

在同一系统上未带参数的之前的 umask 默认输出也被识别为 umask 参数。使用获取的操作在

## Output

如果你指定 umask，输出为符号格式。默认输出样式未指定，但在同一系统上后续调用 umask 时会被识别。作为 umask 参数恢复之前的文件模式创建掩码。

三个值为字母 r, w, x 的组合；字母的存在表示文件模式创建中对应的位是清除的。

## Examples

以下命令之一设置模式掩码，使随后创建的文件清除 S_IWOTH（其它）位。

```
umask a=rx,ug+w
umask 022
```

按照上述设置模式掩码后，以下命令设置模式掩码，使随后创建的文件清除 S_IWGRP（组）和 S_IWOTH（其它）位。

```
$ umask g-w
$ umask 022
```

以下命令设置模式掩码，使随后创建的文件的所有写位都被清除。

```
$ umask -w
$ umask 022
```

> Note — 你必须在掩码操作 r, w, x 或任何以短划（-）开头的内容加上两个短划（--），防止它们被解释为选项。

## Environment Variables

参见 environ(5) 获取影响 mask 执行的环境变量描述：LC_CTYPE, LC_MESSAGES 和 NLPATH。

## Exit Status

文件模式创建掩码成功更改，或未提供掩码操作。

>0
发生了错误。

## Attributes

参见 attributes(5) 获取以下属性的描述：

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNdoc |

## See Also

chmod(1), csh(1), ksh(1), sh(1), chmod(2), creat(2), umask(2), profile(4), attributes(5), environ(5)

## unalias — 移除命令别名

# Synopsis

```
/usr/bin/unalias alias-name...
/usr/bin/unalias -a
```

```
csh
unalias pattern
ksh
unalias name...
```

# Description

See alias(1).
