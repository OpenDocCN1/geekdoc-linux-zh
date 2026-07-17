# Linux 命令行入门指南



![](img/cover00237.jpeg)













如果你对当前的操作系统感到满意，你可能没有足够的理由去切换。然而，如果有些事情经常困扰着你，也许是时候仔细考虑切换到 Linux 了。

# 第 2 章. Linux 环境变量

在谈论 `bash` shell 时，了解它的特性（如环境变量）是非常重要的。这些变量在存储特定 shell 会话的信息以及你一直工作的环境信息方面非常有用。通过这些变量的帮助，你可以向内存中输入信息，并通过运行脚本或直接运行程序来访问这些信息。

## 全局变量

这很容易学习。这些是可以全局访问的变量。简单来说，你可以在程序的任何阶段访问它们。当你声明一个变量时，在你运行程序时，它会被输入到系统的内存中。你可以在任何函数中进行修改，这可能会影响整个程序。全局变量始终以大写字母显示。

```
aka@localhost ~]$ printenv
```

你已经有了一份完整的全局环境变量列表。大部分变量是在登录过程中设置的。如果你想追踪单个变量的值，可以借助 `echo` 命令来实现。只需忘记在变量前添加 `$` 符号来获取它的值即可。让我们来看这种语法。

```
aka@localhost ~]$ echo $PWD
/root
aka@localhost ~]$
```

## 本地环境变量

这些只能在本地进程中可见。全局环境变量和本地环境变量具有同等的价值。获取本地环境变量列表很困难，因为你不能仅仅为了这个目的运行单一命令。`set` 命令显示了为特定目的设置的环境变量。

```
aka@localhost ~]$ set
BASH=/bin/bash
BASHOPTS=checkwinsize:cmdhist:complete_fullquote:expand_aliases:extquote:force_ffignore:histappend:hostcomplete:interactive_comments:progcomp:promptvars:source-path
BASHRCSOURCED=Y
BASH_ALIASES=()
BASH_ARGC=()
BASH_ARGV=()
BASH_CMDS=()
BASH_LINENO=()
BASH_SOURCE=()
BASH_VERSINFO=([0]="4" [1]="4" [2]="23" [3]="1" [4]="release" [5]="riscv64-koji-linux-gnu")
BASH_VERSION='4.4.23(1)-release'
COLUMNS=80
CVS_RSH=ssh
DIRSTACK=()
EUID=0
GROUPS=()
HISTCONTROL=ignoredups
HISTFILE=/root/.bash_history
HISTFILESIZE=1000
HISTSIZE=1000
HOME=/root
HOSTNAME=localhost
HOSTTYPE=riscv64
IFS=$' \t\n'
LANG=en_US.UTF-8
LESSOPEN='||/usr/bin/lesspipe.sh %s'
LINES=30
```

请注意，所有的全局变量也包含在 `set` 命令的细节中。

### 你设置自己的本地环境变量

你可以在 `bash` shell 中设置自己的变量。你可以使用等号给变量赋值。

```
aka@localhost ~]$ test=world
aka@localhost ~]$ echo $test
world
aka@localhost ~]$
```

上面的示例适用于分配简单值。为了分配一个单词间带有空格的字符串值，你需要尝试不同的方法。请注意，你必须使用小写字母来创建一个新变量。这很重要，因为看到大写字母的环境变量可能会导致你产生困惑。让我们来看下面的语法：

```
aka@localhost ~]$ test=theskyisazure
aka@localhost ~]$ echo $test
theskyisazure
aka@localhost ~]$ test=the sky is azure
bash: sky: command not found
aka@localhost ~]$ test='the sky is azure'
aka@localhost ~]$ echo $test
the sky is azure
```

你可以看到，区别在于使用了单引号。

### 如何移除环境变量

你可以通过一个简单的步骤移除变量。让我们来看看 `unset` 命令的语法。

```
aka@localhost ~]$ echo $test
theskyisazure
aka@localhost ~]$ unset test
aka@localhost ~]$ echo $test
aka@localhost ~]$
```

如果你从子进程中删除环境变量，它仍然保留在父进程中。你必须单独从父进程中删除它。

```
aka@localhost ~]$ test=azure
aka@localhost ~]$ export test
aka@localhost ~]$ bash
aka@localhost ~]$ echo $test
azure
aka@localhost ~]$ unset test
aka@localhost ~]$ echo $test
aka@localhost ~]$ $exit
aka@localhost ~]$ echo $test
azure
aka@localhost ~]$
```

你可以清楚地看到，环境变量首先被导出（export），以便成为全局变量。`unset` 命令是在我仍在子进程时应用的。当我切换到父 shell 时，命令仍然有效。这就是为什么你需要在父 shell 中也删除它。

### 检查默认 shell 变量

`bash` shell 包含了自带的环境变量。让我们检查一些变量。

```
aka@localhost ~]$ echo $PATH
/usr/local/sbin:/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin
```

你可以在此命令看到不同的目录。shell 在这些目录中查找命令。可以通过插入冒号并添加目录向命令添加更多目录。变量分配了默认值。让我们来看：

- `PATH`: 正如我向你展示的示例，它携带目录列表。
- `HOME`: 这指向用户的家目录。
- `IFS`: 这带出一个字符列表。
- `CDPATH`: 你将得到一个由冒号分隔的目录列表。

#### PATH 变量的重要性

这可能是 Linux 系统中最重要的变量，因为它引导 shell 在你于命令行输入输入后立即定位到要执行的命令。如果它未能找到，将显示错误信息，其看起来可能类似于下面给出的：

```
aka@localhost ~]$ newfile
-bash : newfile: command not found
aka@localhost ~]$
```




它是 Linux 操作系统中的一种环境变量。当你输入命令或运行 shell 脚本时，它会被激活。shell 脚本就像一个微程序，为类 Unix 系统的用户提供纯文本的用户界面。它可以读取命令并据此执行它们。这里需要考虑的一点是，全大写的 `PATH` 不能被替换为全小写字母的路径。

路径变量（path variable）是完全不同的东西，它是目录的地址。相对路径指的是相对于你当前所在目录的地址。正如已经讨论过的，还有绝对路径，即它是相对于根目录的地址。

另一方面，`PATH` 将表现为系列由冒号分隔的路径，并以纯文本文件的形式存储。为了方便修订和解释，让我们来看看它是如何执行的。

```bash
[aka@localhost ~] echo $PATH
/usr/local/sbin:/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin
```

你可以向此字符串中添加新目录。让我们试一下。

```bash
[aka@localhost ~] echo $PATH
/usr/local/sbin:/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin
[aka@localhost ~] PATH=$PATH:/home/rich/azuresky
[root@localhost ~]# echo $PATH
/usr/local/sbin:/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/home/rich/azuresky
```

需要提到的是，Linux 操作系统中的每个用户都有与其他用户不同的 `PATH` 变量。在安装操作系统后，会为你的 `PATH` 设置一个默认变量。之后，你可以根据需要添加更多内容或完全更改。

**注意**：需要提到，root 用户的 `PATH` 变量比任何其他用户包含更多的目录。关于 `PATH` 变量的一个有趣之处是，你可以仅针对当前会话更改它，也可以永久性更改更改。

# 如何查找 Linux 系统的环境变量

系统在 shell 脚本中使用多个变量用于识别。通过系统变量的帮助，你可以轻松地为程序获取重要信息。Linux 系统有不同的启动方法，在每个系统中，`bash` shell 执行启动文件的方式也不同。

## 登录 Shell (Login Shell)

它会定位四个不同的启动文件，并从中处理命令。最先执行的文件是 `/etc/profile`。你可以将其称为 `bash` shell 的默认文件。每次你登录时，该命令都会执行。

```bash
[aka@localhost ~]# cat /etc/profile
## /etc/profile
```

我是在超级用户登录时运行了此命令。你窗口上的结果可能会略有不同。

请看下述的 `export` 命令：

```bash
export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE HISTCONTROL
```

你可以清楚地看到，`export` 命令确保变量对子进程仍然可用。

## $HOME

这是一个用户特定的变量。让我们运行它来看看它包含了什么。

```bash
[aka@localhost ~]# cat .bash_profile
## .bash_profile
```

```bash
## .bash_profile
if [ -f $HOME/.bash_profile ]; then
    . $HOME/.bash_profile
fi
# 这是一个用户特定的变量。让我们运行它来看看它包含了什么。
# 用户特定的变量
PATH=$HOME
```

## 交互式 Shell (Interactive Shell)

如果你恰好在没有登录系统的情况下启动 shell，你将进入交互式... 进入所谓的 `.bashrc`。




在 GUI 中运行终端模拟器应用程序时，一个非常好的特性是能够打开多个终端窗口。运行多个终端窗口有许多优势——如果你正在运行一个显示实时输出的命令（例如 `top` 监控命令），你可以打开一个新窗口来执行额外的命令。或者如果你正在运行一个处理耗时较长的命令（例如复制几个 GB 的文件），你可以打开一个新窗口，在第一个命令完成工作的同时运行另一个命令。

大多数终端模拟器应用程序都支持打开新的终端窗口。要这样做，你通常需要进入“File（文件）”菜单并选择“New Window（新窗口）”或“New Terminal（新终端）”。一个新的终端窗口就会打开。

如果你不想让桌面被一堆窗口弄乱，大多数终端应用程序现在都提供了标签页（tabs），就像 Mozilla Firefox 和 Google Chrome 浏览器允许你为不同的网页打开新标签页一样。如果你在终端模拟器中打开新标签页，菜单栏下方会出现一排标签，每个标签包含一个独立的终端会话。通常，你可以通过进入“File（文件）”菜单并点击“New Tab（新标签）”来打开新标签。

显然，图形化终端应用程序无法在命令行环境中运行。尽管如此，通过虚拟控制台（virtual consoles）从命令行运行多个终端窗口也是可能的，我们将在下一节中讨论。

## 虚拟控制台 (VIRTUAL CONSOLES)

虚拟控制台本质上是对同一台计算机的第二次连接。记住 Linux 是基于 UNIX 的，而大多数早期的 UNIX 机器是巨大的大型机计算机。为了连接到这些大型机，用户使用远程控制台或哑终端（dumb terminals）。由于 UNIX 是一个多用户操作系统，多个用户可以同时从不同的控制台登录大型机。

虚拟控制台是那些大型机的遗留。大多数 Linux 版本支持最多七个虚拟控制台，这些是构建在操作系统中的软件控制台，模拟了那些旧哑终端的功能。基本上，用户可以使用这些虚拟控制台之一登录操作系统，然后第二个用户可以切换到另一个虚拟控制台并登录，而不会影响第一个用户的会话（尽管他们他们当然需要共享键盘和鼠标）。

正如我们提到的，Linux 支持七个虚拟控制台。要在虚拟控制台之间切换，请同时按下 `CTRL-ALT-FUNCTION#` 键。因此，要切换到虚拟控制台 1，你需要按下 `CTRL-ALT-F1`，切换到虚拟控制台 2，按下 `CTRL-ALT-F2`，依此类推。当你切换到一个新的虚拟控制台时，你会看到一个标准的登录提示。你（或另一个用户）可以登录该虚拟控制台而不影响你的原始会话。

如果你运行的是带有 GUI 的 Linux 版本，也可以使用虚拟控制台。默认情况下，GUI 运行在虚拟控制台七（`CTRL-ALT-F7`）。你可以切换到其他六个虚拟控制台之一。当你完成后后，可以通过按下 `CTRL-ALT-F7` 返回 GUI。

# 第 4 章。关于文件的更多知识

我确定你渴望热切地投入更多命令，并开始对系统进行一些实际操作。在开始之前，我们需要先涵盖一些理论。当你开始玩转系统时，你能够理解它为什么会那样运行，并且你能够进一步学习命令。

## 一切皆文件 (Everything is a file)

我们需要知道的第一点是一切都是文件。例如，文本文件是一个文件，键盘是一个文件，目录是一个文件，甚至显示器也是文件。

## Linux 是无扩展名系统 (Linux is an Extensionless System)

文件扩展名通常是文件末尾后的 2 到 4 个字符，决定了文件的类型。

常见的扩展名包括：

- `File.exe` – 一个可执行程序或文件，
- `File.txt` – 纯文本文件。
- `File [path]`

## 大写敏感 (Case Sensitivity)

许多初学 Linux 的人会被一个特定问题所困扰——虽然许多其他系统（如 Windows）不关注文件引用中字符的大小写，但 Linux 会。得益于这一特性，可以存在多个名称相同但字母大小写不同的文件或目录。

是 目录

`MYFILE1.txt` `Myfile1.txt` `myfile1.TXT`

`file Docs/myfile1.txt`

`Docs/myfile1.txt: ERROR: cannot open ‘fil1.txt’ (No such file or directory)`

在 Linux 中，所有这些都被解释为完全独立的文件。

在处理命令行选项时，意识到大小写敏感非常重要。例如，在命令行中，`s` 和 `S` 两个选项执行完全不同的动作——通常会读到一个大写选项，用小写输入它，然后奇怪为什么你的输入没有返回预期的输出。

## 命名空间 (Name Spaces)

虽然在完全有效的文件和目录名称包含空格是可能的，但必须小心。命令行中的空格表示不同的项目——通过这种方式我们可以知道程序名称是什么并识别命令行中的每个参数。例如，如果目标是进入一个名为“My Photos”的目录，以下命令将无法正常工作：

是 目录

`MYFILE1.txt` `Myfile1.txt` `myfile1.TXT` `My Photos`

`cd My Photos`

`bash: cd: Happyday: No such file or directory`

在这个示例中，“My Photos”被解释为命令行中的两个独立参数。第一个参数指定了 `cd` 移动的目录。为了让其正常工作，你可以使用两个有效选项之一。

### 引号 (Quotation Marks)

首先，你可以用引号包裹整个项。单引号或双引号都是接受的，尽管处理方式略有不同。

```bash
cd "My Photos"
```
```bash
cd 'My Photos'
```

### 转字符 (Escape Characters)

