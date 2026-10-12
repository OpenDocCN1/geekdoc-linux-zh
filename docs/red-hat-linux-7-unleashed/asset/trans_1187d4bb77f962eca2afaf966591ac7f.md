

## 注意

pdksh shell 最初由 Eric Gisin 创建，是 ksh shell 的公共领域版本，在 /usr/bin 目录下以符号链接的形式存在。在 Red Hat Linux 中，pdksh 被命名为 ksh。两个符号链接 /usr/bin/pdksh 和 /usr/bin/ksh 指向 pdksh shell。关于 pdksh 的更多信息，请参见 /usr/doc/pdksh 目录或 ksh 的手册页。

在特定 shell（例如 pdksh）下执行 myenv 的另一种方法如下：

```
# pdksh myenv
```

这会调用一个新的 pdksh shell，并将文件名 myenv 作为参数传递以执行该文件。

你也可以从命令行按以下方式执行 myenv：

| 命令行 | 环境 |
| :--- | :--- |
| # . myenv | pdksh 和 bash |
| # source myenv | tcsh |

点号（.）是一种告诉 shell 执行文件 myenv 的方式。在这种情况下，你无需确保该文件的执行权限已设置。在 tcsh 下，你必须使用 source 命令而不是点号（.）命令。

执行命令 myenv 后，你应当能够从命令行使用 dir 获取当前目录下的文件列表，并使用 ll 获取显示各种属性的文件列表。然而，在 myenv 中使用新命令的最佳方法是将其放入你的 shell 登录文件或配置文件中。对于 Red Hat Linux 用户，默认 shell 是 bash，因此通过将它们放在 /etc/profile.d 目录中，使这些命令对你系统中的所有人都可用。以 .csh 文件扩展名复制 tcsh 版本，并以 .sh 文件扩展名复制 bash/pdksh 版本。

## 注意

如果你发现在登录 Red Hat Linux 后更喜欢使用 bash 以外的 shell，请使用 chsh 命令。系统会要求你输入密码以及新 shell 的位置和名称（参见表 25.1）。新 shell 将成为你的默认 shell（但前提是其名称在 /etc/shells 中列出的可接受系统 shell 列表中）。

在某些情况下，你可能需要修改 shell 脚本的执行方式。例如，大多数 shell 脚本在开头使用 **hash-bang** 行，如下所示：

```
#!/bin/sh
```

这样做的原因之一是控制运行脚本所使用的 shell 类型（在本例中，是一个 **sh**-风格的 **bash**）。其他 shell（例如 **ksh**）可能会根据脚本调用它们的方式而有不同的响应（这就是为什么需要指向不同 shell 的符号链接的原因）。

你还会发现使用不同的 shell 时，脚本中可用不同的或新的环境变量。例如，如果你从 **bash** 命令行启动 **csh**，你会发现至少有几个新变量，或者定义略有不同的变量，例如

```
# env
 ...
 VENDOR=intel
 MACHINE=i386
 HOSTTYPE=i386-linux
 HOST=thinkpad.home.org
```

另一方面，**bash** 可能提供这些变量，或提供同名但定义略有不同的变量，例如

```
# env
 ...
 HOSTTYPE=i386
 HOSTNAME=thinkpad.home.org
```

尽管 **POSIX** 未定义 bang 行的行为，但其变体形式在编写 shell 脚本时可能很有帮助。如 **wsh** 手册页所述，你可以使用 shell 来帮助执行 shell 脚本内部调用的程序，而无需硬编码程序的路径名。这提高了 shell 脚本的可移植性。

例如，如果你想使用 **wsh** 命令（一种窗口化的 tcl 解释器），你最初可能会想写

```
#!/usr/local/bin/wish
```

尽管这在许多其他操作系统上可以工作，但该脚本在 **Linux** 下将失败。但是，如果你使用

```
#!/bin/sh
 exec wish "$0"
```

那么 **wish** 命令（作为二进制文件或本身是一个 shell 脚本）就可以被使用。使用这种方法还有其他优点。关于更多信息，请参见 **wish** 手册页。

## 变量

