
此示例显示了与你当前终端关联的用户，`u` 选项显示了用户名以及其他信息，如进程启动时间和 CPU 使用率。这个概念性术语源于过去，那时人们完全通过字符终端工作，因为一个终端通常代表一个屏幕上的同一个人。现在，你可以通过打开多个终端在同一个屏幕上拥有许多“终端”。

在这个 shell 会话中，并没有发生太多的事情。第一个进程显示用户登录到登录进程（该由 `root` 用户控制）。下一个进程显示 `jane` 正在使用 `bash` shell 并且刚刚运行了 `ps` 命令。终端设备 `tty0` 用于登录会话。`STAT` 列表示进程状态，其中 `R` 表示运行，`S` 表示睡眠。`USER` 列显示启动进程的用户。`PID` 是进程 ID。`%CPU` 和 `%MEM` 列分别显示处理器和内存百分比。`VSZ`（虚拟内存大小）以 KB 为单位显示大小，`RSS`（驻存内存大小）显示内存中的大小。`START` 显示进程开始的时间，`TIME` 显示累计时间。管道（`|`）将一个命令的输出重定向到下一个命令的输入。要查看并监控 Linux 上的所有进程，输入：

```
$ ps au | less
```

# 退出 shell

完成后退出 shell 时，输入 `exit` 或按 `Ctrl+D`。

我展示了一些命令让你快速熟悉 Linux 系统。数百个其他命令包含在 `/bin` 和 `/usr/bin` 等目录中。还有一些管理命令位于 `/sbin` 或 `/usr/sbin`。这些许多命令将在本章的后续部分描述。

# 理解 shell

在图标和窗口接管屏幕之前，你通过输入命令与计算机交互。在 Linux 源自的 UNIX 系统，用于解释和管理命令的程序被称为 shell。

shell 运行程序、处理文件系统、编译计算机代码和管理计算机的方法。虽然 shell 没有 GUI 那么直观，但大多数 Linux 专家认为 shell 比 GUI 强大得多。因为 shell 已经存在了很久，许多高级功能已内置其中。许多老牌 Linux 管理员和程序员主要将 GUI 作为打开 shell 的方式。

在本章中演示的 shell 被称为 `bash`，其全称为 Bourne Again Shell。这个名字源于 `bash` 兼容第一个 UNIX shell：Bourne shell（由 `sh` 命令表示）。其他流行的 shell 包括 C shell（`csh`，在 BSD 用户中流行）和 Korn shell（`ksh`，在 UNIX V 系统中流行）。Linux 还有 `tcsh`（一种 C shell 的变体）和 `ash`（另一个 Bourne shell 变体）。

注意：虽然你可以通过 `/bin/sh` 调用 Bourne shell，但该命令实际上是以兼容模式运行 `bash` shell。运行 `/bin/sh` 产生的 shell 行为比 `bash` 更像 `sh`，但你将可以使用一些真正的 Bourne shell 无法识别的 `bash` 脚本概念。`sh` 存在主要是为了与专门为该 shell 编写的脚本保持兼容性。

## 第 4 章：使用 Linux 命令

尽管大多数 Linux 用户偏好使用某一种特定的 shell，但只要你学会了如何使用其中一种 shell，就可以通过偶尔参考该 shell 的帮助页（man page）（例如，输入 `man bash`）来快速学习其他任何 shell。`bash` shell 与 `sh` shell 基本兼容。

## 在 Linux 中使用 Shell

当你在 shell 中输入命令时，你还可以包含其他字符，这些字符可以改变或增加命令的工作方式。除了命令本身，你还可以在命令行中输入一些其他项目：

- **选项 (Options)** —— 大多数命令都有一个或多个可以添加的选项，以更改其行为。选项通常由单个字母组成，前面有一个连字符（`-`）。例如，命令 `ls -la` 会列出当前目录的内容。`-l` 请求显示详细的（长）列表信息，而 `-a` 请求列出以点（`.`）开头的文件。当使用单个选项时，前面通常是双连字符（`--`）。例如，为了使用许多命令的帮助信息，你可以在命令行中输入 `--help`。这里是 `ls` 命令的帮助信息示例（输出通过管道传递给命令；`q` 退出）：