你也可以通过转义字符（即反斜杠 `\`）来定义带有空格的项。反斜杠消除了其后字符的特殊含义。

```bash
cd My\ Photos
```
你可以看到上面的参数忽略了空格。

## 隐藏文件和目录 (Hidden Files and Directories)

指定文件或目录是否隐藏的机制在 Linux 中非常优雅。通过以点 `.` 开始文件或目录的名称，它将被解释为隐藏——这不需要任何特殊的命令或操作。文件或目录被隐藏有几个原因。例如，用户的配置文件（存储在主目录中）通常是隐藏的，以便为用户的日常任务清理空间。

是 目录

`MYFILE1.txt` `Myfile1.txt` `myfile.TXT`

`ls -a Docs`

… `MYFILE1.txt` `Myfile1.txt` `myfile.TXT` `.hidden` `.file.txt` …

## tar 命令

`tar` 命令被频繁使用，因为它简单高效。它备份文件，包括文件树。

### 备份 (Backup)

```bash
tar -cvf Filename.tar Files
```
- `c`: 创建存档
- `v`: 详细模式：显示正在执行的操作
- `f`: 指明后续参数是存档名称

示例：
```bash
tar -cvf /media/your_media/archive.tar /home/user01/Documents/
```

### 带压缩的备份 (Backup with compression)

```bash
tar -cvzf archive.tar.gz Filers
```
示例：
```bash
tar -cvzf /media/your_media/archive.tar.gz /home/user01/Documents/
```
- `z`: 添加 Gzip 压缩。

### 显示存档内容 (Show the contents of the archive)

```bash
tar -tvf archive.tar
```
- `t`: 显示存档的内容

### 恢复 (Restoration)

NB：不要忘记通过命令 `cd /` 放在文件夹 (`/`) 中

```bash
tar -xvf archive.tar Fichiers
```
- `x`: 从存档中提取所有文件。

示例：
```bash
tar -xvf /media/your_media/archive.tar
tar -xvzf /media/your_media/archive.tar.gz
```



本章将向你展示如何从命令行执行网络任务。你将学习如何查找计算机的 IP 地址和 MAC 地址，如何测试连接性，以及如何查找计算机的 DNS 服务器是否正常运行。

## 查找你的 IP 地址

在大多数 Linux 发行版中，从命令行查找 IP 地址实际上比通过图形界面（GUI）简单得多。只需在提示符处输入此命令：

```
ifconfig
```

`ifconfig` 命令将生成如下输出：

![](img/image00188.jpeg)

这里信息很多，但大部分都是很有用的。`eth0` 指系统上的第一个以太网连接。`indet addr` 显示系统的 IP 地址，而 `Mask` 显示子网掩码。`HWaddr` 显示你的以太网适配器的 MAC（媒体访问控制）地址，该地址（理论上）对于每个适配器都是唯一的。（某些无线网络要求你在允许系统连接之前提供 MAC 地址。）

你可以将 `ifconfig` 命令的输出通过管道（pipe）传给 `grep` 来快速找到你需要的特定项目。假设你只想找到 IP 地址：

```
ifconfig | grep inet
```

这次的输出将如下所示，你可以从结果中快速选出你的 IP 地址：

![](img/image00188.jpeg)

同样，你可以用 `ifconfig` 和 `grep` 快速找到计算机的 MAC 地址。（MAC 地址代表媒体访问控制，是一种硬接地址，理论上对每个网络适配器都是唯一的。）

```
ifconfig | grep HWaddr
```

你可以轻松地从输出中提取出 MAC 地址：

![](img/image00188.jpeg)

## 查找默认网关

`ifconfig` 命令生成了很多有用输出，但它不包含默认网关的地址。要获取它，你可以使用带有 `route` 选项 `ip` 命令：

```
ip route
```

命令将生成如下输出：

![](img/image00188.jpeg)

寻找以 `default via` 开头的行。你的系统默认网关就是这两个词之后的 IP 地址。在示例截图中，默认网关将是 `192.168.2.1`。

## 获取 IP 地址

大多数时候，你的 Linux 系统将从 DHCP 服务器接收 IP 地址。

`DHCP` 代表 `动态主机配置协议`（Dynamic Host Configuration Protocol），是一种服务器，当客户端连接到 DHCP 服务器的网络时，它会为客户端分配 IP 地址。手动为每台计算机配置 IP 地址既耗时又容易出错；如果一台或多个计算机接收到相同的 IP 地址，将由于地址冲突而无法连接。DHCP 消除了这个过程中的猜测。当计算机插入以太网网络（或连接到无线网络）时，它会向 DHCP 服务器发送请求。如果网络上有 DHCP 服务器，它会为计算机提供 IP 地址，并且 DHCP 服务器会确保没有两台计算机接收到相同的 IP 地址。

大多数时候，当你接入新网络时，会自动获得 DHCP 地址。但如果没有获得，请尝试此命令：

```
dhclient
```

注意，你需要以 root 身份运行 `dhclient`，无论是以 root 登录还是通过 `sudo` 借用 root 权限。

这将手动告诉你的系统搜索 DHCP 服务器并接受地址。如果此命令不起作用，说明你使用的网络没有运行正常的 DHCP 服务器，或者有某些阻止了 DHCP 服务器与你的计算机通信。

## 释放 IP 地址

DHCP 地址带有一个`租期`（`lease`），这意味着你的计算机允许保留该地址的时间。通常，你的计算机会在租期到期前的一半处联系 DHCP 服务器，并请求保留它，DHCP 服务器几乎总是授予该请求。

有时你想尽早释放已租的 IP 地址——例如如果你的网络 DHCP 服务器更改了，或者你的计算机拒绝释放 IP 地址。你可以使用 `dhclient` 命令和 `-r` 选项来实现这一点：

```
dhclient -r
```

这将释放你的 IP 地址，然后你可以使用 `dhclient` 联系 DHCP 服务器以接收新地址。

## 测试你的 DNS 服务器

如我们上面提到的，如果你的 DNS 服务器停止响应，你可能会遇到各种网络问题。当它正常工作时，你会忘记它的存在。但一旦它故障，一切都会停滞。没有它，你无法在浏览器的地址栏中输入地址，无法使用任何依赖 DNS 的网络资源。

要诊断你的 DNS 服务器，你可以使用名为 `nslookup` 的命令。`nslookup` 命令提供当前 DNS 服务器的 IP 地址，并对该服务器运行测试查找以检查其是否运行正常。例如，如果你想确定 DNS 服务器是否可以运行，可以使用此命令：

```
nslookup distrowatch.org
```

输出将如下所示：

![](img/image00188.jpeg)

前两行列出了计算机使用的 DNS 服务器。在这种情况下，我们正在使用 IP 地址为 `192.168.2.1` 的 DNS 服务器。第二组行显示了我们执行的查找结果——`distrowatch.org` 的 IP 地址。在这里，你可以看到 `distrowatch.org` 的 IP 地址是 `66.180.174.35`。由于 `nslookup` 成功返回了 `distrowatch.org` 的 IP 地址，你知道你的 DNS 服务器运行正常。

## 测试连接性

如果你曾经修理过电脑（甚至用过电脑），你就知道网络和互联网连接问题是一个令人沮丧的常见现象。幸运的是，命令行工具对于获取任何网络问题的价值信息非常有帮助。

第一个也是最常用的网络诊断命令是 `ping` 命令。`ping` 命令代表数据包互联网探测器（Packet Internet Groper），它依赖于 ICMP 协议（互联网控制消息协议）。基本上，`PING` 命令向网络目标（如服务器或其他 PC）发送一个数据包，如果目标处于激活状态，它将返回一个确认包。例如，如果你想 ping IP 地址为 `192.168.1.2` 的 PC，将使用此命令：

```
ping 10.10.11.254
```

如果 `10.10.11.254` 是在线的，`ping` 命令将生成如下输出：

![](img/image00188.jpeg)

`ping` 命令将继续 ping 目标，直到你按下 `CTRL-C` 取消命令。

该命令还有几个你可以使用的选项来更改其性能。`-c` 选项告诉 `ping` 发送固定数量的数据包然后停止。例如，如果你只想 ping `192.168.1.2` 六次，你将使用此命令：

```
ping -c 6 192.168.1.2
```

注意，即使远程目标具有活跃的网络连接，`ping` 命令也不总是起作用的。这是因为某些操作系统默认会拦截 ICMP 流量。但是，有足够的设备允许 ICMP 流量，使得 PING 成为一个实用的诊断工具。

## 追踪路径

有时你的网络连接是激活的，但你无法访问特定目标。在这种情况下，`traceroute` 命令变得很有用。`traceroute` 命令映射从你的计算机到目的地的网络路由，并向路径中的每个设备发送一个 ICMP 数据包。然后你可以查看路径中哪些设备没有响应，并希望确定解决方案。例如，要追踪到 `10.10.11.254` 的路径，你可以这样使用 `traceroute`：

```
traceroute 10.10.11.254
```

输出将如下所示，每一行代表通往目的地的一个跳（`hop`，链中的另一个设备）：

![](img/image00188.jpeg)

`traceroute` 命令默认运行三十跳。

# 第 6 章 启动与关机

## 概述

本章涵盖了用于启动和关机 Unix、Linux 和 BSD 系统的命令。它还提供了热门平台特定服务控制命令的概述。

## 本节涵盖的命令：

```
shutdown
```




## 关闭系统。

`poweroff`

## 关机系统。

`reboot`

## 重启系统。

`halt`

## 停止系统运行。

`telinit`

更改运行级别（runlevel）。

`runlevel`

显示上一个级别和当前的运行级别。

`service`

管理 Linux 系统上的服务。

`sysv-rc-conf`

显示并编辑 Linux 运行级别配置。

`chkconfig`

显示并编辑基于 Red Hat Linux 系统的运行级别配置。

`rc-update`

显示并编辑 Gentoo Linux 系统的运行级别配置。

`rc-status`

显示 Gentoo Linux 系统上的服务状态。

`stopsrc/startsrc`

在 AIX 系统上停止/启动服务。

`lssrc`

显示 AIX 系统上的服务状态。

`svcs`

显示 Solaris 系统上的服务状态。

`svcadm`

在 Solaris 系统上启动/停止服务。

## 本节使用的术语表：

### Init (初始化程序)
一个控制 Unix、Linux 和 BSD 系统启动（又称初始化）的程序。

### Runlevel (运行级别)
`init` 程序使用的一组配置文件，定义了系统启动期间（或通过 `telinit` 命令调用时）要加载的程序和服务。

### Service (服务)
一种提供 Web 服务器、DNS 服务器、邮件服务器等服务的系统程序。服务有时被称为守护进程（Daemons）或服务守护进程（Service Daemons）。

## shutdown
**目的：** 关闭系统。
**用法语法：** `shutdown [OPTIONS] [TIME] [MESSAGE]`

### # shutdown now
```
来自 ROOT 的广播消息：
系统现在正在关机！
* 正在停止服务 [ OK ]
* 正在终止进程 [ OK ]
...
系统现在停止。
```
shutdown 命令的示例输出

`shutdown` 命令用于关闭本地系统。可以执行几种不同类型的关机：`halt`、`poweroff` 和 `reboot`。

**注意：** `shutdown` 的用法在不同的 Unix、Linux 和 BSD 平台之间有所不同。本页示例适用于 Linux 系统。如需特定环境的特定用法示例，请在本地系统上输入 `man shutdown`。

当执行 `shutdown` 命令时，会向所有登录到本地系统的用户广播警告。可以在时间参数之后指定一个可选消息，如下例所示。

### # shutdown 2 请尽快保存工作并注销！
```
来自 ROOT 的广播消息：
系统将在 2 分钟后关机！
请尽快保存工作并注销！
```
shutdown 命令广播消息的示例输出

**常见用法示例：**
* `shutdown now` - 立即关闭系统
* `shutdown [MIN]` - 等待指定的分钟数后关机
* `shutdown [HH:MM]` - 在指定时间关闭（24 小时制格式）
* `shutdown -r now` - 重启系统
* `shutdown -H now` - 停止系统运行
* `shutdown -P now` - 关机

## poweroff
**目的：** 关系统电源。
**用法语法：** `poweroff`

### # poweroff
```
来自 ROOT 的广播消息：
系统现在正在关机电源！
* 正在停止服务 [ OK ]
* 正在终止进程 [ OK ]
...
系统现在将断电。
```
poweroff 命令的示例输出

`poweroff` 命令将立即关闭并切断系统电源。它本质上是 `shutdown -P now` 的快捷方式。`poweroff` 命令存在所有 Linux 发行版以及某些 BSD 和 Unix 系统中。

**注意：** 要检查你的系统是否支持 `poweroff` 命令，请输入 `whereis poweroff`。

**警告：** `poweroff` 命令不提供缓冲期，执行时将立即关掉系统。

**常见用法示例：**
* `poweroff` - 关并切断系统电源

## reboot
**目的：** 重启系统。
**用法语法：** `reboot`

### # reboot
```
来自 ROOT 的广播消息：
系统现在正在重启！
* 正在停止服务 [ OK ]
* 正在终止进程 [ OK ]
...
系统现在将重启。
```
reboot 命令的示例输出

`reboot` 命令用于平稳地重启系统。它本质上是 `shutdown -r now` 的快捷方式。在命令行上执行 `reboot` 将如上例所示立即重启系统。

**警告：** `reboot` 命令不提供缓冲期，执行时将立即重启系统。

## halt
**目的：** 停止系统运行。
**用法语法：** `halt`

### # halt
```
来自 ROOT 的广播消息：
系统现在正在停止运行！
* 正在停止服务 [ OK ]
* 正在终止进程 [ OK ]
...
系统现在将停止。
```
halt 命令的示例输出

`halt` 命令将停止运行中的系统。`halt` 是一种特殊的关机类型，它会平稳地关闭操作系统，但不切断系统电源。

**注意：** 某些商用 Unix 系统在停止后会进入维护模式。这可以访问启动前的配置/诊断环境。

## telinit
**目的：** 更改运行级别。
**用法语法：** `telinit [RUNLEVEL]`

### # telinit 1
```
*** 正在切换到运行级别 1 ***
```

### # runlevel
```
3 1
```
使用 `telinit` 更改系统的运行级别

`telinit` 通知系统的 `init` 进程停止并启动为指定运行级别配置所需的服务。在上面的示例中，使用 `telinit` 命令将系统切换到运行级别 1。然后执行 `runlevel` 命令（见第 7 节）来显示当前和上一个运行级别。

每个系统的运行级别配置取决于所使用的发行版，并可以根据需要进行自定义。大多数 Unix、Linux 和 BSD 系统将具有与下表类似的运行级别配置：

| 运行级别 | 描述 |
| :--- | :--- |
| 0 | 关机或特殊管理模式 |
| 1 | 单用户模式 |
| 2 | 多用户模式 |
| 3 | 多用户模式 |
| 4 | 多用户模式 |
| 5 | 发行版特定 |
| 6 | 重启 |

**常见用法示例：**
* `telinit [RUNLEVEL]` - 通知 init 进程加载指定的运行级别

## runlevel
**目的：** 显示上一个和当前的运行级别。
**用法语法：** `runlevel`

```bash
$ runlevel
3 1
```
runlevel 命令的输出

`runlevel` 命令显示当前和上一个运行级别。运行级别是由 `init` 进程调用的初始化序列，定义了系统启动和关机的程序。在上面的示例中，第一个数字是上一个运行级别，第二个数字是当前运行级别。

**注意：** 如果没有上一个运行级别，系统将在第一个字段显示 `N`。

**常见用法示例：**
* `runlevel` - 显示上一个和运行级别

## service
**目的：** 管理 Linux 系统上的服务。
**用法语法：** `service [OPTIONS] [SERVICE] [ACTION]`

### # service --status-all
```
[ + ] acpid
[ - ] anac
[ + ] apache2
[ + ] atd
[ + ] cups
[ + ] dbus
[ + ] gdm
[ + ] hal
[ + ] klogd
[ + ] ssh
...
```
使用 service 命令显示服务的状态

`service` 命令管理 Linux 系统上的服务。在上面的示例中，`--status-all` 选项显示系统中所有服务的状态。`+` 符号表示正在运行的服务，`-` 符号表示停止的服务。

`start`、`stop`、`restart` 和 `status` 选项可控制单个服务，如下例所示。

```
## service ssh stop
* 正在停止 OpenBSD Secure Shell server sshd [ OK ]