Linux shell 编程是一种成熟的编程语言，因此支持各种类型的变量。变量有三种主要类型：环境、内置和用户。

-   **环境变量**是系统环境的一部分，你不需要定义它们。你可以在 shell 程序中使用它们。其中一些（例如 *PATH*）也可以在 shell 程序中修改。
-   **内置变量**由系统提供。与环境变量不同，你无法修改它们。
-   **用户变量**由你在编写 shell 脚本时定义。你可以随意在 shell 程序中使用和修改它们。

shell 编程与其他编程语言的一个主要区别在于，在 shell 编程中，变量不进行类型强制转换。也就是说，你不必指定变量是数字还是字符串等。

### 给变量赋值

假设你想使用一个名为 lcount 的变量来计数 shell 程序中循环内的迭代次数。你可以按以下方式声明并初始化此变量：

| 命令 | 环境 |
| :--- | :--- |
| lcount=0 | pdksh 和 bash |
| set lcount = 0 | tcsh |

> **注意**
> 在 pdksh 和 bash 中，你必须确保等号（=）前后没有空格。

Shell 编程语言不使用类型化的变量，因此同一个变量可以一次存储整数值，另一次存储字符串。然而，不推荐这样做，并且你应该小心避免这样做。

要将字符串存储在变量中，你可以使用以下方法：

| 命令 | 环境 |
| :--- | :--- |
| myname=Sanjiv | pdksh 和 bash |
| set myname = Sanjiv | tcsh |

如果字符串没有嵌入空格，可以使用上述方法。如果字符串包含嵌入的空格，你可以按以下方式进行赋值：

| 命令 | 环境 |
| :--- | :--- |
| myname='Sanjiv Guha' | pdksh 和 bash |
| set myname = 'Sanjiv Guha' | tcsh |

### 访问变量值

你可以通过在变量名前加上 $（美元符号）来访问变量的值。也就是说，如果变量名是 var，你可以使用 $var 来访问该变量。如果你想将 var 的值赋给变量 lcount，你可以按以下方式操作：

| 命令 | 环境 |
| :--- | :--- |
| lcount=$var | pdksh 和 bash |
| set lcount = $var | tcsh |

### 位置参数

你可以编写 shell 脚本，使其在从命令行或另一个 shell 脚本调用时接受多个参数。这些选项由 Linux 作为位置参数提供给 shell 程序，这些参数具有系统提供的特殊名称。第一个参数存储在一个名为 1（数字 1）的变量中，可以在程序内使用 $1 访问。第二个参数存储在一个名为 2 的变量中，可以在程序内使用 $2 访问，依此类推。在调用 shell 程序时，可以省略一个或多个较高编号的位置参数。

```
#!/bin/sh
#Name display program
if [ $# -eq 0 ]
then
echo "Name not provided"
else
echo "Your name is $1"
fi
```

## 第四部分

如果你在 pdksh 和 bash 中按以下方式执行 mypgm1

```
# . mypgm1
```

你会得到以下输出：

Name not provided

但是，如果你按以下方式执行 mypgm1

```
# . mypgm1 Sanjiv
```

你会得到以下输出：

Your name is Sanjiv

shell 程序 mypgm1 还说明了 shell 编程的另一个方面：内置变量。在 mypgm1 中，变量 $# 是一个内置变量，它提供了传递给 shell 程序的位置参数的数量。

## 内置变量

内置变量是 Linux 提供给你的特殊变量，可用于在程序内部做出决策。你无法在 shell 程序内修改这些变量的值。

这些变量中的一些包括

-   **$#** 传递给 shell 程序的位置参数数量
-   **$?** 在 shell 程序内执行的最后一条命令或 shell 程序的完成代码（返回值）
-   **$0** shell 程序的名称
-   **$*** 在调用 shell 程序时传递的所有参数的单个字符串

为了展示这些内置变量的使用情况，下面是一个名为 mypgm2 的示例程序：

```
#!/bin/sh
#my test program
echo "Number of parameters is $#"
echo "Program name is $0"
echo "Parameters as a single string is $*"
```

如果你在 pdksh 和 bash 中从命令行按以下方式执行 mypgm2

```
# . mypgm2 Sanjiv Guha
```

