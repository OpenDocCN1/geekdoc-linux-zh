
```
$ echo $PATH
/usr/kerberos/bin:/usr/local/bin:/usr/bin:/bin:/usr/X11R6/bin:/home/bball/bin
```

# 公有领域 Korn Shell

`pksh` shell 最初由 Eric Gisin 创建，与 David Korn 创建的原版 Korn shell 一样，它属于公有领域。在 Fedora 中，`pksh` 被称为 `ksh`。两个符号链接 `/usr/bin/pksh` 和 `/usr/bin/ksh` 指向名为 `/bin/ksh` 的 `pksh` shell。有关 `pksh` 的更多信息，请查看 `/usr/share/doc/pksh` 目录或阅读 `ksh` 手册页。您可以通过浏览 `ftp://ftp.cs.mun.ca/pub/pksh/` 下载最新版本的 `pksh`（源代码形式）。

2000 年 3 月 1 日，AT&T 将官方版本的 korn shell，即 KornShell 93，作为开源软件发布。如果您有兴趣尝试 David Korn 编写的原版 korn shell，请从 `http://www.kornshell.com/` 的 KornShell 网页上下载副本。

## 注意

> 切勿在您的 `$PATH` 中加入 `.`，以便在当前目录中执行文件或命令——这带来了严重的安全风险，尤其是对于 root 操作员而言，如果 `.` 位于您的 `$PATH` 搜索顺序的最前面，风险甚至更大。被破解者放置在 `/tmp` 等目录中的特洛伊脚本可能被用于恶意目的，并且如果当前工作目录是您 `$PATH` 的一部分，它们将立即被执行。

# 存储 Shell 脚本以实现系统级访问

执行 `myenv` 命令后，您应该能够使用命令行中的 `ldir` 命令获取当前目录下文件的列表，并使用 `ll` 命令获取带有属性显示的文件列表。然而，使用 `myenv` 中新命令的最佳方法是将其放入您的 shell 的登录文件或 profile 文件中。对于 Fedora 以及几乎所有 Linux 用户而言，默认 shell 是 `bash`，因此您可以将这些命令放入 `/etc/bashrc` 文件中，以便让系统中的每个人都能使用这些命令。用于 `test` 的系统级别名包含在 `/etc/profile.d` 目录下扩展名为 `.csh` 的文件中。`pksh` shell 也可以使用这些命令别名。

## 注

> 若要登录时使用除 `bash` 以外的 shell，请在命令行中使用 `csh` 命令，或在 X 会话期间使用 `system-config-users` 客户端。系统会要求您输入密码（如果使用 `system-config-users`，则可能需要 root 密码），以及新 shell 的位置和名称（参见表 14.1）。新 shell 将成为您的默认 shell，但前提是 `/etc/shells` 中可接受的系统 shell 列表中包含其名称。有关更改 shell 的详细信息，请参阅第 5 章“Fedora 初始步骤”。

# 通过特定 Shell 解释 Shell 脚本

大多数 shell 脚本在开头使用 shebang 行（`#!`）来控制运行该脚本所用的 shell 类型；这个 bang 行要求使用 `bash` 的 `sh` 咒语：

```bash
#!/bin/sh
```

Shebang 行（"sharp" 和 "bang" 的简称，即 `#` 和 `!` 的两个名称）告诉 Linux 内核，应使用特定的命令（shell，或者在其他脚本的情况下，可能是 `awk` 或 `Perl`）来解释文件的内容。使用 shebang 行是所有 shell 脚本编写中的常见做法。例如，如果您使用 `bash` 编写 shell 脚本，但希望该脚本像由 Bourne shell（`sh`）运行一样执行，那么您的脚本的第一行将包含 `#!/bin/sh`，这是指向 `bash` shell 的链接。以 `sh` 身份运行 `bash` 会导致 `bash` 表现得像 Bourne shell。这就是指向 `bash` 的符号链接 `sh` 存在的原因。

## Shebang 行

Shebang 行是一个魔数（magic number），定义在 `/usr/share/magic` 中——这是 Linux `file` 命令的魔数文本数据库。许多不同的 Linux 命令使用魔数来快速识别文件类型，该数据库格式记录在名为 `magic` 的五部分手册页中（使用 `man 5 magic` 阅读）。例如，Linux `file` 命令可以使用魔数来显示脚本的身份（无论使用什么文件名），作为使用特定 shell 或其他解释器（如 `awk` 或 `Perl`）的 shell 脚本。