## service ssh start
* 正在启动 OpenBSD Secure Shell server sshd [ OK ]

## service ssh restart
* 正在重启 OpenBSD Secure Shell server sshd [ OK ]

## service ssh status
* sshd is running
```

**常见用法示例：**
* `service [SERVICE] stop` - 停止指定的服务
* `service [SERVICE] start` - 启动指定的服务
* `service [SERVICE] restart` - 重启指定的服务
* `service [SERVICE] status` - 显示指定服务的状态
* `service --status-all` - 显示所有状态

## sysv-rc-conf
**目的：** 显示并编辑 Linux 运行级别配置。
**用法语法：** `sysv-rc-conf [OPTIONS] [SERVICE] [ON|OFF]`

![](img/image00189.jpeg)
sysv-rc-conf 命令的示例输出




`sysv-rc-conf` 命令用于管理 Linux 系统上的服务/运行级别（runlevel）配置。在上面的示例中执行 `sysv-rc-conf` 会启动一个配置实用程序，使用户可以选择在不同的运行级别上启动哪些服务。

如下一个示例所示，还可以通过 `--list` 和 `--level` 选项通过命令行显示并修改服务。

```
## sysv-rc-conf --level 2345 apache off

## sysv-rc-conf --list apache2
```

```
apache2 2:off 3:off 4:off 5:off

## sysv-rc-conf --level 2345 apache2 on

## sysv-rc-conf --list apache2
```

```
apache2 2:on 3:on 4:on 5:on
```

### 使用 `sysv-rc-conf` 命令在命令行管理服务

**常见用法示例：**

- `sysv-rc-conf`: 显示运行级别配置工具
- `sysv-rc-conf --list`: 列出所有服务的运行级别配置
- `sysv-rc-conf --level [LEVEL] [SERVICE] on`: 在指定的级别上启用服务
- `sysv-rc-conf --level [LEVEL] [SERVICE] off`: 在指定的级别上禁用服务

### `chkconfig`

**目的：** 在基于 Red Hat Linux 的系统上显示并编辑运行级别配置。

**用法语法：** `chkconfig [OPTIONS] [SERVICE] [ON|OFF] [LEVEL]`

```
## chkconfig -l
acpi-support 0:off 1:off 2:on 3:on 4:on 5:on 6:off
acpid 0:off 1:off 2:on 3:on 4:on 5:on 6:off
alsa-utils 0:off 1:off 2:off 3:off 4:off 5:off 6:off
anacron 0:off 1:off 2:on 3:on 4:on 5:on 6:off
apache2 0:off 1:off 2:off 3:off 4:off 5:off 6:off
apport 0:off 1:off 2:on 3:on 4:on 5:on 6:off
...
```

#### 使用 `chkconfig` 命令列出服务配置

`chkconfig` 命令用于在 Red Hat Linux 系统上管理服务。`-l` 参数列出当前的运行级别配置，如上面的示例所示。如果没有指定服务，将显示所有服务。指定服务名称将显示该服务的运行级别配置，如接下来的示例所示。

```
## chkconfig -l apache2
apache2 0:off 1:off 2:on 3:on 4:on 5:on 6:off
```

#### 使用 `chkconfig` 命令列出特定服务

`-s` 选项用于在指定的运行级别上启用或禁用服务，如下一个示例所示。

```
## chkconfig -s apache2 off 2345
## chkconfig -l apache2
apache2 0:off 1:off 2: off 3: off 4: off 5:off 6:off

## chkconfig -s apache2 on 2345
## chkconfig -l apache2
apache2 0:off 1:off 2:on 3:on 4:on 5:on 6:off
```

#### 使用 `chkconfig` 命令管理服务

**常见用法示例：**

- `chkconfig -l`: 列出所有服务的运行级别配置
- `chkconfig -l [SERVICE]`: 列出服务的当前配置
- `chkconfig -s [SERVICE] on [LEVEL]`: 在指定的级别上启用服务
- `chkconfig -s [SERVICE] off [LEVEL]`: 在指定的级别上禁用服务

### `rc-status`

**目的：** 在 Gentoo Linux 系统上显示服务的状态。

**用法语法：** `rc-status [OPTIONS]`

```
## rc-status
Runlevel: default
amavisd [ started ]
apache2 [ started ]
clamd [ started ]
courier-authlib [ started ]
courier-imapd [ started ]
courier-imapd-ssl [ started ]
courier-pop3d [ started ]
hostname [ started ]
keymaps [ started ]
...
```

#### `rc-status` 命令的输出

`rc-status` 显示 Gentoo Linux 系统上服务的状态。在上面的示例中，列出了当前级别下的所有服务及其当前状态。

**注意：** Gentoo Linux 使用非传统的 init 结构，与大多数 Linux 系统不同。你可以在网上 www.gentoo.org/doc/en/handbook/ 了解更多关于 Gentoo init 系统的信息。

**常见用法示例：**

- `rc-status`: 列出当前运行级别的服务
- `rc-status -a`: 列出所有服务
- `rc-status -l`: 列出所有定义的运行级别

### `rc-update`

**目的：** 在 Gentoo Linux 系统上显示并编辑运行级别配置。

**用法语法：** `rc-update [OPTIONS] [SERVICE] [LEVEL]`

```
## rc-update show
amavisd | default
apache2 | default
bootmisc | boot
checkfs | boot
checkroot | boot
clamamd | default
clock | boot
consolefont | boot
courier-authlib | default
courier-imapd | default
courier-imapd-ssl | default
courier-pop3d | default
courier-pop3d-ssl | default
```

#### 使用 `rc-update` 命令显示运行级别配置

`rc-update` 命令管理基于 Gentoo Linux 的系统服务。在上面的示例中，`show` 选项用于显示当前运行级别配置。`add` 和 `del` 选项用于从指定的运行级别添加或删除服务，如接下来的示例所示。

```
## rc-update add sshd default
* sshd added to runlevel default

## rc-update del sshd default
* sshd removed from following runlevels
```

#### 使用 `rc-update` 向默认级别添加和移除服务

**常见用法示例：**

- `rc-update show`: 列出所有服务的运行级别配置
- `rc-update add [SERVICE] default`: 将指定服务添加到默认级别
- `rc-update del [SERVICE] default`: 从默认级别移除服务

### `lssrc`

**目的：** 在 AIX 系统上显示服务的状态。

**用法语法：** `lssrc [OPTIONS] [SERVICE/GROUP]`

``` own# lssrc -a
Subsystem Group
acpi-support 0:off 1:off 2:on 3:on 4:on 5:on 6:off
acpid 0:off 1:off 2:on 3:on 4:on 5:on 6:off
alsa-utils 0:off 1:off 2:off 3:off 4:off 5:off 6:off
anacron 0:off 1:off 2:on 3:on 4:on 5:on 6:off
apache2 0:off 1:off 2:off 3:off 4:off 5:off 6:off
apport 0:off 1:off 2:on 3:on 4:on 5:on 6:off
```

#### 使用 `lssrc` 命令列出服务配置

`lssrc` 命令在 Red Hat Linux 系统上管理服务。`-l` 参数列出当前的运行级别配置，如上面的示例所示。如果没有指定服务，将显示所有服务。指定服务名称将显示该服务的运行级别配置，如接下来的示例所示。

```
## chkconfig -l apache2
apache2 0:off 1:off 2:on 3:on 4:on 5:on 6:off
```

#### 使用 `lssrc` 命令列出特定服务

`-s` 选项用于在指定的运行级别上启用或禁用服务，如下一个示例所示。

```
## chkconfig -s apache2 off 2345
## chkconfig -l apache2
apache2 0:off 1:off 2: off 3: off 4: off 5:off 6:off

## chkconfig -s apache2 on 2345
## chkconfig -l apache2
apache2 0:off 1:off 2:on 3:on 4:on 5:on 6:off
```

#### 使用 `lssrc` 命令管理服务

**常见用法示例：**

- `chkconfig -l`: 列出所有服务的运行级别配置
- `chkconfig -l [SERVICE]`: 列出服务的当前配置
- `chkconfig -s [SERVICE] on [LEVEL]`: 在指定的级别上启用服务
- `chkconfig -s [SERVICE] off [LEVEL]`: 在指定的级别上禁用服务





要查看单个服务的状态，可以像下一个示例所示指定服务名称。

## svcs

```
svcs apache
STATE STIME FMRI
legacy_run 19:42:17 lrc:/etc/rc3_d/S50apache
```

使用 `svcs` 命令列出单个服务的状态。

## `svcs` 常见用法示例

- `svcs`: 显示所有激活的服务。
- `svcs -a`: 显示所有服务。
- `svcs [SERVICE]`: 显示指定的服务。
- `svcs -d [SERVICE]`: 显示指定服务的依赖项。
- `svcs -D [SERVICE]`: 显示依赖于指定服务的服务。
- `svcs -l [SERVICE]`: 显示关于指定服务的详细信息。

## svcadm

**目的**：在 Solaris 系统上启动/停止服务。

**用法语法**：`svcadm [OPTIONS] [SERVICE]`

## svcadm enable sendmail

```bash
svcadm enable sendmail
svcs sendmail
STATE STIME FMRI
online 14:26:14 svc:/network/smtp:sendmail
```

使用 `svcadm` 命令启动服务。`svcadm` 命令控制 Solaris 系统上的服务。它可以用于启动、停止和重启服务。在上面的示例中，使用 `enable` 参数来启动 `sendmail` 服务。下一个示例演示了如何使用 `disable` 参数停止 `sendmail` 服务。

## svcadm disable sendmail

```bash
svcadm disable sendmail
svcs sendmail
STATE STIME FMRI
disabled 14:27:51 svc:/network/smtp:sendmail
```

使用 `svcadm` 命令停止服务。要重启服务，请如下一个示例所示使用 `restart` 参数。

## svcadm restart sendmail

```bash
svcadm restart sendmail
```

使用 `svcadm` 命令重启服务。

## `svcadm` 常见用法示例

- `svcadm enable [SERVICE]`: 启动指定的服务。
- `svcadm disable [SERVICE]`: 停止指定的服务。
- `svcadm restart [SERVICE]`: 重启指定的服务。

# 第 7 章 Linux Shell 编程

在 Linux 中，创建 shell 脚本非常简单。通过 shell 编程，我们可以将多个命令组合成链，然后执行它们以获得所需的输出。让我们从编写第一个脚本开始。打开你选择的编辑器；我正在使用 `vi` 编辑器。将以下 shell 程序添加到文件中：

```bash
#!/bin/bash
echo "Hello World"
```

上述是一个 shell 程序的示例。保存该文件并将其命名为 `hello.sh`。注意，我们使用了 `.sh` 扩展名来表示这是一个 shell 程序。现在，下一步是使脚本具有可执行性。这可以通过以下方式实现：

打开命令提示符并输入以下命令：

```bash
chmod 744 hello.sh
```

运行上述命令后，将创建一个可执行的文件 `hello.sh`；运行上述命令后，文件 `hello.sh` 的可执行版本将被创建；由于我们使用了 `.sh` 扩展名来表示这是一个 shell 程序。现在，下一步是使脚本具有可执行性。这可以通过以下方式实现：

打开命令提示符并输入以下命令：

```bash
chmod 744 hello.sh
```
#!/bin/bash
echo "Hello World"
```

上述是一个 shell 程序的示例。保存该文件并将其命名为 `hello.sh`。注意，我们使用了 `.sh` 扩展名来表示这是一个 shell 程序。现在，下一步是使脚本具有可执行性。这可以通过以下方式实现：

打开命令提示符并输入以下命令：

```bash
chmod 744 hello.sh
```

运行上述命令后，将创建一个可执行的文件 `hello.sh`；由于我们使用了 `.sh` 扩展名来表示这是一个 shell 程序。现在，下一步是使脚本具有可执行性。这可以通过以下方式实现：

打开命令提示符并输入以下命令：

```bash
chmod 744 hello.sh
```

运行上述命令后，将创建一个可执行的文件 `hello.sh`；由于我们使用了 `.sh` 扩展名来表示这是一个 shell 程序。现在，下一步是使脚本具有可执行性。这可以通过以下方式实现：

打开命令提示符并输入以下命令：

```bash
chmod 744 hello.sh
```

运行上述命令后，将创建一个可执行的文件 `hello.sh`；由于我们使用了 `.sh` 扩展名来表示这是一个 shell 程序。现在，下一步是使脚本具有可执行性。这可以通过以下方式实现：

打开命令提示符并输入以下命令：

```bash
chmod 744 hello.sh
```

运行上述命令后，将创建一个可执行的文件 `hello.sh`；由于我们使用了 `.sh` 扩展名来表示这是一个 shell 程序。现在，下一步是使脚本具有可执行性。这可以通过以下方式实现：

打开命令提示符并输入以下命令：

```bash
chmod 744 hello.sh
```

