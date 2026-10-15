

你还可能通过使用不同的 shell 在脚本中发现不同的或新的环境变量。例如，如果你从 bash 命令行启动 csh，你会发现几个新的变量或定义略有不同的变量，例如

```
$ env
...
VENDOR=intel
MACHTYPE=i386
HOSTTYPE=i386-linux
HOST=thinkpad.home.org
```

另一方面，bash 可能提供这些变量或同名但定义略有不同的变量，例如

```
$ env
...
HOSTTYPE=i386
HOSTNAME=thinkpad.home.org
```

尽管 shebang 行的行为并未由 POSIX 定义，但其用法的变体在你编写 shell 脚本时可能很有帮助。例如，如 wish 手册页所述，你可以使用 shell 来帮助执行 shell 脚本中调用的程序，而无需硬编码程序的路径名。wish 命令是一个窗口化 Tool Control Language（tcl）解释器，可用于编写图形客户端。避免使用程序的具体路径名可提高 shell 脚本的可移植性，因为并非每个 Unix 或 Linux 系统都将程序放在相同的位置。

例如，如果你想使用 wish 命令，你的第一反应可能是写

```
#!/usr/local/bin/wish
```

尽管这在许多其他操作系统上都能工作，但在 Linux 下脚本会失败，因为 `wish` 位于 `/usr/bin` 目录下。然而，如果你这样写命令行，

```sh
#!/bin/sh
exec wish "$@"
```

你可以使用 wish 命令（作为二进制文件或 shell 脚本本身）；你的第一反应可能是要在 Linux 中写 wish。

## 在 Shell 脚本中使用变量

在为 Linux 编写 shell 脚本时，你会使用三种类型的变量：

- **环境变量**——属于系统环境，你可以在 shell 程序中使用它们。可以定义新变量，其中一些变量，如 PATH，也可以在 shell 程序中进行修改。
- **内置变量**——这些是变量，例如在命令上使用的选项（由 shell 解析为 *位置参数*）由 Linux 提供。与环境变量不同，你无法修改它们。
- **用户变量**——由你在编写 shell 脚本时定义。你可以在 shell 程序中随意使用和修改它们。

shell 编程与其他编程语言的一个主要区别是，在 shell 编程中，变量不是 *类型化* 的——也就是说，你不必指定变量是数字还是字符串，等等。

## 为变量赋值

假设你想使用一个名为 `lcount` 的变量来计算 shell 程序中循环的迭代次数。你可以按如下方式声明并初始化此变量：

| Command | Environment |
|---|---|
| `lcount=0` | `pdksh` and `bash` |
| `set lcount=0` | `tcsh` |

> **NOTE**
> 
> 在 pdksh 和 bash 下，你必须确保等号 (`=`) 前后没有空格。

要将字符串存储在变量中，你可以使用以下方法：

| Command | Environment |
|---|---|
| `myname=Sanjiv` | pdksh and bash |
| `set myname=Sanjiv` | tcsh |

如果字符串中没有嵌入空格，请使用前面的变量形式。如果字符串包含嵌入空格，你可以按如下方式进行赋值：

| Command | Environment |
|---|---|
| `myname="Sanjiv Guha"` | pdksh and bash |
| `set myname="Sanjiv Guha"` | tcsh |

## 访问变量值

你可以通过在变量名前加上 $（美元符号）来访问变量的值。也就是说，如果变量名为 var，你可以通过使用 $var 来访问其值。

如果你想将 var 的值赋给变量 lcount，可以按如下方式操作：

| Command | Environment |
|---|---|
| `lcount=$var` | pdksh and bash |
| `set lcount=$var` | tcsh |

## 位置参数

可以从命令行或另一个 shell 脚本向你的 shell 程序传递选项。

这些选项由 Linux 作为位置参数提供给 shell 程序，这些参数具有系统规定的特殊名称。第一个参数存储在名为 1（数字 1）的变量中，可以在程序中使用 $1 访问。第二个参数存储在名为 2 的变量中，可以在程序中使用 $2 访问，以此类推。在调用 shell 程序时，可以省略一个或多个编号较高的位置参数。

了解如何使用这些位置参数以及如何访问和从命令行检索变量对于开发更高级的 shell 程序是必要的。

## 位置参数的一个简单示例

例如，如果 shell 程序 mypgm 预期两个参数——例如名字和姓氏——你可以仅使用一个参数，即名字来调用 shell 程序。但是，你不能仅使用第二个参数，即姓氏来调用它。

