
让我们逐步分析这个脚本。它以 she-bang、用法说明开始，并在切换到目标对象的 `/boot` 目录之前，将命令行参数数量保存在 `oldir=$(pwd)` 行中。脚本的下部分尝试通过 `System.map` 文件名来修复正确的内核版本。由于可能安装了多个内核，这变得有些复杂。

为了该脚本，我们假设目标对象运行的是安装的最新内核版本。这是为什么你应该在关机之前在目标系统上运行 `-a` 的另一个原因。确定内核版本的行之所以如此复杂，是因为可能存在多个 `System.map` 文件。让我们拆解 `ver=...`

第一个命令是 `ls System.map*`，它导致所有的 `System.map` 文件输出到同一行。下一个命令 `sed "s/System.map/-"` 简单地剥离了前缀，留下一个内核版本列表，每行一个。第三个命令 `tr "\n" "|"` 将字符转换为垂直竖线，从而将所有内容放在同一行。第四个命令包含一个长正则表达式和一个替换命令。

一旦识别出版本，脚本将通过 `cd "$(oldir)"` 这一行返回原始目录。环境变量被包含在大括号中，因为这比使用基础变量（如 `${oldir}`）更安全，后者有时会被误解。当前工作目录和 `make` 命令的完整路径分别保存在 `PWD` 和 `MAKE` 环境变量中。

`cat <<EOF Makefile.${ver}` 行与我们之前使用的 `cat <<EOF` 有些不同。在这里，我们将 `cat` 的输出重定向到文件，而不是终端或其他程序。随后的行“EOF”用于创建一个 `Makefile`。对于不熟悉 `Makefile` 的人，它们通过仅重新构建必要的部分来更高效地构建软件。Makefile 的通用格式是读取 `<target>: [dependencies]`，后面紧跟着一个用制表符缩进的构建目标的命令列表。缩进行必须使用制表符而不是空格，`make` 工具才能正确解析它们。

通常通过简单输入 `make [target]` 来使用 makefile。为了使用这种形式的 `make`，当前目录下必须存在一个名为 `Makefile` 的文件。`make` 的 `-f` 选项允许指定备用的 Makefile。这正是我们在脚本中所做的。脚本的最后几行运行 `make` 来创建一个 dwarf 文件；从系统拷贝 `System.map`；创建一个 Volatility 使用的 zip 文件。从该输出生成的 profile 如图 8.1 所示。

![](img/7abfab28a493757db3f096946a95ec01_302_0.png)

图 8.1

一旦构建了 profile，将其拷贝到 `volatility/plugins/overlays/linux` 目录。对于我的笔记本电脑，完整路径是 `/usr/local/lib/python2.7/dist-packages/volatility-2.4-py2.7.egg/plugins/overlays/linux`。如图 8.2 所示，此目录中的任何有效 zip 文件都会变成有效的 Volatility Linux profile。`vol.py -info` 命令运行 Volatility 并列出所有可用 profile 和其他信息。如果你将结果通过给 `grep`，例如 `vol.py -info | grep Linux`，它将如如图所示提供一个 profile 列表（以及其他几项）。

![](img/7abfab28a493757db3f096946a95ec01_302_0.png)

图 8.2

一旦构建了 profile，...

### 图 8.4

一些可 Volatility Linux 命令。

Volatility 为 Linux 系统提供了许多进程命令。其中最简单的是 `linux_pslist`，它通过遍历任务列表生成任务列表。该命令输出进程名称、进程 ID (PID)、用户 ID (UID) 和组 ID (GID)（以及其他几个你可能不需要的字段）。在我们的 PFE 目标系统上运行此命令的部分输出如图 8.5 所示。高亮行显示了一个在进程 3027 中以 root 权限运行的与形意拳（Xing Yi Quan）rootkit 相关的 shell。

![](img/7abfab28a493757db3f096946a95ec01_305_0.png)

### 图 8.5

Volatility linux_pslist 命令的局部输出。高亮行显示了一个以管理员权限运行的 rootkit shell。

另一个列出进程的命令是 `linux_psaux`。该命令以 `ps -aux` 命名，这是想要获取包含命令行的所有进程列表的人们喜欢的命令。该命令的部分输出如图 8.6 所示。高亮行显示了如何使用 `sudo -s` 创建了一个 root shell（进程 3034）；这导致 bash 以 root 身份运行（进程 3035）；然后安装了 LiME 模块（进程 3073）以转储内存。

![](img/7abfab28a493757db3f096946a95ec01_306_0.png)

### 图 8.6

到目前为止的两个进程命令只显示了孤立的进程。要获取进程之间的关系信息，可以使用 `linux_pstree` 命令。该命令将显示进程及其列在其下方的任何子进程，子进程前会有一个点。嵌套进程的名称前会有多个点。不乎意料的是，几乎所有内容都是 `init` 的子进程，因为 `init` 是在启动时执行的第一个程序，其进程 ID 为 1。在 PFE 目标系统上运行此命令的部分输出如图 8.7 所示。高亮部分清晰地显示了 ID 为 1000 的用户创建了 root shell，随后该 shell 被用于 LiME 转储内存。

![](img/7abfab28a493757db3f096946a95ec01_307_0.png)

图 8.7

在 PFE 目标系统上运行 Volatility linux_pstree 命令的局部结果。高亮输出显示了图 8.6 中高亮的进程之间的关系。

`-p` 选项，允许你提供一组逗号分隔的进程标识数字。要获取此或其他任何其他 Volatility 命令的帮助，请运行 `vol.py <command> -h` 查看简要帮助屏幕。图 8.8 显示了 `linux_psenv` 帮助界面的最后部分，以及与 rootkit 相关的进程上运行 `linux_psenv` 的结果。