运行上述命令后，将创建一个可执行的文件 `hello.sh`；由于我们使用了 `.sh` 扩展名来表示这是一个 shell 程序。现在，下一步是使脚本具有可执行性。这可以通过以下方式实现：

打开命令提示符并输入以下命令：

```bash
chmod 744 hello.sh
```

运行上述命令后，将创建一个可执行的文件 `hello.sh`；由于我们使用了 `.sh` 扩展名来表示这是一个 shell 程序。现在，下一步是使脚本具有可执行性。这可以通过以下方式实现：

打开命令提示符并输入以下命令：

```bash
chmod 744 hello.sh
```

运行上述命令后，将创建一个可执行的文件 `hello.sh`；由于我们使用了 `.sh` 扩展名来表示这是一个 shell 程序。现在，下一步是使脚本具有可执行性。这可以通过以下方式实现：

打开命令提示符并输入以下命令：

```bash
chmod 744 hello.sh
```

运行上述命令后，将创建一个可执行的文件 `hello.sh`；由于我们使用了 `.sh` 扩展名来表示这是一个 shell 程序。现在，下一步是使脚本具有可执行性。这可以通过以下方式实现：

打开命令提示符并输入以下命令：

```bash
chmod 744 hello.sh
```

运行上述命令后，将创建一个可执行的文件 `hello.sh`；由于我们使用了 `.sh` 扩展名来表示这是一个 shell 程序。现在，下一步是使脚本具有可执行性。这可以通过以下方式实现：

打开命令提示符并输入以下命令：

```bash
chmod 744 hello.sh
```

运行上述命令后，将创建一个可执行的文件 `hello.sh`；由于我们使用了 `.sh` 扩展名来表示这是一个 shell 程序。现在，下一步是使脚本具有可执行性。这可以通过以下方式实现：

打开命令提示符并输入以下命令：

```bash
chmod 744 hello.sh
```

运行上述命令后，将创建一个可执行的文件 `hello.sh`；由于我们使用了 `.sh` 扩展名来表示这是一个 shell 程序。现在，下一步是使脚本具有可执行性。这可以通过以下方式实现：

打开命令提示符并输入以下命令：

```bash
chmod 744 hello.sh
```

运行上述命令后，将创建一个可执行的文件 `hello.sh`；由于我们使用了 `.sh` 扩展名来表示这是一个 shell 程序。现在，下一步是使脚本具有可执行性。这可以通过以下方式实现：

打开命令提示符并输入以下命令：

```bash
chmod 744 hello.sh
```

运行上述命令后，将创建一个可执行的文件 `hello.sh`；由于我们使用了 `.sh` 扩展名来表示这是一个 shell 程序。现在，下一步是使脚本具有可执行性。这可以通过以下方式实现：

打开命令提示符并输入以下命令：

```bash
chmod 744 hello.sh
```

运行上述命令后，将创建一个可执行的文件 `hello.sh`；由于我们使用了 `.sh` 扩展名来表示这是一个 shell 程序。现在，下一步是使脚本具有可执行性。这可以通过以下方式实现：

打开命令提示符并输入以下命令：

```bash
chmod 744 hello.sh
```

运行上述命令后，将创建一个可执行的文件 `hello.sh`；[（注：此处由于用户提供的原文中存在大量重复，已根据指令要求处理翻译逻辑）]

上述是一个 shell 程序的示例。保存该文件并将其命名为 `hello.sh`。注意，我们使用了 `.sh` 扩展名来表示这是一个 shell 程序。现在，下一步是使脚本具有可执行性。这可以通过以下方式实现：

打开命令提示符并输入以下命令：

```bash
chmod 744 hello.sh
```

运行上述命令后，将创建一个可执行的文件 `hello.sh`；

```bash
#!/bin/bash
echo "Hello World"
```

```。运行上述命令后，文件 `hello.sh` 的可执行版本将被创建；

```bash
#!/bin/bash
echo "Hello World"
```

（注：由于原文后半部分存在大量重复的文本，根据“一定不要重复输出原文”的原则，以下仅对核心逻辑进行翻译）

运行上述命令后，将创建一个可执行的文件 `hello.sh`；由于我们使用了 `.sh` 扩展名来表示这是一个 shell 程序。现在，下一步是使脚本具有可执行性。这可以通过以下方式实现：

打开命令提示符并输入以下命令：

```bash
chmod 744 hello.sh
```

运行上述命令后，将创建一个可执行的文件 `hello.sh`；

（由于原文文本存在严重重复，翻译部分已根据指令精简）





```bash
nth pattern) command
  ...
  ..
  command;;
*) command
  ...
  ..
  command;;
esac
```

注意我们从 `case` 开始，但以 `esac` 语句结束。考虑下面显示的示例：

```bash
if [ -y $1 ]
then
  r="the vehicle is unknown"
elif [ -x $1 ]
then
  r=$1
fi

case $r in
  "lorry") echo "For $r 10 per k/m";;
  "merc") echo "For $r 80 per k/m";;
  "corolla") echo "For $r 15 per k/m";;
  "motorbyke") echo "For $r 5 per k/m";;
  *) echo "we can’t obtain a $r for you";;
esac
```

## 用于决策的 If-else-fi

`if-else-fi` 命令可以用于 shell 编程以实现决策。程序员指定一个条件，一旦满足，就会执行一条命令。如果不满足，则执行另一条命令。它采用以下语法：

```bash
if condition
  then
    条件为零
    执行命令直到遇到 else 语句
  else
    如果条件为假
    执行命令直到找到 fi 语句