```
$ ls --help | less
Usage: ls [OPTION]... [FILE]
List information about the FILEs (the current directory by default).
Sort entries alphabetically or if none of the -ftcSUSX nor --sort.
```

长选项的强制性参数对于短选项也是强制性的

  --all 不隐藏以 . 开头的条目

  -A, --almost-all 不列出隐含的 . 和 ..

- **参数 (Arguments)** —— 许多命令在输入任何选项后还接受参数。参数是命令使用的额外额外信息，例如文件名，可以被命令使用。例如，`cat /etc/passwd` 会在屏幕上显示 `/etc/passwd` 文件的内容。在这种情况下，`/etc/passwd` 就是参数。

- **环境变量 (Environment variables)** —— shell 将可能对用户 shell 会话有用的信息存储在所谓的环境变量中。环境变量的示例包括 `$SHELL`（识别你正在使用的 shell）、`$PS1`（定义你的 shell 提示符）和 `$MAIL`（识别你的信箱位置）。

> 提示：你可以随时检查你的环境变量。输入 `declare` 来列出当前环境变量。或者你可以输入 `echo $VALUE`，其中 `VALUE` 替换为你想要列出的特定环境变量名称。

- **元字符 (Metacharacters)** —— 这些是对 shell 具有特殊意义的字符。元字符可以用于将命令的输出重定向到文件（`>`）、将输出管道到另一个命令（`|`）或在后台运行命令（`&`）等。元字符将在本章稍后的部分进行讨论。

为了方便输入，shell 具有一些功能可以存储你想要重用的命令、回溯之前的命令并编辑命令。你可以创建别名（aliases），允许你通过输入短命令来运行一个较长的命令。shell 将之前输入的命令存储在历史列表中，你可以显示该列表并从中回溯命令。这在该节的剩余部分将进一步讨论。

除非你特意切换到其他 shell，否则 `bash` 是你在 Fedora 或 RHEL 中使用的。`bash` shell 包含了其他 shell 中可用的大部分功能。尽管本章的描述带你介绍了许多 `bash` 特性，但你可以通过输入 `man bash` 更多关于 `bash` shell 的信息。关于学习使用 shell 的其他方法，请参考侧边栏“获取使用 Shell 的帮助”。

## 定位命令

如果你知道包含要运行命令的目录，运行它的的一种方法是输入该命令的完整路径。例如，你通过输入以下内容从 `/bin` 目录运行 `date` 命令：

```
$ /bin/date
```

当然，这可能并不方便，特别是当命令位于名称很长的目录时。更好的方法是将命令存储在已知目录中，然后将这些目录添加到你 shell 的 `PATH` 环境变量中。路径由一系列目录组成，系统会按顺序检查你输入的命令。若要查看你当前的路径，请输入以下内容：

```
$ echo $PATH
/usr/kerberos/bin:/usr/local/bin:/usr/bin:/usr/X11R6:/home/chris/bin
```

结果显示了普通 Linux 用户的默认路径。路径列表中的目录由冒号（:`）分隔。大多数随 Linux 自的用户命令存储在 `/bin`、`/usr/bin` 或 `/usr/local/bin` 目录中。尽管图形界面命令（用于 GUI 使用）包含在 `/usr/bin` 中，但有一些特殊的 X 命令位于 `/usr/bin/X11R6/bin` 目录中。最后显示的目录是用户目录下的 `bin` 目录。（在 Fedora 和 RHEL 系统中，`/usr/kerberos/bin` 位于其他目录之前，如果你正在使用 Kerberos 进行网络认证，将使用许多网络客户端的 Kerberos 版本而不是普通的 Linux 版本。）

> 提示：如果你想添加自己的命令或 shell 脚本，请将其放在家目录下的 `bin` 目录中（例如对于名为 chris 的用户是 `/home/chris/bin`）。该目录会自动添加到你的路径中（尽管你通过输入 `mkdir $HOME/bin` 来创建它）。只要你向 `bin` 添加了具有执行权限的命令（在“理解文件权限”章节中描述），你就可以通过简单在 shell 提示符处输入命令名称来立即开始使用该命令。

# 第 4 章：使用 Linux 命令 155

shell 历史（shell history）是你输入的命令列表。在使用 `history` 命令之前，你可以查看之前的命令。然后，通过各种 shell 功能，你可以从该列表中召回单独的命令行并根据你的意愿对其进行修改。