使用不同的 shell 时，您还可能会发现脚本中可以使用不同的或新的环境变量。例如，如果您从 `bash` 命令行启动 `csh`，您会发现一些新变量或定义略有不同的变量，例如：

```bash
$ env
...
VENDOR=intel
MACHTYPE=i386
HOSTTYPE=i386-linux
HOST=thinkpad.home.org
```

另一方面，`bash` 可能会提供这些变量或名称相同但定义略有不同的变量，例如：

```bash
$ env
...
HOSTTYPE=i386
HOSTNAME=thinkpad.home.org
```

虽然 shebang 行的行为并未由 POSIX 定义，但其使用的变体在编写 shell 脚本时可能会有所帮助。例如，正如 `wish` 手册页中所述，您可以使用 shell 来帮助执行 shell 脚本内调用的程序，而无需硬编码程序的路径名。`wish` 命令是一个窗口化工具控制语言（tcl）解释器，可用于编写图形客户端。避免使用指向程序的具体路径可以增加 shell 脚本的可移植性，因为并非每个 Unix 或 Linux 系统都在相同位置放置程序。

例如，如果您想使用 `wish` 命令，您的第一反应可能是编写：

```bash
#!/usr/local/bin/wish
```

虽然这在许多其他操作系统上可以正常工作，但在 Linux 下该脚本将失败，因为 `wish` 位于 `/usr/bin` 目录下。但是，如果您这样编写命令行：

```bash
#!/bin/sh
exec wish "$@"
```

您就可以在 Linux 中使用 `wish` 命令（作为二进制文件或 shell 脚本本身）。

## 在 Shell 脚本中使用变量

为 Linux 编写 shell 脚本时，您需要处理三种类型的变量：

- **环境变量**——系统环境的一部分，您可以在 shell 程序中使用它们。可以定义新变量，并且其中一些（如 `PATH`）也可以在 shell 程序内修改。
- **内置变量**——这些变量（例如命令中使用的选项（被 shell 解释为*位置参数*））由 Linux 提供。与环境变量不同，您无法修改它们。
- **用户变量**——您在编写 shell 脚本时定义的变量。您可以在 shell 程序中随意使用和修改它们。

Shell 编程与其他编程语言的一个主要区别在于，在 shell 编程中，变量不是*有类型*的——也就是说，您不必指定变量是数字还是字符串等。

## 给变量赋值

假设您想使用名为 `1count` 的变量来统计 shell 程序中循环的迭代次数。您可以按以下方式声明和初始化该变量：

| 命令 | 环境 |
|---|---|
| `1count=0` | `pdksh` 和 `bash` |
| `set 1count=0` | `tcsh` |

**注**

在 `pdksh` 和 `bash` 下，您必须确保等号（`=`）前后没有空格。

要将字符串存储在变量中，您可以使用以下方法：

| 命令 | 环境 |
|:--- |:--- |
| `myname=Sanjiv` | `pdksh` 和 `bash` |
| `set myname=Sanjiv` | `tcsh` |

如果字符串不包含嵌入式空格，请使用前面的变量形式。如果字符串包含嵌入式空格，您可以按以下方式进行赋值：

| 命令 | 环境 |
|:--- |:--- |
| `myname="Sanjiv Guha"` | `pdksh` 和 `bash` |
| `set myname="Sanjiv Guha"` | `tcsh` |

## 访问变量值

您可以通过在变量名前加上 `$`（美元符号）来访问变量的值。也就是说，如果变量名为 `var`，您可以使用 `$var` 来访问该变量。

如果您想将 `var` 的值赋给变量 `lcount`，可以按以下方式操作：

| 命令 | 环境 |
|:--- |:--- |
| `lcount=$var` | `pdksh` 和 `bash` |
| `set lcount=$var` | `tcsh` |

## 位置参数

您可以从命令行或另一个 shell 脚本向您的 shell 程序传递选项。

这些选项由 Linux 作为*位置参数*提供给 shell 程序，它们具有系统提供的特殊名称。第一个参数存储在名为 `1`（数字 1）的变量中，可以在程序中使用 `$1` 访问。第二个参数存储在名为 `2` 的变量中，可以在程序中使用 `$2` 访问，依此类推。在调用 shell 程序时，可以省略一个或多个较高编号的位置参数。

在开发更高级的 shell 程序时，了解如何使用这些位置参数以及如何访问和使用从命令行获取的变量是必要的。