虽然 `linux_psaux` 命令很好且提供了很多信息，但还有另一个可以提供更多信息的命令。该命令是 `linux_psenv`。该命令列出了每个显示进程的完整进程环境。由于此命令会生成一个输出列表，你可能希望使用 -

![](img/7abfab28a493757db3f096946a95ec01_308_0.png)

运行 `vol.py linux_psenv -h` 的部分结果以及在与 rootkit 相关进程上运行此命令的结果。

图 8.8 高亮了帮助界面中的 `-p` 选项。查看图形底部，我们看到该进程是由 ID 为 1000 的用户 john 执行的，并且使用了 `sudo`。这并不意味着 John 参与了此次攻击。相反，这告诉我们他的账户被使用了。他的账户可能被使用的原因有很多。他可能遭了某个知道他拥有管理员权限的人的攻击。也很有可能是他有一个弱密码，攻击者能够破解它。

Volatility 为进程提供了一个交叉引用（[cross-reference](https:cross-reference））命令，名为 `linux_psview`。你为什么想要这样的命令呢？某些恶意软件会尝试通过修改内部内核结构来隐藏其进程。通过比较（交叉引用）各种结构，更容易识别出与恶意软件相关的不一致之处。在 PFE 目标系统上运行此命令的部分结果如图 8.9 所示。在这种情况下，没有发现任何异常。

![](img/7abfab28a493757db3f096946a95ec01_309_0.png)

图 8.9
在 PFE 目标系统上运行 `linux_psxview` 的部分结果。

### 进程映射与转储

在上一节中，我们看到了如何使用 Volatility 获取进程列表，包括每个进程的详细信息。在本节中，我们将研究如何使用 Volatility 来确定进程在内存中是如何布局（映射）的。我们将讨论的第一个命令是 `linux_proc_maps`。在 PFE 目标系统上的 rootkit 进程上运行此命令的结果如图 8.10 所示。

![](img/7abfab28a493757db3f096946a95ec01_310_0.png)

获取 rootkit 的进程映射。`linux_proc_maps` 命令显示了进程使用的段。注意每个段都有标志（权限），其中是可写的。该程序还有一个堆（heap）。一些共享库，它们也在内存中。进程栈（stack，向下增长）也位于较高的内存位置。另一种获取此信息的命令是 `linux_proc_maps_rb`。该命令使用平衡树结构，这就是 rb 后缀的原因。C 库已加载这一事实表明该 rootkit 是用 C 或 C++ 编写的。然而，在不分析代码的情况下无法证明这一点，因为即使 rootkit 是汇编等语言编写的也可以加载。Volatility linux_procdump 命令可以将进程转储到文件。我们在书中检测到恶意软件时将讨论如何处理此类文件。`linux_procdump` 命令接受可选的 ID 列表，并要求通过 `-D`（或 `-directory=`）指定输出目录。图 8.11 显示了在我们的 rootkit 上运行 linux procdump 并打印转储内容的部分结果。转储的前几个字节显示这是一个 ELF 格式的可执行文件。

![](img/7abfab28a493757db3f096946a95ec01_311_0.png)

图 8.11

在 PFE 目标系统的 rootkit 上运行 Volatility linux_procdump 命令的结果。转储的前几个字节显示这是一个 ELF 格式的可执行文件。

### 获取 BASH 历史

在本书的早期部分，我们讨论了如何从历史文件中获取用户的 bash 历史。我们也可以从 bash 内存中获取 bash 历史信息。如之前所述，复杂的攻击者可能会删除历史文件和或将历史大小设置为零。历史大小由环境变量 `HISTSIZE` 决定，该变量通常设置在 .bashrc 文件中（默认值为 1000）。即使历史没有保存到磁盘，它仍然存在于内存中。

从 bash 进程内存检索 bash 历史的 Volatility 命令是 `linux_bash`。在 PFE 目标系统上运行此命令的部分输出显示了可疑活动，如图 8.12 和图 8.13 所示。发现了许多未显示的攻击者的其他操作。

### 图 8.12

在 PFE 目标系统上运行 `linux_bash` 的部分结果。高亮部分显示了攻击者在移动虚造的 john 家目录后，尝试修改 `/etc/passwd` 文件。

![](img/7abfab28a493757db3f096946a95ec01_312_0.png)

### 图 8.13

在 PFE 目标系统上运行 `linux_bash` 的部分结果。高亮部分显示了攻击者为新创建的用户移动了家目录并为系统账户设置了密码。

正如我们获取任何进程环境的命令 `linux_psenv` 一样，有一个 Volatility 命令可以返回任何正在运行的 bash shell 的环境。该命令称为 `linux_bash_env`。运行此命令的部分结果如图 8.14 所示。从图中所示每个 bash shell 的 `USER` 变量中，我们可以看到一个 shell 由用户运行，另一个由 root 运行。该用户可能通过 `sudo -s` 启动了第二个 shell。

![](img/7abfab28a493757db3f096946a95ec01_313_0.png)

图 8.14

当命令在 bash shell 中首次运行时（部分输出），bash 必须搜索 PFE 目标系统。

当命令在 bash shell 中首次运行时，bash 必须搜索 `user-> path` 路径（存储在 `PATH` 环境变量中）。因为这是一个耗时的过程，bash 将经常运行的命令存储在哈希表中，以减轻每次都要查找程序的需要。此哈希表可以使用 `hash` 命令进行查看、修改甚至清除。Volatility 提供了 `linux_bash_hash` 命令用于查看内存中每个 bash shell 的此哈希表。在 PFE 目标系统上运行此命令的结果如图 8.15 所示。