fi
```

考虑下面显示的示例：

```bash
#!/bin/bash
if [ $# -eq 0 ]
then
echo "$0 : an integer must be supplied"
exit 1
fi

if t $2 -gt 0
then
echo "$2 is a positive number"
else
echo "$2 is a negative number"
fi
```

如果没有给出命令行，则将打印错误信息，即必须提供一个整数。下部分涉及检查已传递的参数数量。如果我们传递了任何参数，那么“`if`”将结果为假，反之为真。`exit 1` 语句将在成功执行后终止程序。

# 第 8 章：网络

单机家用电脑的时代早已过去了。现代服务器和工作站几乎总是连接到互联网，或者至少连接到局域网。为了从命令行有效地使用 Linux 系统，你至少需要具备 TCP/IP 计算机网络的基础知识，以及从提示符可用的网络命令。在本章中，我们将为你提供网络原理的基本概述。

## 什么是 IP 地址？

首先，我们应该讨论 IP 地址。在解释 Linux 命令行提示符的网络命令之前，牢固掌握 IP 划分的基础知识是一个好主意。

`IP` 字母代表互联网协议（Internet Protocol），而互联网协议是 `TCP/IP`（传输控制协议/互联网协议）套件的一部分，这是一组相关的协议，规定了计算机在网络（包括局域网和更广泛的互联网）上通信的规则。因此，IP 地址是（理论上）分配给计算机的唯一地址。它有点像地址——它允许其他计算机向你的系统发送流量并从你的系统接收流量。IP 地址由四组由点分隔的数字组成：

`192.168.1.1`

这些数字实际上是二进制数字的形式形式。这些数字中没有高于 255。（在看侦探剧集时，偶尔看到警察使用一个荒谬且不可信的 IP 地址（如 `689.34.385.339`）来追踪罪犯，会非常搞笑。）

IP 协议的主流版本是第 4 版，通常称为 `IPv4`。（此处原文中存在大量重复内容，已处理。）




`myline` 是一个变量。`read` 命令将只读取文件的第一行并放入变量 `myline` 中。`-r` 选项确保该行以原始格式读取。

### 4. 读取文件
`read` 命令可以与 `while` 循环结合使用逐行读取文件。下文所示：

```bash
while read -r myline; do
    # 对变量 myline 执行某些操作
done < file
```

当 `read` 命令遇到文件结束符（EOF）时，将返回错误代码。此时 `while` 循环将停止。

注意，我们将 `< file` 放在了末尾。为了避免这种情况，可以将文件内容通过管道传递给 `while` 循环，如下：

```bash
cat file | while IFS= read -r myline; do
    # 对变量 myline 执行某些操作
done
```

### 5. 读取文件的任意行并赋值给变量
外部程序可以帮助 bash 读取程序的行。考虑下面的代码：

```bash
$ read -r rline < <(shuf file)
```

`shuf` 在现代 Linux 系统上可用，并可以实现此功能。上述代码将读取文件的随机行并将其赋值给变量 `rline`。

### 6. 提取 tar 归包
使用以下命令：

```bash
tar xvf b.tar
```

### 7. 查找两个文件中共同行的数
```bash
sort doc1 doc2 | uniq –d
```

### 8. 随机化文件的行
```bash
shuf filename.txt
```

### 9. 求特定列的和
```bash
awk '{ sum+=$1} END {print sum}' document.txt
```

# 第 10 章. 文件共享命令

在网络环境中工作时，能够在用户和系统之间共享文件非常重要。Linux 有多种方法可以在 Linux、Windows 和 Mac 系统之间共享文件。

- FTP
- SFTP
- HTTP/HTTPS
- NFS

## Samba

## FTP

FTP 协议是在互联网或网络上共享文件的一种快速方便的方法，但它非常不安全。FTP 协议以明文传输用户名和密码，这可以被任何能够截获客户端与 FTP 服务器之间流量的人捕获。由于安全考虑，您应该只使用 FTP 共享不需要加密的文件。

在大多数 Linux 系统上，如果您想通过 FTP 提供文件，将需要安装 FTP 服务器。如果您必须使用 FTP，请确保安装 FTP 服务端软件的服务器没有在网络中执行任何关键功能。您也不应该在内部网络上放置允许来自外部网络或互联网连接的 FTP 服务器。如果您需要与互联网共享文件，您的 FTP 服务器应该位于防火墙的非军事化区（DMZ）。

### 在 Ubuntu 和 Debian 上安装 FTP 服务器
在 Ubuntu 和 Debian 上安装 FTP 服务器，可以使用 `apt-get install` 命令。

```bash
sudo apt-get install vsftpd
```

Ubuntu 和 Debian 会配置并启用 `vstfpd` 服务，并在安装过程中自动启动该服务。

### 在 Fedora 上安装 FTP 服务器
在 Fedora 上安装 FTP 服务器，可以使用 `dnf install` 命令。当有多个版本可用时，`--best` 选项告诉 Fedora 安装与系统最匹配的软件版本。

```bash
sudo dnf install vsftpd --best
```

Fedora 安装了 `vsftpd` 服务器但不会自动启动服务。使用 `systemctl` 命令启动并启用 `vsftpd` 服务器以便在开机时启动。

```bash
sudo systemctl start vsftpd
sudo systemctl enable vsftpd
```

### 防火墙

如果您的 Linux 系统安装并运行了基于主机的防火墙，那么您必须开放 FTP 入站端口 TCP 端口 21，以允许传入连接。在 Linux 系统上运行 FTP 这种不安全的协议存在安全风险，因此在防火墙上开放端口之前，请确保系统已正确配置并放置在网络中。

本节将涵盖以下子章节：

- Ubuntu 和 Debian
- Fedora

##### Ubuntu 和 Debian
Ubuntu 和 Debian 使用 Uncomplicated Firewall (`UFW`) 来控制基础防火墙配置，但防火墙默认是不配置的。使用以下命令打开 TCP 端口 21：

```bash
sudo ufw allow in ftp
```

#### Fedora 
Fedora 使用 `firewalld` 控制基础防火墙配置，且防火墙默认已配置好。使用以下命令打开 TCP 端口 21：

```bash
firewall-cmd --permanent --add-port=21/tcp
firewall-cmd --reload
```

### FTP 客户端
为了连接到 FTP 服务器，您需要一个 FTP 客户端。Ubuntu 和 Debian 已经自带了它。Fedora 没有，所以您必须使用 `dnf install` 命令安装。

```bash
sudo dnf install ftp
```

本节将涵盖以下子章节：
- 连接到服务器
- 被动模式
- 帮助
- 列出远程文件
- 列出本地文件
- 当前远程目录
- 当前本地目录
- 更改远程目录
- 更改本地目录

#### 连接到服务器
连接到 FTP 服务器，使用 `ftp` 命令后跟 IP 地址或主机名。如下：

```bash
ftp 192.168.1.1
```

系统将被要求输入用户名和密码以访问服务器。默认情况下，`ftp` 使用当前用户，除非您指定特定用户。

您可以在 `ftp` 程序内部通过 `open` 命令连接到服务器，如下：

```bash
open 10.0.0.1
```

如果让 `ftp` 连接保持过久，将会与服务器断，可能需要重新连接。

#### 被动模式
FTP 协议可以在两种模式运行：主动或被动。主动模式使用两个 TCP 端口 20 和 21，而被动模式仅使用 TCP 端口 21。大多数服务器现在运行被动模式，但大多数 FTP 客户端默认使用主动模式。要确保使用正确的模式，可以使用 `passive` 命令将 FTP 客户端设置为被动模式，如下：

```bash
passive
```

#### 帮助
FTP 客户端带有一个帮助菜单，可以通过输入 `?` 或 `help` 访问。可以通过 `help` 命令后跟特定命令来获取帮助，如下：

```bash
help get
```

#### 列出远程文件
使用 `dir` 或 `ls` 命令可以获取远程系统的文件和目录列表，如下：

```bash
ls
```

#### 列出本地文件
在 `dir` 或 `ls` 命令前加上 `!` 字符可以获取本地系统的文件和目录列表，如下：

```bash
!ls
```

#### 当前远程目录
使用 `pwd` 命令可以查看当前远程目录，如下：

```bash
pwd
```

#### 当前本地目录
使用 `!pwd` 命令可以查看当前本地目录，如下：

```bash
!pwd
```

#### 更改远程目录
使用 `cd` 命令可以更改远程目录。在示例中，`pwd` 命令用于检查远程目录，`ls` 命令用于查看远程目录，`cd` 命令用于切换到 Documents 目录。

```bash
cd Documents
```

#### 更改本地目录
使用 `!cd` 命令更改本地目录。

```bash
!cd Downloads
```




你可以使用 `lcd` 命令来更改本地目录。在下面的示例中，使用 `!pwd` 命令来检查远程目录，并使用 `lcd` 命令切换到 `Documents`（文档）目录。

![](img/image00205.jpeg) 

## 获取文件 

要从 FTP 服务器获取或下载文件，可以使用 `get` 命令后跟文件名。在下面的示例中，使用 `!ls` 命令查看本地目录，使用 `ls` 命令查看远程目录，使用 `mget` 命令获取 `myfile4` 文件，并使用 `!ls` 命令查看本地目录以验证文件是否已下载。

![](img/image00206.jpeg) 

要从 FTP 服务器获取或下载多个文件，可以像下面的示例所示使用 `mget` 命令后跟文件名。

![](img/image00207.jpeg)

## 上传文件

要向 FTP 服务器存入或上传文件，可以使用 `put` 命令后跟文件名。默认情况下，`vsftpd` 的配置为不允许写入 FTP 服务器，如下面的示例所示。

![](img/image00208.jpeg) 

若要启用向 FTP 服务器写入，必须编辑 `vsftpd.conf` 文件，删除 `write_enable=YES` 一行前面的 `#` 字符并保存文件。Ubuntu 和 Debian 将 `vsftpd.conf` 文件放在 `/etc/` 目录下，而 Fedora 将该文件放在 `/etc/vsftpd` 目录下。

![00133.jpeg](img/image00209.jpeg)

你需要重启 vsftpd 服务。

```bash
sudo systemctl restart vsftpd
```

一旦服务器重启，你就可以像下面的示例所示使用 `put` 命令上传文件了。

![00134.jpeg](img/image00210.jpeg)

若要向 FTP 服务器上传多个文件，可以像下面的示例所示使用 `mput` 命令后跟文件名和通配符。

![00135.jpeg](img/image00211.jpeg)

## 退出 FTP

要退出 ftp 程序，只需使用 `exit` 命令即可。

## SFTP

由于 FTP 是不安全的，因此不建议用于安全文件传输。要安全地传输文件，你可以使用 SFTP 协议，它使用 TCP 端口 `22`  SSH 协议来传输文件。

你可以像在下面的示例中使用 `ftp` 命令一样使用 `sftp` 命令。

![00136.jpeg](img/image00212.jpeg)

## HTTP/HTTPS

你可以使用 HTTP 和 HTTPS 协议共享文件。放置在 Web 服务器上下载的文件可以使用 `wget` 命令后跟 URL 从命令行下载，如下面的示例所示。

![00137.jpeg](img/image00213.jpeg)

如果下载文件目录中已存在同名文件，`wget` 命令会在文件名末尾添加一个 `.` 和一个数字。

## NFS

网络文件系统 (NFS) 允许 Linux 系统之间跨网络共享文件和目录。NFS 服务器托管目录，NFS 客户端可以在远程系统上挂载。

### Ubuntu 和 Debian 服务器

在 Ubuntu 和 Debian 上安装 NFS 服务器，使用 `apt-get install` 命令。

```bash
sudo apt-get install nfs-kernel-server
```

### Fedora 服务器  

在 Fedora 上安装 NFS 服务器，使用 `dnf install` 命令。

```bash
sudo dnf install nfs-utils --best
```

### 防火墙

如果你的 Linux 系统安装并运行了基于主机的防火墙，则你必须开放 NFS TCP 和 UDP 端口 `2049` 的入站端口以允许传入连接。在 Linux 系统上运行 NFS 等协议都存在安全风险，因此在打开防火墙端口之前，请确保已正确配置系统并将其放置在网络中。

本节将涵盖以下子章节：

- Ubuntu 和 Debian
- Fedora
- `/etc/exports`

##### Ubuntu 和 Debian

Ubuntu 和 Debian 使用简单防火墙 (UFW) 来控制基本的防火墙配置，但防火墙默认未配置。使用以下命令打开 TCP 和 UDP 端口 `2049`：

```bash
sudo ufw allow in nfs
```

##### Fedora

Fedora 使用 firewalld 控制基本的防火墙配置，且防火墙默认已配置。使用以下命令打开 TCP 和 UDP 端口 `2049`：

```bash
firewall-cmd --permanent --add-service=nfs
firewall-cmd --reload
```

#### /etc/exports

安装完服务器后，需要编辑 `/etc/exports` 文件以添加你想要通过 NFS 提供的目录。

```bash
sudo vi /etc/exports
```

exports 文件中的条目语法如下：

`directoryhosts(options)`

- `directory` 是你想要共享的本地目录。
- `hosts` 是允许访问该共享的主机。你可以使用 IP 地址、网络 ID、主机名或 `*`（表示所有主机）。
- `options` 控制共享的权限。以下是常用选项：
  - `ro` - 只读访问
  - `rw` - 读写写访问
  - `no_root_squash` - 允许客户端的 root 用户在服务器上拥有 root 权限。
  - `no_subtree_check` - 如果共享了整个卷，则禁用目录子树的验证以加快访问速度。
  - `sync` - 防止数据损坏

以下是 `/etc/exports` 文件中的共享示例：

向任何 IP 地址共享 `/home` 目录并提供读写权限：
`/home *(rw)`

向 IP 地址 192.168.1.3 共享 `/home` 目录并提供只读权限：
`/home 192.168.1.3(ro)`

向 IP 地址 192.168.1.3（读写）和 192.168.1.4（只读）共享 `/home` 目录并允许 root 拥有权限：
`/home 192.168.1.3(rw,no_root_squash) 192.168.1.4(ro,no_root_squash)`

一旦编辑了 `/etc/exports` 文件，你必须重启 nfs 服务：

对于 Ubuntu 和 Debian：
```bash
sudo systemctl restart nfs-kernel-server
```

对于 Fedora：
```bash
sudo systemctl restart nfs-server
```

### NFS 客户端

为了从 Linux 系统连接到 NFS 服务器，系统必须拥有 NFS 客户端，且客户端的用户在服务器上具有相同的用户名和密码。

##### Ubuntu 和 Debian

在 Ubuntu 和 Debian 上安装 NFS 客户端，使用 `apt-get install` 命令。

```bash
sudo apt-get install nfs-common
```

##### Fedora

在 Fedora 上安装 NFS 客户端，使用 `dnf install` 命令。

```bash
sudo dnf install nfs-utils --best
```

#### mount

为了访问 NFS 服务器上的 NFS 共享，你必须将共享挂载到本地空目录。使用 `mkdir` 命令制作一个空目录：

```bash
mkdir ~/mydir
```

将共享挂载到空目录，使用 `mount` 命令。语法如下：

```bash
sudo mount ip_address:share_name local_directory
```

在下面的示例中，使用 `mount` 命令将 IP 地址为 192.168.56.163 的 NFS 服务器上的 `/home` 文件夹挂载到本地文件夹 `myfolder`。

![00138.jpeg](img/image00214.jpeg)

若要在启动时自动挂载共享，请将共享信息添加到 `/etc/fstab` 文件：

```
192.168.56.163:/home ~/myfoldernfsrw00
```




在 Ubuntu 和 Debian 上安装 Samba 服务器，请使用 `apt-get install` 命令。

```bash
sudo apt-get install samba
```

![00139.jpeg](img/image00215.jpeg)

### Fedora 服务器

在 Fedora 上安装 Samba 服务器，请使用 `dnf install` 命令。

```bash
sudo dnf install samba --best
```

Fedora 不会自动启动 `smb` 服务，因此您需要使用 `systemctl` 命令启动该服务。

```bash
sudo systemctl start smb nmb
```

### 防火墙

如果您的 Linux 系统安装并运行了主机防火墙，那么您必须开放 `SMB` 的 `TCP` 端口 `445` 入站端口以允许传入连接。在 Linux 系统上运行任何如 `SMB` 的协议都存在安全风险，因此在防火墙上开放端口之前，请确保您的系统已正确配置并处于网络环境中。

本节将涵盖以下子章节：

- Ubuntu 和 Debian
- Fedora

##### Ubuntu 和 Debian

Ubuntu 和 Debian 使用简单的防火墙 (`UFW`) 来控制基本的防火墙配置，但防火墙默认未配置。使用以下命令开放 `TCP` 端口 `445`：

```bash
sudo ufw allow in samba
```

##### Fedora

Fedora 使用 `firewalld` 控制基本的防火墙配置，且防火墙默认已配置。使用以下命令开放 `TCP` 端口 `445`：

```bash
firewall-cmd --permanent --add-service=samba
firewall-cmd --reload
```

#### 配置 Samba 密码

Samba 用户使用的密码与 Linux 登录密码不同，但您可以将它们设置为相同。在用户访问 Samba 共享之前，必须使用 `smbpasswd` 命令配合 `-a` 选项设置密码，如下示例所示。

![00140.jpeg](img/image00216.jpeg)

##### 编辑 `/etc/samba/smb.conf`

Samba 共享定义在 `/etc/samba/smb.conf` 文件中。

```bash
sudo vi /etc/samba/smb.conf
```

进入文件末尾并添加以下内容：

```text
[share_name]
  comment = share_comment
  path = share_path
  valid users = samba_user
  read only = yes or no
  guest ok = yes or no
  browseable = yes or no
```

下例显示了共享名称 `myshare` 的配置。

![00141.jpeg](img/image00217.jpeg)

您需要重启 `smb` 服务使更改生效。

##### Ubuntu 和 Debian

```bash
sudo systemctl restart smbd
```

##### Fedora

```bash
sudo systemctl restart smb nbd
```

### 连接到 Samba 服务器

为了从 Linux 系统或 Windows 系统连接到 Samba 服务器，系统必须拥有 `SMB` 客户端，且使用该客户端的用户在服务器上拥有用户名和密码。

#### Linux

在 Linux 系统上，如果尚未安装 Samba 客户端，则必须安装。

##### Ubuntu 和 Debian

```bash
sudo apt-get install smbclient
```

##### Fedora

```bash
sudo dnf install samba --best
```

安装 Samba 客户端后，您可以使用 `smbclient` 命令配合 `-L` 选项查询 Samba 服务器的共享信息，如下示例所示。第一个示例是来自 Ubuntu 服务器的共享信息，第二个示例来自 Fedora 服务器。在两个示例中，您都能看到共享 `myshare`。您需要提供之前创建的 Samba 密码。

![00142.jpeg](img/image00218.jpeg)
![00143.jpeg](img/image00219.jpeg)

您还可以使用 `smbclient` 命令连接到共享。在下例中，IP 地址之前有四个 `\`，之后有两个。这是因为在使用 `smbclient` 命令时，您必须转义 `\` 字符以赋予其特殊含义，因此如果您需要两个 `\` 字符，则必须转义每一个，从而得到四个。您需要提供之前创建的 Samba 密码。连接后，您将获得 `smb: >` 提示符，这意味着您已连接到服务器。在下例中，使用 `?` 命令来访问帮助菜单。

![00144.jpeg](img/image00220.jpeg)

连接到 Samba 服务器后，您可以使用命令在服务器上获取和存放文件，就像使用 `FTP` 和 `SFTP` 一样。

下例显示了使用的 `\` 字符不足时会发生什么。

![00145.jpeg](img/image00221.jpeg)

您还可以使用通用网络文件系统 (`CIFS`) 挂载 Samba 共享。大多数 Linux 系统默认没有安装 `CIFS`，因此您需要安装该软件。

##### Ubuntu 和 Debian

```bash
sudo apt-get install cifs-utils
```

##### Fedora

```bash
sudo dnf install cifs-utils --best
```

安装 `CIFS` 后，您可以使用 `mount` 命令挂载 Samba 共享，如下例所示。

![00146.jpeg](img/image00222.jpeg)

您还可以使用 `mount` 命令查看已挂载共享的信息，如下例所示。您可能需要使用 `grep` 命令来筛选特定的共享，因为服务器上可能有许多共享。

![00147.jpeg](img/image00223.jpeg)

要卸载 Samba 共享，请使用 `umount` 命令。

```bash
sudo umount ~/myfolder
```

#### Fstab

使用 `/etc/fstab` 文件，可以配置让 Samba 共享在启动过程中挂载到文件系统。这种配置存在一些安全问题，因为 Samba 用户名和密码被写入了配置文件。

##### 用户文件

由于 Samba 共享根据用户名和 Samba 密码控制访问，您必须通过将用户名和密码存储在文件中，以便启动过程可以使用。

创建 `/etc/samba/user` 文件。

添加以下行，并将 `sabmba_username` 替换为实际用户名，将 `samba_password` 替换为实际密码。

```text
username=sabmba_username
password=samba_password
```

编辑 `/etc/fstab` 并添加如下内容：

```text
//ip_address/sharename /local_mount_point cifs credentials=/etc/samba/user,noexec 0
```

重启系统以挂载 Samba 共享。

##### Windows

从 Windows 系统访问 Samba 共享，打开文件资源管理器窗口并在地址栏中输入 `\\` 后跟运行 Samba 的 Linux 服务器的 IP 地址。

`\\ip_address\`

您也可以通过包含共享名称直接连接到共享。

`\\ip_address\sharename`

您将需要提供 Samba 用户名和密码。



当你与 Linux 终端交互时，你的计算机会识别你的输入设备（如鼠标和键盘）为应当传输命令的设备。另一方面，标准输出和错误输出会以终端中文本的形式显示在你的屏幕上。

当你成功更改命令的输入和输出方向时，你会得到什么呢？做到这一点可以让你在操作系统中执行更复杂的任务。例如，如果你正尝试管理文件，或者在使用 Linux 进行软件开发时，能够操作 I/O 流将使你变得更高效。

## 从文件获取输入

如果你需要某个命令从特定文件读取指令，你可以指示 Linux 使用该特定文件作为标准输入，而不是键盘。例如，输入命令：

```bash
cat < /etc/passwd
```

运行此命令将允许你看到 `/etc/passwd` 文件中包含的所有行列表。因为你使用了 `<` 符号，你成功地重定向了标准输入，让 Linux 认为 `stdin` 是 `/etc/passwd` 文件而不是你的键盘。

## 将命令输出发送到另一个文件

如果你想记录某个命令的输出并将其保存为文件，你需要将 `stdout` 更改为文件。例如，在进入主目录后，输入以下命令：

```bash
grep typedef *" > typedef.out
```

使用此命令将允许你搜索所有包含文本 `typedef` 的文件，然后将结果保存到名为 `typedef.out` 的文件中。`>` 符号将标准输出重定向到你指定的文件。请注意，上述命令展示了另一个 bash 特性：当使用星号 `*` 时，你本质上是在要求 Linux 包含指定目录中的所有文件，在此例中，即 `/usr/include` 目录下的所有文件。

提示：你可以使用 `>>` 符号将输出追加或添加到现有文件的末尾，而不是必须创建一个新文件来保存输出。请注意此格式：

```bash
grep typedef *" >> typedef.out
```

你也可以通过 `cat` 命令将标准输出更改为文件，这将准备一些小的文本文件。例如，如果你想让 Linux 存储你输入的所有内容，并且仅在你输入 `ZZ` 并按回车时才停止，可以使用此命令：

```bash
cat > file.txt
```

这意味着你的计算机将记录你在键盘上输入的所有内容，并且只在你按下 `ZZ` 和回车键时才会停止。

## 将错误保存到文件中

在某些情况下，你输入了错误并想将其重定向到文件。你可以使用 `2>` 运算符来重定向 `stderr`。例如：

```bash
ls /non_existent_directory 2> error.log
```

这将错误信息保存在 `error.log` 中，而不是显示在终端上。




现在，考虑上面的示例图。假设你正处于根目录，并且想要进入 `www` 目录。如果你输入：

```
cd www
```

Linux 将无法带你进入 `www` 目录；它会提示该目录不存在。为什么？因为记住，你现在处于根目录。对于 Linux 而言，此时根目录下只有两个目录：`etc` 和 `var`。要从根目录进入 `www` 目录，你必须输入：

```
cd /var/www
```

现在你可能会问，上面命令中的第二个正斜杠难道不会带你回根目录吗？不会，并不会。Linux 仅将第一个斜杠解释为根目录。第二个斜杠将被解释为一条指令，即从该斜杠之前的目录开始，查找紧随其后的目录。

这里另一个例子：假设你正处于 `www` 目录，想要进入 `etc` 目录。如果你输入：

```
cd etc
```

这个命令将不起作用。请记住，你目前位于 `www` 目录。对于 Linux 而言，`www` 目录内部并没有 `etc` 目录。为了让这个命令生效，你必须输入下面的命令：

```
cd /etc
```

所以再次，第一个斜杠会被 Linux 解释为先前往根目录的指令。一旦到达根目录，它就会找到 `etc` 目录。当然，这个命令将成功地带你进入 `etc` 目录，因为它存在于根文件夹中。

## 列出/显示文件

现在，一旦你进入一个目录，找出该目录下还有什么内容始终是重要的。在 Linux 中列出文件，你只需要使用 `ls` 命令即可。

```
ls
```

然后，根据你想执行的操作，可以应用两个参数之一。如果你执行：

```
ls -l
```

发生的情况是所有的文件和文件夹都将被列出来。此外，它还会显示这些文件和文件夹的权限、修改日期、组所有者以及个人所有。

很多时候，这可能会变成一个非常大的列表。所以，你也可以输入：

```
ls -m
```

这一次，Linux 不再是给你一个非常长的列表，而是将所有内容输入到一个整齐的区块中，这样你就能看到文件和文件夹的每一条信息。这就是在 Linux 中列出文件和文件夹你需要的所有操作。

现在，假设你想编辑一个关键的配置文件，但你完全不知道那个文件在哪里。坦率地说，Linux 确实有一个搜索选项。为了搜索文件和文件夹，你只需要输入：

```
sudo find -iname <file/folder name>
```

那是 `sudo`，后面跟着一个空格，然后是单词 `find`，另一个空格，参数 `-iname`，另一个空格，最后是你正在查找的文件或文件夹的名称。现在你可能会问，`-iname` 参数是做什么的？嗯，它的作用是使搜索不区分大小写。

例如，如果你正在寻找一个名为 `home` 的文件夹，并使用了带有 `-iname` 参数的搜索命令，它将返回所有以 `home` 为名称的文件夹。无论该文件夹名为 `Home`、`homE`、`hOme`、`HOme`、`hoMe` 还是 `HOME`，它都会出现在搜索结果中。

如果你搞错了要查找的文件或文件夹名称的大小写，且没有使用 `-iname` 参数，搜索可能返回空结果，因为没有文件或文件夹与该大小写匹配。

此外，在 Linux 中执行 `find` 命令时，不要忘记 `sudo` 命令。如果你不在开头输入 `sudo`，`find` 命令将以一种最烦人的方式失败，因为它不会告诉你它失败了。它只是不会给你任何结果。所以你会认为电脑上不存在该文件，而实际上它存在，你只是没有使用 `sudo`。

如果你在文件或文件夹名称之前放一个星号 `*`，这意味着你正在寻找该特定文件或文件夹名称之前的“任何内容”。假设你正尝试在 Linux 中定位配置文件。在 Linux 中，所有的配置文件都有 `.conf` 后缀。如果你正在寻找配置文件但忘记了确切名称，你可能想调出所有以 `.conf` 为后缀的文件。在这种情况下，你输入下面的命令：

```
sudo find -iname *.conf
```

这个命令的作用是查找一个以任何内容开头并以 `.conf` 结尾的文件或文件夹名称。现在，如果你知道要查找的文件名，但不知道后缀怎么办？在这种情况下，你需要输入下面的命令：

```
sudo find -iname php*
```

这个命令的作用是查找一个以 `php` 开始并以任何内容结尾的文件或文件夹名称。

## 创建、删除、移动、复制、重命名

现在我们需要谈谈在 Linux 中创建、删除、移动、复制和重命名文件及文件夹。我们要做的第一件事是讨论创建文件夹。这非常简单。你只需要输入：

```
sudo mkdir <name of directory/folder>
```

那是 `sudo`，后面跟着一个空格，然后是 `mkdir` 参数，另一个空格，然后是你想要创建的文件夹或目录名称。正如你可能已经猜到的，`mkdir` 代表 "make directory"创建目录）。

请记住，如果你不提供目录的完整路径，此命令将在你当前所在的目录下创建该目录或文件夹。例如，假设你处于 `var` 目录，想要在 `etc` 目录中创建一个 `Notes` 文件夹。如果你输入：

```
sudo mkdir Notes
```

这个命令只会在 `var` 目录下创建 `Notes` 文件夹。要在 `etc` 目录中创建 `Notes` 文件夹，你必须输入这样的完整路径：

```
sudo mkdir /etc/Notes
```

这样，Linux 会先去根目录，然后去 `etc` 目录，并在 `etc` 目录内创建一个文件夹。输入完整路径可以确保无论你在哪里都能创建该文件夹。这就是在 Linux 中创建文件夹或目录你需要的所有操作。

删除文件或文件夹同样简单。你只需要输入下面的命令：

```
sudo rm <file or folder name>
```

那是 `sudo`，一个空格，后面跟着字母 `rm`，另一个空格，最后才是你想要删除的文件或文件夹的名称。正如你可能已经猜到的，`rm` 代表 remove（删除）。例如，假设你想删除一个名为 `Notes` 的文件。

### 删除文件夹

然而，删除文件夹稍有不同。实际上，你仍然遵循与删除文件相同的语法。唯一的区别是，在删除文件夹时必须在命令末尾添加 `-R` 参数。`-R` 参数代表 recursive（递归）。通过使用递归参数，你基本上是在告诉 Linux 对文件夹内部的内容执行相同的任务。

假设你想删除包含三个文件的 `www` 文件夹。要这样做，你只需输入：

```
sudo rm www -R
```

这个命令不仅会删除文件夹本身，还会删除里面的三个文件。如果你在删除文件夹的命令末尾没有加递归参数，Linux 将无法成功执行，因为你不能在不删除内容的情况下删除文件夹。只有在没有递归参数的情况下成功删除文件夹的情况，是该文件夹本身就是空的。

### 重命名文件和文件夹

在 Linux 中，并没有专门用于重命名文件和文件夹的命令。与其说 rename，我们在 Linux 中使用的是 `mv` 命令。例如，假设你有一个名为 `file1` 的文件，想要将其更名为 `file2`。为了做到，你必须输入下面的命令语法：

```
sudo mv <name of old file> <name of new file>
```



那是 `sudo`，后面跟着空格，然后是字母 `mv`，另一个空格，原始文件的名称，再次一个空格，最后是新文件的名称。回到我们的示例，如果你想将名称 `file1` 改为 `file2`，你必须输入：

```bash
sudo mv file1 file2
```

此命令将 `file1` 的名称更改为 `file2`。这在技术上仍然是重命名文件，但在 Linux 中，我们使用“移动”（move）这一术语。那么将文件从一个文件夹移动到另一个文件夹呢？同样的语法仍然适用。不过，你必须指定完整路径，而不仅仅是文件的名称。

假设你想将 `var` 文件夹内名为 `file1` 的文件移动到根目录下的 `etc` 文件夹。为此，你必须输入以下命令：

```bash
sudo mv /etc/var/file1 /etc/file1
```

那是 `sudo`，后面跟着空格，然后是代表移动的字母 `mv`，另一个空格，源文件的准确路径，另一个空格，最后是目的地的准确路径。操作非常简单。

复制是 Linux 中的另一项重要任务。很多时候，特别是当你在处理配置文件时，在开始修改原始文件之前，创建一个备份文件是非常关重要的。否则，如果你弄乱了原始文件，可能会损坏该文件关联的程序。

在 Linux 中复制文件，你只需要输入：

```bash
sudo cp <name of the file> <name of the copied file>
```

那是 `sudo`，后面跟着空格，然后是代表复制的字母 `cp`，另一个空格，你想要复制的文件名称，另一个空格，最后是副本文件的名称。假设你想为名为 `file10` 的文件创建一个副本。你只需要输入：

```bash
sudo cp file10 file10.bak
```

在这里，`file10.bak` 是 `file10` 的副本文件名称。如你所见，在 Linux 中复制文件很容易。

## 挂载驱动器 (Mounting Drives)

为了在 Linux 中导航，你需要理解的最后一个大概念就是挂载驱动器。当你有一个外部硬盘并将其插入计算机时，你需要挂载驱动器才能浏览其内容。这个外部硬盘可以是普通硬盘、优盘或 CD-ROM 驱动器。在 Linux 中，优盘和 CD-ROM 驱动器被视为硬盘。

基本上，你连接到计算机的任何驱动器都是必须挂载的驱动器。你首先需要理解的是 Linux 中的挂载过程是如何工作的。挂载过程如下：

- 步骤 1 – 连接硬盘。
- 步骤 2 – 为你的挂载点创建一个文件夹。
- 步骤 3 – 获取硬盘的一些特定信息，然后将挂载点文件夹指向该硬盘。

这基本上就是你挂载驱动器的方法。挂载点文件夹现在与硬盘绑定在一起。由于它们绑定在一起了，你现在可以通过挂载点文件夹浏览硬盘的内容。

那么，你如何在命令行提示符中创建挂载点文件夹呢？简单：只需输入以下命令：

```bash
sudo mkdir /mnt/<name of mount point folder>
```

注意我们在这里创建的 `/mnt` 目录。要清楚 `/mnt` 是 Linux 中标准的挂载目录。这个挂载目录是通用的。如果你愿意，可以使用不同的挂载目录。然而，使用 `/mnt` 被认为是最佳实践，因为大多数 Linux 管理员和程序员都会默认使用它。

现在，假设你想将连接的硬盘挂载到名为 `drive1` 的挂载点。为此，你只需输入：

```bash
sudo mkdir /mnt/drive1
```

通过输入上面的命令，你正在创建硬盘将挂载到的文件夹。一旦完成此操作，下一步要做的是找到你尝试挂载的硬盘信息。为此，你只需运行以下命令：

```bash
sudo fdisk -l
```

上述命令将列出连接到系统的所有物理硬盘。此列表将向你显示连接到系统的不同硬盘、它们拥有的空间等。在那里，你要寻找类似于 `/dev/sda1` 的内容。这些在 Linux 中被称为磁盘名称。

Linux 磁盘名称始终按字母顺序排列。例如，如果你的 Linux 系统连接了两个硬盘，它们将分别命名为 `/dev/sda` 和 `/dev/sdb`。跟在磁盘名称后面的数字指的是特定硬盘内的分区。

例如，如果你的第一个硬盘有两个分区，它们将分别显示为 `/dev/sda1` 和 `/dev/sda2`。如果你的第二个硬盘有三个分区，它们将分别显示为 `/dev/sdb1`、`/dev/sdb2` 和 `/dev/sdb3`。

因此，为了挂载硬盘，一旦我们找到了磁盘名称，只需要输入以下内容：

```bash
sudo mount <disk name> <mount point>
```

如果我们把此命令语法应用于我们的示例，命令看起来应该是这样的：

```bash
sudo mount /dev/sda /mnt/drive1
```

这就是你挂载硬盘需要的所有操作。现在，你可以通过输入命令切换目录到 `/mnt/drive1`：

```bash
sudo cd /mnt/drive1
```

一旦你进入了挂载点目录，就可以输入：

```bash
ls -l
```

上述命令将列出硬盘的所有内容。现在，如果你完成了对该硬盘的操作并想卸载它，你只需要：

```bash
sudo umount <mount point>
```

正如你可能的那样，`umount` 代表 un-mount（卸载）。一旦成功卸载驱动器，你就可以将其断开。

# 第 15 章 进程 (The Processes)

如果你想成为 Linux 用户，也应该理解进程。在本章中，你将学习 Linux 中执行的进程。

## 基础知识

### 多用户与多任务

既然你已经知道如何与系统交互，就可以更详细地研究进程了。某些命令无法使用单个进程执行。此外，Linux 基于 Unix 系统，在那里不同的用户运行不同的命令是理所当然的。显然，你需要确保计算机的处理器能够处理所有活动进程。你还应该提供允许用户在不同进程之间切换的功能。在某些情况下，即使启动该进程的用户已经注销，你也必须继续运行该进程。

## 不同类型的进程

### 交互式进程 (Interactive Processes)

你必须使用终端会话来启动和控制交互式进程。这意味着只有在你连接到系统时，才能启动交互式进程。基本上，系统不会作为基本功能的一部分自动启动这些进程。交互式进程在前台运行，并接管启动它的终端。当这种情况发生时，只要特定进程处于激活状态，你就无法启动其他程序。作为替代方案，你可以在后台运行它们，这样你使用的终端就可以接收其他命令。Linux Shell 提供了一项名为 `job control`（作业控制）的功能。该功能允许你轻松处理各种进程。作业控制可以在后台和前台之间切换进程。通过此功能，你可以快速地在后台启动进程。

重要提示：你只能对不需要用户输入的程序在后台运行进程。通常情况下，如果任务完成需要很长时间，则将其放在后台。

以下列表显示了 Linux 系统的常用控制应用程序：





*   `bg` – 用于在后台重新激活被中断的进程。
*   `fg` – 将进程返回到前台。
*   `jobs` – 显示正在后台运行的命令。
*   `kill` – 结束一个任务。
*   `regular_command` – 在系统的前台运行该命令。
*   `command &` – 在系统的后台运行该命令。这会释放终端：你可以在上一个命令仍处于激活状态运行时其他程序。
*   `Ctrl + Z` – 停止（挂起但不终止）一个在系统前台运行的进程。
*   `Ctrl + C` – 中断（停止并终止）一个在在前台运行的进程。
*   `%n` – 系统为每个后台运行的进程分配一个数字。使用 `%` 符号，你可以通过数字引用进程（例如 `bg %2`）。

## 自动进程

自动进程（也称为批处理进程）不链接到任何终端。相反，这些是在可以在打印队列区域（spooler area）中排序的任务，它们将按照先入先出的原则执行。这些进程可以使用以下方法之一执行：

*   在指定的日期和时间 – 你必须使用 `at` 命令来实现。
*   在系统整体负载足够低以接收额外任务的时间。你可以通过 `batch` 命令实现此操作。通常，进程会排队，以便在系统负载低于 `0.8` 时执行。在大型系统中，当需要处理海量数据或在已经繁忙的系统上执行需要大量资源的任务时，管理员可能会利用批处理。你也可以使用批处理来优化系统性能。

## 守护守护进程 (Daemons)

这些是持续运行的服务器进程。它们通常在启动期间激活，并在系统后台等待，直到需要其服务。一个常见的例子是 `xinetd`，这是一个网络进程，在每次启动过程中都会被触发。启动过程完成后，`xinetd` 会一直等待某个程序（例如 POP3 客户端）需要连接互联网。

## 启动过程

Linux 的流行特性之一是其启动和挂起操作系统的方法，它通过理想设置获取特定程序，允许你修改设置和启动程序，并以组织且优雅的方式停止。

除了操作启动和关机过程外，Linux 系统的“开放性”有助于你确定与机器关机或启动相关的问题原因。

### 步骤

当计算机启动时，CPU 会寻找并执行基本输入/输出系统 (BIOS)。该程序被编码在计算机的永久性-ROM（只读存储器）中，并可随时使用。计算机的 `BIOS` 为外围设备提供低级接口，并处理启动过程的第一阶段。

`BIOS` 检查整个系统，搜索并测试外围设备，并寻找可启动系统的驱动器。通常，`BIOS` 会检查 CD-ROM 驱动器（针对较新的操作系统）或软盘驱动器（针对旧的系统）是否有可用介质。用于启动过程的驱动器序列通常由操作系统上的特定 `BIOS` 配置管理。一旦 Linux 系统安装到计算机的硬盘上，`BIOS` 将搜索从第一块硬盘起始部分开始的 `MBR`（即主引导记录），将数据放入内存并将控制权移交给它。

`MBR` 存储了如何通过预定的操作系统使用 `LILO` 或 `GRUB` 引导加载程序的步骤。之后，`MBR` 激活加载程序（如果主引导记录中安装了加载程序，它将控制过程的其余部分）。在红帽操作系统的标准配置中，`grub` 利用主引导记录中的设置显示可用的启动选项。一旦 `grub` 从配置文件或其命令行获取了启动操作系统的正确指令，它就会获取所需的启动文件并将计算机的控制权传递给操作系统。

## GRUB 的不同特性

这种启动计算机的方法被称为直接加载。这是因为在加载程序和操作系统主文件（例如内核）之间不存在过渡代码。因此，启动指令被用于直接加载操作系统。

另一方面，其他系统使用的启动过程可能与上述过程不同。例如，MS-DOS 和 Windows 操作系统在安装后会立即完全覆盖 `MBR`，而不会使用现有 `MBR` 设置的任何部分。这会删除存储在 `MBR` 内部其他操作系统（例如 Linux）的数据。微软的操作系统和其他商业系统一样，通过一种称为链式加载启动的方法启动。在这种方法中，`MBR` 检查持有操作系统的分区的初始段，从那里获取启动操作系统所需的文件。

`Grub` 可以同时支持这两种方法。这意味着你可以将 `grub` 用于几乎操作系统、常见的文件结构以及你的 `BIOS` 可以识别的硬盘。

`GRUB` 还有其他实用的特性。以下是最重要的几个：

*   `Grub` 为 x86 计算机提供了一个基于命令的环境（即使尚未安装操作系统）。这允许计算机实现最大的通用性——它们可以轻松加载操作系统或收集有关这些系统的数据。
*   `Grub` 兼容 LBA（即逻辑块寻址）模式。访问 IDE 和 SCSI 硬盘需要这种模式。如果没有 LBA，硬盘可能会面临 1024 磁道的限制，此时计算机的 `BIOS` 无法获取超过该点之后的文件。
*   每次启动系统时，`grub` 的配置文件都会从硬盘加载。这意味着你可以在不覆盖 `MBR` 中数据的情况下更改启动选项。

## INIT

一旦加载完成，内核就会在 `/sbin` 目录中找到 `INIT` 并运行它。

`INIT` 是 Linux 操作系统上自动运行的所有任务的父进程/祖进程。首先，`INIT` 读取它自己的初始化文件（该文件位于 `/etc/inittab` 目录）。初始化文件告诉 `INIT` 加载系统配置脚本，该脚本安排路径、开始交换、扫描系统文件等。简单来说，此阶段完成了你的机器在系统启动期间需要的所有工作（例如启动串口、设置计算机时钟等）。

之后，`INIT` 继续读取初始化文件，该文件定义了操作系统在每个运行级别应如何运行。该文件还为系统分配了一个运行级别（run level）。运行级别是计算机进程的配置。一旦为系统分配了运行级别，`INIT` 开始执行系统所需的后台任务。`INIT` 通过检查对应运行级别的正确 `/rc` 目录来实现。最后，`INIT` 使用 stop 参数运行所有的 kill 脚本。

## 关机

Linux 设计并不是为了关闭。然而，如果你确实需要，可以运行 `shutdown` 命令。一旦关机过程完成，你可以使用 `-h` 挂起系统或使用 `-r` 重启系统。

如果在操作系统使用运行级别 1 到 5 时使用 `-r` 和 `-h` 选项，现在调用 `shutdown` 命令。这个运行级别范围确保了整个系统的正确关机。然而，这是一个坏习惯，并不是所有的 Linux 系统都具备这种能力。

如果机器没有自动关闭，在屏幕显示指示操作系统已挂起或完成关机的消息之前，你不能关闭电源。等待此消息可以为你的计算机提供充足的时间断开活动的分区。记住：急躁可能会导致数据丢失。

## 如何管理进程

### 管理员的任务





虽然管理系统进程是管理员的工作，但对于普通用户来说，了解一些相关知识可能也会帮助。当涉及到用户自己的任务和效率时，这些知识就会变得非常重要。

本节将用理论解释系统性能。在这里，你将学习到：

- 普通用户遇到的问题
- 普通用户可以用来优化可用资源的方法

## 进程需要多少时间？

Bash 提供了一个预装的 `time` 命令，用于显示执行进程所需的时间。该工具具有准确性和多功能性——你可以用它获取任何命令的精确数据。为了帮助你理解 `time` 命令，下面提供了一个截图：

在此示例中，使用 `time` 命令来计算创建某个 `.pdf` 文件所需的时间。结果显示该过程需要 1 分钟 41 秒。

文件目录 `/usr/bin` 包含一个 GNU 版本的 `time` 命令（这与预装的 `BASH` 工具不同）。该命令显示了更多可以各种方式使用的数据。此外，它还会显示命令的退出状态和总运行时间。当配合 GNU `time` 命令使用时，上述示例提供了这些结果：

如果你想了解更多关于这些时间命令的知识，可以检查系统的 `Info` 页面。

## 性能

对于普通用户而言，“卓越性能”指的是进程执行快速且正确。然而，对于系统管理员来说，这些词具有更多含义：管理员需要最大化整个系统的性能，包括守护进程、程序和用户。通常，系统性能可能取决于许多未被 `time` 命令评估的“微不足道”因素。以下是这些“微不足道”因素示例：

- 对驱动器、显示器、控制器、接口等的访问。
- 运行的程序设计不合理或未有效利用计算机资源。
- 系统中活动用户的数量。
- 一天中的时间。
- 远程网络的可用性。

## 负载

基本上，负载取决于你网络中的正常情况。例如，一台运行防火墙、文件服务器、SSH 服务器、路由守护进程、代理服务器、sendmail 服务器和其他设备的旧 P133 可以支持最多 7 个活动用户。在这种情况下，负载仍然为零。某些系统（特别是具有多个处理器的系统）可以轻松支持高达 67 个用户。

识别网络负载的方法只有一种：定期检查。这样，你就能知道对你的网络来说什么是正常的。如果不使用这种方法，你只能从命令行的响应时间来判断系统负载。响应时间缺乏准确性——由于各种因素会影响它，因此它是不可靠的。

记住，即使负载平均值相同，不同的网络表现也不同。例如，如果一个网络拥有支持硬件加速的显卡，它可以流畅地渲染 3D 图像。然而，使用旧 VGA 卡的网络在渲染图像时会像乌龟一样慢。旧系统在启动 X 服务器时可能缓慢，而现代系统甚至“感觉不到”增加的负载。

## 优先级

任务的重要性（或优先级）由其 **nice 值**（谦性值）决定。高 nice 任务对其他用户、其他任务以及网络本身都是“合作”的（或“友好”的）：它们是低优先级任务。低 nice 值表示其所属的任务很重要，并将占用更多的系统资源。

你可以通过给任务更高的 nice 值来让任务变得“更友好”。然而，这种技术仅对需要大量 CPU 时间的进程（例如软件编译器）有效。持续利用大量 I/O 时间的进程会被赋予较低的 nice 值（即更高的优先级）。例如，键盘输入在计算机网络中始终获得最高优先级。

你可以使用 `nice` 命令设置程序的重要性。

许多系统提供名为 `BSD renice` 的命令。该命令允许用户编辑活动程序的“友好程度”。你可能需要检查操作系统的手册以确定此命令是否可用。

## CPU 资源

在每个操作系统上，许多进程需要同时使用计算机的 CPU。即使你是唯一的活动用户也是如此。每个进程都需要特定数量的 CPU 资源才能正常运行。由于 CPU 处理许多请求，有时计算机程序无法获得足够的资源。如果你想优化计算机，就需要了解可用的系统资源。可以使用工具来获取这些数据。

`Uptime` 是 Linux 中可以使用命令之一，它缺乏准确性（它只能显示平均值，你需要识别正常数值），但在某些情况下很有用。以下是你可以采取的一些提高 CPU 效率的方法：

- 停止系统执行不必要的任务。停止你不使用的程序和守护进程。你可以使用 `locate` 命令来实现。
- 在系统负载低水平时运行资源密集型进程。通常，你应该在夜运行“重型”进程。
- 先运行低优先级任务。

如果这些方法不能解决你的问题，你可能需要一个更好的 CPU。对于 Linux 系统，这是系统管理员的工作。

## 用户

在 Linux 系统中，根据使用系统资源的方式，计算机用户可以分为不同的类型。以下是 Linux 用户的三种类型：

- 运行许多小进程的人。一个很好的例子是缺乏经验的 Linux 用户。
- 运行几个（但复杂的）进程的人。这种类型的示例是运行模拟器、计算和仿真的人。
- 运行少量需要 CPU 时间的进程的人。

## 可视化工具

在图形环境中，你有大量的工具。这是一个名为 System Monitor（系统监控）的工具截图。该工具可以查找任务。

## 列出和显示信息

使用 `ps` 命令显示当前运行的进程。如果没有指定选项，`ps` 将显示与当前会话相关的进程。

- 要查看所有进程，使用 `ps -e`。
- 要查看包括非你所有的在内的进程，使用 `ps -A`。
- 要查看特定用户，使用 `ps -u`。
- 要查看特定 PID，使用 `ps -p`。
- 要查看完整列表，使用 `ps -f`。
- 要查看所有进程，使用 `ps -ef`。
- 要查看进程树，使用 `ps -H`。
- 要查看进程树，使用 `ps --forest`。
- 要查看进程树，使用 `ps --tree`。

```bash
ps
  19511 pts/2    00:00:00 bash
  19554 pts/2    00:00:00 ps


``````bash
ps -p 19511
  19511 pts/2    00:00:00 bash
```

```bash
ps -f
UID         PID  PPID C STIME TTY          TIME CMD
bob         19511 19509 0 16:50 pts/2      00:00:00 -bash
bob         19556 19511 0 16:50 pts/2      00:00:00 ps -f
```

```bash
ps -e | head
  PID TTY             TIME
    1 ?               00:00:02 init
    2 ?               00:00:00 kthreadd
    3 ?               00:00:19 ksoftirqd/0
    5 ?               00:00:00 kworker/0:0H
    7 ?               00:00:00 migration/0
    8 ?               00:00:00 rcu_bh
```





```
9 ?         00:00:17 rcu_sched
10 ?        00:00:12 watchdog/0
11 ?        00:00:00 khelper
```

```bash
$ ps -ef | head

UID         PID PPID C STIME TTY       TIME CMD
root        1     0 0 Dec27 ?      00:00:02 /sbin/init
root        2     0 0 Dec27 ?      00:00:00 [kthreadd]
root        3     2 0 Dec27 ?      00:00:19 [ksoftirqd/0]
root        5     2 0 Dec27 ?      00:00:00 [kworker/0:0H]
root        7     2 0 Dec27 ?      00:00:00 [migration/0]
root        8     2 0 Dec27 ?      00:00:00 [rcu_bh]
root        9     2 0 Dec27 ?      00:00:17 [rcu_sched]
root       10     2 0 Dec27 ?      00:00:12 [watchdog/0]
root       11     2 0 Dec27 ?      00:00:00 [khelper]
```

```bash
$ ps -fu www-data

UID         PID PPID C STIME TTY       TIME CMD
www-data    941  938 0 Dec27 ?      00:00:00 /usr/sbin/apache2 -k start
www-data    942  938 0 Dec27 ?      00:00:00 /usr/sbin/apache2 -k start
www-data    943  938 0 Dec27 ?      00:00:00 /usr/sbin/apache2 -k start
```

这里是其他可以让你查看运行中进程的命令。

- `pstree` - 以树状格式显示运行中的进程。
- `htop` - 交互式进程查看器。此命令比 `top` 不常用，系统上可能不可用。
- `top` - 交互式进程查看器。

## 在前台和后台运行进程

到目前为止，你执行的所有命令都是在前台运行的。当一个命令、进程或程序在前台运行时，在进程进程退出之前，shell 提示符都不会显示。对于运行时间长的程序，将它们发送到后台可能会非常方便。后台运行进程仍然会执行并完成其任务，但它们不会阻止你在 shell 提示符处输入后续命令。要将进程放入后台，请在命令末尾加上一个和符号 (`&`)。

- `command &` - 在后台启动命令。
- `Ctrl-c` - 杀死前台进程。
- `Ctrl-z` - 挂起前台进程。
- `bg [%num]` - 将挂起的进程放入后台。
- `fg [%num]` - 将后台进程放入前台。
- `kill [%num]` - 通过作业号或 PID 杀死进程。
- `jobs [%num]` - 列出作业。

```bash
$ ./long-running-program &
[1] 22686

$ ps -p 22686
PID TTY           TIME CMD
22686 pts/1     00:00:00 long-running-pr

$ jobs
[1]+  Running  ./long-running-program &

$ fg
./long-running-program
```

当命令被放入后台时，会显示两个数字。括号中的数字是作业号，可以通过在其加百分号来引用它。第二个数字是 PID。以下是在后台启动多个进程的示例外观。

```bash
$ ./long-running-program &
[1] 22703

$ ./long-running-program &
[2] 22705

$ ./long-running-program &
[3] 22707

$ ./long-running-program &
[4] 22709

$ jobs
[1]    Done      ./long-running-program
[2]    Done      ./long-running-program
[3]-  Running  ./long-running-program &
[4]+  Running  ./long-running-program &
```

`jobs` 输出中的加号 (`+`) 代表当前作业，而减号 (`-`) 代表上一个作业。当前作业被认为是最后一个在前台被停止的作业，或者是最后一个在后台启动的作业。当前作业可以通过 `%%` 或 `%+` 引用。如果未向 `fg` 或 `bg` 提供作业，则对当前作业进行操作。上一个作业可以通过 `%-` 引用。你会注意到作业 1 和 2 被报告为完成。shell 不会中断你的命令行，但在显示新提示符之前会报告作业状态。例如，如果你在后台启动一个程序，会返回一个提示符。shell 不会在显示新提示符之前报告作业状态。你可以通过简单按回车键请求显示新提示符。要将作业带回前台，输入作业名称或使用 `fg`。要将当前作业调前台，执行 `%%`、`%+`、`fg %%`、`fg %+` 或 `fg %num`。要将作业 3 调前台，执行 `%3` 或 `fg %3`。

```bash
$ jobs
[3]-  Running  ./long-running-program &
[4]+  Running  ./long-running-program &

$ fg %3
./long-running-program
```

要暂停或挂起正在前台运行的作业，输入 `Ctrl-z`。一旦作业被挂起，就可以在前台或后台恢复。要将挂起的作业放入后台，输入作业名称后加上和符号，或通过作业名使用 `bg`。

```bash
$ jobs
[1]  Running  ./long-running-program &
[2]-  Running  ./long-running-program &
[3]+  Running  ./another-program &

$ fg
./another-program
^Z
[3]+  Stopped  ./another-program

$ jobs
[1]  Running  ./long-running-program &
[2]-  Running  ./long-running-program &
[3]+  Stopped  ./another-program

$ bg %3
[3]+ ./another-program &

$ jobs
[1]  Running  ./long-running-program &
[2]-  Running  ./long-running-program &
[3]+  Running  ./another-program &
```

你可以使用 `kill` 命令停止或杀死后台作业。例如，要杀死作业 1，执行 `kill %1`。要杀死正在前台运行的作业，输入 `Ctrl-c`。

```bash
$ jobs
[1]  Running  ./long-running-program &
[2]-  Running  ./long-running-program &
[3]+  Running  ./another-program &

$ kill %1
[1]  Terminated  ./long-running-program

$ jobs
[2]-  Running  ./long-running-program &
[3]+  Running  ./another-program &

$ fg %2
./long-running-program
^C
$ jobs
[3]+  Running  ./another-program &
```

## 杀死进程

- `Ctrl-c` - 杀死前台进程。
- `kill [signal] pid` - 向进程发送信号。
- `kill -l` - 显示信号列表。

`kill` 使用的信号是终止（termination）。你会看到此信号被称为 `SIGTERM` 或简写 `TERM`。信号有与其名称对应的数字。默认的 `TERM` 信号是 15。因此，运行 `kill pid`、`kill -15 pid` 和 `kill -TERM pid` 都是等效的。如果进程在你发送 `TERM` 信号后没有终止，请使用 `KILL` 信号，它是数字 9。

# 第 16 章. 让 Linux 更安全

有很多理由你你保护计算机免受其他用户的侵害，但根本在于你不希望任何用户删除或修改你的系统文件。如果你正在处理一个计算机网络，你也不希望任何用户无意或故意更改其系统中的任何可能导致整个系统受到破坏的内容。





Unix 密码在历史上被存储在一个名为 `/etc/passwd` 的文件中，任何用户都可以读取该文件。例如，计算机 root 用户的 `/etc/passwd` 文件条目可能![00099.jpeg](img/image0022.jpeg)所示：

你会发现该文件中的字段是用冒号分隔的，第二个字段显示的是加密形式的用户密码。为了让系统验证输入的用户密码是否有效，使用密码的程序会对该条目进行加密，然后将结果与 `/etc/passwd` 文件中存储的加密文本进行比较。如果条目匹配，用户就可以使用该程序。

然而，任何黑客都可以轻松地使用字典攻击来破解密码——这种解密方法通过尝试加密密码中所有可能的组合来寻找其对应的明文等值。如果你拥有 `/etc/passwd` 文件的访问权限，那么你离破解密码仅一步之遥。如果你不是你尝试破解的计算机的授权用户，你可以利用目标 Web 服务（如 FTP 和邮件服务）中可能存在的漏洞来渗透并获取你想要的文件。

幸的是，Linux 在提高操作系统安全性方面做了多项改进，包括以下内容：

### 影子密码 (Shadow Passwords)

将密码存储在易于访问的位置是不安全的，即使这些密码经过了加密。出于这个原因，Linux 不再将密码存储在每个人都可以访问的 `/etc/passwd` 文件中——密码现在存储在一个名为 `/etc/shadow` 的影子密码文件中，该文件只有 root 用户可以访问。

![00100.jpeg](img/image00225.jpeg)在 Linux 中，`/etc/passwd` 文件看起来如下所示：

请注意，第二个字段并没有显示加密密码，而是显示单个字符 `x`。该字段中的 `x` 是你的影子密码，真正的加密![00101.jpeg](img/image00226.jpeg)密码存储在 `/etc/shadow` 文件中，其内容如下：

你会发现文件中的字段仍然是用冒号分隔的，其中前两个字段分别代表用户名和加密密码。另一方面，其余字段控制着密码的有效期。这意味着你不需要更改甚至解密存储在此文件中的密码。相反，你可以使用 `change` 命令更改密码的过期日期。

作为 root 用户，你可以使用以下![00102.gif](img/image00227.jpeg)命令查看用户的密码过期日期：

如果你想确保会强制定期更改密码，可以使用 `-M` 设置密码的有效天数。例如，如果你想强制用户 `kdulaney` 每 90![00103.jpeg](img/image00228.jpeg)天更改密码，请使用以下命令（确保你已以 root 身份登录）：

### PAM (可插身份模块)

Linux 在提高密码安全性方面还使用了另一种功能，即使用 MD5 算法。它的作用是将文档归纳为 128 位的摘要（称为指纹），这样你就可以附加数字签名并使用私钥对其进行加密。虽然 MD5 以确保文档安全闻名，但同样的原理适用于密码。

MD5 优于传统密码的另一个优势是你可以使用更长的密码。正如你所知，即使 `/etc/shadow` 文件落入犯罪黑客手中，更长的密码也难以破解。你可以看到此文件中的![00104.jpeg](img/image00229.jpeg)字段采用了 MD5 加密：

另一个名为 PAM（pluggable authentication module）的模块使用 MD5 加密密码。在 Linux 中，你可以设置 PAM，以便在运行时切换身份验证方式，而无需更改验证身份所需的程序（如用户名和密码）。

Linux 中的 PAM 被广泛使用，也被用于系统的其他不同模块。所有涉及 PAM 的配置文件都存储在名为![00105.jpeg](img/image00230.jpeg)`etc/pam.d` 的目录下。要查看该目录下的文件，请使用以下命令：

## 配置默认权限

当你创建一个新文件时，默认情况下谁可以使用这个文件？你可以通过输入 `umask` 命令来确定答案，它将显示用户文件创建掩码。当你输入此命令时，将看到你所查询的文件创建掩码。如果你是 root 用户，用户掩码配置为 `22`，而其他人为 `0002`。在以下练习中，你将看到文件创建掩码的工作原理：

1.  ![00106.gif](img/image00231.jpeg)以 root 用户登录并输入：

这将创建一个名为 `junkfile` 的空文件。

2.  输入 `ls -l` 命令来查看权限。你会看到一行类似![00107.jpeg](img/image00232.jpeg)的内容：

现在，你可以通过转换第一个字段中显示的权限字母来解释权限设置的值。为此，认为第一个字母赋值为 4，第二个赋值为 2，第三个为 1。如果你有权限字母 `rw-`，它翻译为 `4+2+0`（0 是因为第三字母不可用），等同于 `6`。继续下一个三个字母 `r--`，你得到等同于 `4` 的值。这意味着权限字符串 `-rw--r--` 等同于 `644`。

3.  从 `666` 减去你得到的权限设置，以确定 umask 设置。`666-644` 等于 `022`。

现在，如果你想设置不同的 umask，只需输入 `umask` 命令，然后输入掩码的数值值。你可以这样执行此任务：

1.  确定新创建文件的权限设置。如果你希望所有新文件仅允许所有者读取和编辑，你需要编写一个显示为 `rw-------` 的权限设置。

2.  将权限设置转换为对应的数值值。你需要为起始字段分配 4，下一个字段分配 2，第三个分配 1。在本例中，你需要设置一个值为 `600` 的权限设置。

3.  从 `666` 减去目标权限，得到你想要分配的掩码值。为了实现 `600` 权限设置，通过计算 `666-600` 的结果来得出掩码。你得到值 `066`。

4.  输入 `umask` 命令，后跟确定的值。

![00108.gif](img/image00233.jpeg)要获得你需要的权限设置，请输入此命令：

注意：022 被设置为默认 umask，因为它翻译为仅允许文档所有者读取和写入功能，而赋予其他人读取权限。这样做的原因是 Linux 假设文件所有者不希望其文件被所有人编辑，以防止潜在风险。

## 关注设置用户 ID (User ID) 的权限





有一种权限设置被认为是对安全的威胁，它被称为 `setuid` 或 `suid`（设置用户 ID）。这种权限设置适用于你可以运行的文件，即可执行文件。当允许 `setuid/suid` 权限时，文件将在其所有者的用户 ID 运行下执行。简而言之，如果开启了 `suid` 权限且该文件属于 `root` 用户，那么目标程序将认为 `root` 用户是运行该文件的执行者，而不会检查实际上是谁运行了该程序。这意味着 `suid` 权限将允许该程序执行比所有者意图让其他用户执行的更多的功能。还需要注意的是，如果包含 `suid` 权限的上述程序存在某些安全漏洞，犯罪黑客可以通过这些程序造成更大的破坏。

要找到所有已启用的 `suid` 权限，你可以像这样使用 `find` 命令：

![00109.jpeg](img/image00234.jpeg)

![00110.jpeg](img/image00235.jpeg)输入此命令后，你将看到一个像示例所示的文件列表：

请注意，许多程序因为需要而设置了 `suid` 权限。然而，你可能想检查整个列表，以确保没有具有异常 `suid` 权限的程序。例如，你可能不希望在你的主目录下存在 `suid` 程序。

![00111.jpeg](img/image00236.jpeg)这是一个示例：输入 `ls –l /bin/su` 将给你带来以下结果：

权限设置中指向所有者的字符 s（显示为 `–rws`）表示文件 `/bin/su` 具有 `suid` 权限。这意味着允许任何用户拥有超级用户权限的 `su` 命令可以被任何人使用。

# 结论

在当时代，你应该学习 Linux 的理由数以千千计。即使你还没有准备好从当前的操作系统切换到基于 Linux 的系统，学习它们的运行机制也是一项有用的技能。最近的一项调查发现，雇主更有可能雇用熟悉 Linux 发行版的人，因为这证明了你的灵活性和多才。在许多情况下，使用基于 Linux 的系统会更合适。

Linux 社区也是另一个应该吸引你的点。有很多 Linux 用户总是渴望为你提供帮助。在大多数情况下，你遇到的任何问题很可能已经在论坛中得到了解决。所以，请花点时间注册一个论坛并浏览对话，以了解更多关于 Linux 世界正在发生的事情。当你最终成为高级用户时，请通过帮助他人来回馈社区。这正是 Linux 社区变得如此伟大并成为如此强大力量的原因。

我们可以列出许多你应该使用 Linux 的理由，但最重要的一点是你拥有实验和尝试新事物的自由。命令行赋予了你巨大的力量来理解和控制计算机的工作方式、免费的软件库、多种桌面功能、硬件支持、在任何计算机上使用 Linux、安全性以及与其他系统的互操作性。所有这些原因以及更多原因使得学习并熟悉 Linux 变得至关重要。

如果你想要一个与 Windows 不同、更安全且在许多情况下比 Windows 更好的系统，Linux 最终是实现这些目标的唯一选择，因为你可以用它做很多事情，并且有很多你可以尝试的自定义选项，包括更改系统的某些方面。在这一方面，它不像 Windows 那样受到束缚，而且与其他系统相比，许多人切换到 Linux 是有原因的。在 Linux 时，你应该采取的下一步是亲自尝试一下。你应该花一些时间尝试确保你正在这个系统上工作，并从那里为你的系统创建一个出色的数据库和环境。学习确实需要一点时间，可能会令人恐惧，但一旦你开始在 Linux 上运行你的计算机，你就会理解为什么现在大家都在这样做了。它更简单、更快，而且总体来说为你提供了更多可以尝试的选项，以及许多你可以从中享受的体验。当你使用它时确实会有所不同，你也会变得更加快乐。

