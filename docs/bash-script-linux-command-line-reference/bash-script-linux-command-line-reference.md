
# BASH 脚本 Linux 命令行参考指南

![](img/f56a99e3c386b03fdc3134b00fa0e57a_0_0.png)

**要点：** Linux 发行版可以利用广泛的命令来完成各种任务。对于大多数 Linux 发行版，`Bash`（bourne again shell）是执行这些命令的默认命令行界面或壳（shell）。在这份从 A 到 Z 的命令列表中，我们尝试包含了尽可能多的可以使用 `bash` 运行的命令。

> CLI（命令行界面）已经存在很久了。我们可以将其根追溯到 20 世纪 50 年代为了“通过打字机与计算机进行交互”而构建的首个 CLI。它允许用户与系统进行交互，从键盘或脚本接收基于字符的命令输入。然而，CLI 只是一个界面，主要任务是由名为命令行语言解释器的程序完成的。

在过去，我们编写了 Microsoft Windows 中 `CMD` 命令行解释器的命令列表，你可以在下方查看：

> 另请阅读：你需要的 Windows `CMD` 命令从 A 到 Z 全列表

众所周知，即使 Linux 系统的图形桌面环境已经变得非常用户友好，命令行界面（CLI，也称为 shell）仍然各种 Linux 用户数字生活中不可或缺的一部分。

当你进入 shell 时看到的第一段文本被称为“提示符”（prompt）。它表示系统已准备好执行命令。通过终端（Terminal）访问 shell —— 终端是一种用于输入数据和显示输出的硬件设备。然而，你在 Linux 系统上使用的终端应用程序是一个仿真器，复制了真实世界终端的功能。

许多人经常混淆 shell（壳）和 terminal（终端）这两个术语。以汽车为例：车身是终端，仪表盘可以被视为 shell，你可以在仪表盘上执行加速、倒车、换挡等各种操作。汽车会对你通过仪表盘执行的操作做出响应。同样地，终端会显示使用 shell 或 CLI 执行的命令的响应。

## Linux CLI 是区分大小写的吗？

答案是，肯定的。如果你尝试运行 `LS` 而不是 `ls`，它将显示错误。使用区分大小写的命令行界面有一些优势。几十年前的计算机不够快，比较相同的字符串比归一化大小写更有利。这种做法持续并变成了一种习惯，尽管今天的机器已经快得多、高效得多。它还为人们在选择命令名称时提供了灵活性。

# Linux 命令 A-Z列表

所以，在这篇文章中，我尝试编译了一份在各种 Linux 发行版使用的命令列表。这是通过 `Ubuntu Wiki`、`SS64` 和 `Linux Dev Center` 的输入实现的。正如你可能知道的，其中某些或许多命令可能在你的发行版无法运行。运行这些命令可能需要你安装额外的包，或者这些命令本身就不是为你的系统而设计的。

这些 Linux 命令的描述基于它们的帮助页（man pages）。要访问帮助页：

```
man command_name
```

例如：`man cat`

如果你发现任何差异，请随时联系我们进行纠正。

## Linux 命令 – A

| 命令 | 描述 |
| :--- | :--- |
| `accept` | 接受或拒绝到目标（如打印机）的任务。 |
| `access` | 检查用户对文件的 `RWX`（读写执行）权限。 |
| `aclocal` | `GNU autoconf` 工具 |
| `aconnect` | `ALSA` 序列器连接管理器。 |
| `acpi` | 显示关于高级配置和电源接口（`ACPI`）的信息。 |
| `acpi_available` | 检查系统是否存在 `ACPI` 功能。 |
| `acpid` | 通知用户空间程序 `ACPI` 事件。 |
| `addr2line` | 用于将地址转换为文件名和行号。 |
| `addresses` | 互联网邮件地址的格式。 |
| `agetty` | 一种替代的 Linux `Getty` |
| `alias` | 为 Linux 命令创建别名 |
| `alsactl` | 访问 `ALSA` 声卡驱动程序的高级控制。 |
| `amidi` | 为 `ALSA RawMIDI` 端口执行读/写操作。 |
| `amixer` | 访问 `ALSA` 声卡驱动的基于 CLI 的混音器。 |
| `anacron` | 用于定期运行命令。 |
| `aplay` | 适用于 CLI 的音频录制器和播放器。 |
| `aplaymidi` | 用于播放 MIDI 文件的命令行工具。 |
| `apm` | 在旧系统上显示高级电源管理（`APM`）硬件信息。 |
| `apmd` | 用于处理由 `APM BIOS` 驱动程序报告的事件。 |
| `apropos` | 显示包含特定关键字的所有帮助页列表 |
| `apt` | 高级包工具，Debian 及其衍生版本的包管理系统。 |
| `apt-get` | 基于 `APT` 系统安装/删除/更新包的命令行工具。 |
| `aptitude` | 另一个基于 `APT` 系统添加/删除/升级包的工具。 |
| `ar` | 用于从归档创建/修改/提取的工具。 |
| `arch` | 显示打印机硬件名称。 |
| `arecord` | 就像 `aplay`，它是 `ALSA` 声卡驱动的音频录制器和播放器。 |
| `arecmidi` | 录制标准 MIDI 文件。 |
| `arp` | 用于更改系统的 `ARP` 缓存 |
| `as` | 可移植的 GNU 汇器。 |
| `aspell` | 交互式拼写检查工具。 |
| `at` | 用于在指定的日期时间调度命令执行，从输入文件中读取命令。 |
| `atd` | 用于执行由 `at` 命令队列的任务。 |
| `atq` | 列出用户等待 命令的待处理任务。 |
| `atrm` | 删除由 `at` 命令队列的任务。 |
| `audiosend` | 用于将音频录制作为电子邮件发送。 |
| `aumix` | 音频混音器工具。 |
| `autoconf` | 从 `TEMPLATE-FILE` 生成配置脚本并将输出发送到标准输出。 |
| `autoheader` | 为配置创建模板头文件。 |
| `automake` | 从模板文件创建符合 GNU 标准的 `Makefile` |
| `autoreconf` | 更新生成的配置文件。 |
| `autoscan` | 生成初步的 `configure.in` |
| `autoupdate` | 将 `configure.in` 文件更新到较新的 `autoconf`。 |
| `awk` | 用于在文件（文件）中查找和替换文本。 |

## Linux 命令 – B

| 命令 | 描述 |
| :--- | :--- |
| `badblocks` | 磁盘分区中的坏道。 |
| `banner` | 用于将字符作为海报打印。 |
| `basename` | 用于通过目录或后缀显示文件名。 |
| `bash` | GNU `Bourne-Again Shell`。 |
| `batch` | 用于在标准输入上运行命令。 |
| `bc` | 访问 GNU 计算 计算工具。 |
| `bg` | 将进程发送到后台。 |
| `biff` | 在运行 `comsat` 服务器的系统上通知入站邮件和发送者姓名。 |
| `bind` | 用于将名称绑定到套接字。 |
| `bison` | 一个 GNU 解析器生成器，兼容 `yacc`。 |
| `break` | 用于退出循环（例如：`for`, `while`, `select`）。 |
| `builtin` | 用于运行 shell 内置命令，为扩展其功能的命令创建自定义函数。 |
| `bzcmp` | 用于为 `bzip2` 压缩文件调用 `cmp` 程序。 |
| `bdiff` | 为 `bzip2` 压缩文件调用 `diff` 程序。 |
| `bgrep` | 为 `bzip2` 压缩文件调用 `grep`。 |
| `bzip2` | 一种用于缩小给定文件的块排序压缩器。 |
| `bzless` | 用于对 `bzip2` 压缩文件应用‘less’（一次显示页信息）。 |
| `bzmore` | 用于对 `bzip2` 压缩文件应用‘more’（`less` 的低级版本）。 |

## Linux 命令 – C

| 命令 | 描述 |
| :--- | :--- |
| `cal` | 显示日历。 |
| `cardctl` | 用于控制 `PCMCIA` 插槽并选择配置方案。 |
| `cardmgr` | 监控 `PCMCIA` 设备插槽的添加/删除。 |
| `case` | 通过匹配模式条件地执行命令。 |
| `cat` | 用于连接文件并将其打印到屏幕上。 |
| `cc` | GNU C 和 C++ 编译器。 |

| 命令 | 描述 |
| :--- | :--- |
| `cd` | 用于切换目录。 |
| `cddawav` | 用于从 CD-ROM 刻录并 WAV 文件。 |
| `cdparanoia` | 使用数据验证算法更可靠地从 CD 录制音频。 |
| `cdrdao` | 将指定的所有内容一次性写入 CD。 |
| `cdrecord` | 用于刻录数据或音频光盘。 |
| `cfdisk` | 显示或更改磁盘分区表。 |
| `chage` | 用于更改用户密码信息。 |
| `chattr` | 用于更改文件属性。 |
| `chdir` | 切换工作目录。 |
| `chfn` | 用于更改真实用户名和信息。 |
| `chgrp` | 用于更改文件的组所有权。 |
| `chconfig` | 管理运行级别服务的执行。 |
| `chmod` | 修改文件的访问权限。 |
| `chown` | 更改文件的所有者或组。 |
| `chpasswd` | 批量更新密码。 |
| `chroot` | 以 `root` 权限运行命令。 |
| `chrt` | 修改实时进程属性。 |
| `chsh` | 切换登录 shell。 |
| `chvt` | 更改前景虚拟终端。 |
| `ccksum` | 对文件执行 `CRC` 校验和。 |
| `clear` | 用于清除终端窗口。 |
| `cmp` | 比较两个文件（按字节比较）。 |
| `col` | 从输入中过滤反向（和半反向）换行符。 |
| `colcrt` | 为 `CRT` 预览过滤 `nroff` 输出。 |

| 命令 | 描述 |
| :--- | :--- |
| `colrm` | 删除文件行中的列。 |
| `column` | 将输入格式化为列的实用。 |
| `comm` | 用于按行比较两个已排序的文件。 |
| `command` | 在忽略 shell 函数命令的情况下执行带参数的命令。 |
| `compress` | 用于压缩一个或多个文件并替换原始文件。 |
| `continue` | 继续循环的下一次迭代。 |
| `cp` | 将一个文件的内容复制到另一个文件。 |
| `cpio` | 在归档文件之间复制文件。 |
| `cpp` | GNU C 语言处理器。 |
| `cron` | 用于执行计划命令的守护进程。 |
| `crond` | 与 `cron` 功能相同。 |
| `crontab` | 为用户管理 `crontab` 文件（包含计划命令）。 |
| `csplit` | 根据上下文行将文件拆分为多个部分。 |
| `ctags` | 为编程源文件中定义的函数和宏名称创建列表。 |
| `cupsd` | `CUPS` 的调度调度器。 |
| `curl` | 使用支持的协议从服务器或向服务器传输数据。 |
| `cut` | 从一个或多个文件的每行中删除部分。 |
| `cvs` | 并发版本系统。用于跟踪文件版本，允许存储/检索之前的版本，并允许多个用户处理同一个文件。 |

## Linux 命令 – D

| 命令 | 描述 |
| :--- | :--- |
| `date` | 显示系统日期和时间。 |
| `dc` | 桌面计算器实用。 |
| `dd` | 用于转换和复制文件、克隆磁盘、写入磁盘头等。 |
| `ddrescue` | 用于从崩溃的分区恢复数据。 |
| `deallocvt` | 为未使用的虚拟控制台释放内核内存。 |
| `debugfs` | `ext2/ext3/ext4` 文件系统调试器 |
| `declare` | 用于声明变量并分配属性。 |
| `depmod` | 生成 `module.dep` 和映射文件。 |
| `devdump` | 交互式显示设备或文件系统 `ISO` 的内容。 |
| `df` | 显示磁盘占用。 |
| `diff` | 用于逐行比较文件。 |
| `diff3` | 逐行比较三个文件。 |
| `dig` | 域名信息查询，一种 `DNS` 查找工具。 |
| `dir` | 列出目录内容。 |
| `dircors` | 通过修改 `LS_COLORS` 环境变量为‘ls’设置颜色。 |
| `dirname` | 显示删除斜杠及其字符后的路径名。 |
| `dirs` | 显示记忆中的目录列表。 |

| 命令 | 描述 |
| :--- | :--- |
| `disable` | 限制对打印机的访问。 |
| `dlpsh` | 用于 `PalmOS` 的交互式桌面链接协议 (`DLP`) shell。 |
| `dmesg` | 检查并控制内核缓冲区。 |
| `dnsdomainname` | 显示系统的 `DNS` 域名。 |
| `dnssec-keygen` | 为给定名称生成加密的安全 `DNS` 密钥。 |
| `dnssec-makekeyset` | 由 `dnssec-keygen` 生成的一个或多个 `DNS` 安全密钥产生域密钥集。 |
| `dnssec-signkey` | 使用密钥标识符列表中指定的签名安全 `DNS` 密钥集。 |
| `dnssec-signzone` | 使用指定标识符列表中的签名安全 `DNS` 区域文件。 |
| `doexec` | 使用提供的任意 `argv` 列表运行执行文件。 |
| `domainname` | 显示或设置当前 `NIS`（网络信息服务）域名。 |
| `dosfck` | 检查并修复 `MS-DOS` 文件系统。 |
| `du` | 显示文件的磁盘占用摘要。 |
| `dump` | `ext2/ext3` 文件系统的备份工具。 |
| `dumpe2fs` | 倾储 `ext2/ext3/ext4` 文件系统。 |
| `dumpkeys` | 显示键盘驱动程序当前翻译表的信息。 |

## Linux 命令 – E

| 命令 | 描述 |
| :--- | :--- |
| `e2fsck` | 用于检查 `ext2/ext3/ext4` 文件系统。 |
| `e2image` | 将重要的 `ext2/ext3/ext4` 文件系统元数据存储到文件中。 |
| `e2label` | 显示或更改 `ext2/ext3/ext4` 文件系统上的标签。 |
| `echo` | 将输入字符串发送到标准输出，即在屏幕上显示文本。 |
| `ed` | GNU `Ed` – 一个面向行的文本编辑器。 |
| `edquota` | 使用文本编辑器（如 `vi`）编辑文件系统配额。 |
| `egrep` | 搜索并显示匹配模式的文本。 |
| `eject` | 弹出可移动介质。 |
| `elvtune` | 用于为指定的块设备调度 `I/O` 活动的电梯算法设置延迟。 |
| `emacs` | `Emacs` 文本编辑器命令行工具。 |
| `enable` | 用于启用/禁用 shell 内置命令。 |
| `env` | 在修改的环境中运行命令。显示/设置/删除环境变量。 |
| `envsubst` | 替换格式字符串中的环境变量值。 |
| `esd` | 启动 `Enlightenment` 音守护进程 (`Esound` 或 `esd`)。允许多个应用程序同时访问同一个音频设备。 |
| `esd-config` | 管理 `EsoundD` 配置。 |

| 命令 | 描述 |
| :--- | :--- |
| `esd` | 使用 `EsounD` 从指定文件发送音频数据。 |
| `esdctl` | `EsounD` 控制程序。 |
| `esddsp` | 用于将非 `esd` 音频数据重定向到 `es` 并使用 `esd` 控制所有音频。 |
| `esdmon` | 用于复制发送到设备的声音。发送到辅助设备。 |
| `esdplay` | 使用 `EsounD` 系统播放文件。 |
| `esdrec` | 使用 `EsounD` 将音频录制到文件。 |
| `esdsample` | 使用 `esd` 采样。 |
| `etags` | 为编程源文件创建函数和宏列表。`emacs` 使用。对于 `vi` 使用 `ctags`。 |
| `ethtool` | 用于查询和控制网络硬件设置。 |
| `eval` | 用于一次评估多个命令或参数。 |
| `ex` | 交互式命令 |
| `exec` | 交互式行编辑器。 |
| `exit` | 退出终端。 |
| `expand` | 将文件中的制表转换为空格并显示输出。 |
| `expect` | `Tcl` 脚本扩展，根据预期输出自动与其他应用程序交互。 |
| `export` | 用于设置环境变量。 |
| `expr` | 评估表达式并输出到标准输出。 |

## Linux 命令 – F

| 命令 | 描述 |
| :--- | :--- |
| `factor` | 显示指定整数的质因数。 |
| `false` | 什么都不做，失败。以指示失败的状态码退出。 |
| `fc-cache` | 在扫描目录后制作字体缓存。 |
| `fc-list` | 显示可用字体列表。 |
| `fdformat` | 对软盘进行低级格式化。 |
| `fdisk` | 更改磁盘分区表。 |
| `fetchmail` | 从邮件服务器获取邮件并转发到本地邮件投递系统。 |
| `fg` | 将作业发送到前景。 |
| `fgconsole` | 显示当前虚拟终端的编号。 |
| `fgrep` | 从文件中显示指定字符串的行。`grep` 的变体。 |
| `file` | 确定文件类型。 |
| `find` | 在目录层次结构中搜索文件。 |
| `finger` | 显示用户数据，包括每个用户主目录下列出的 `.plan` 和 `.project` 信息。 |
| `fingerd` | 为 `finger` 程序提供网络接口。 |
| `flex` | 生成对文本进行模式匹配的程序。 |



| `fmt` | 用于将文本转换为指定的宽度，通过填充行和移除换行符来显示输出。 |
| `fold` | 将输入行折叠以适应指定的宽度。 |
| `for` | 展开并对结果列表中的每个单词运行命令。 |
| `formail` | 用于将标准输入过滤为邮箱格式。 |
| `format` | 用于格式化磁盘。 |
| `free` | 显示系统空闲和使用的内存。 |
| `fsck` | 检查并修复 Linux 文件系统。 |
| `ftp` | 文件传输协议用户界面。 |
| `ftpd` | FTP 服务器进程。 |
| `function` | 用于定义函数宏。 |
| `fuser` | 查找并杀死访问文件的进程。 |

## Linux 命令 – G

| Command | Description |
|---|---|
| `g++` | 运行 `g++` 编译器。 |
| `gawk` | 用于模式扫描和语言处理。AWK 语言的 GNU 实现。 |
| `gcc` | GNU 提供的 C 和 C++ 编译器。 |
| `gdb` | 用于调试程序并了解崩溃位置的工具。 |
| `gdb` | GNU 提供的 C 和 C++ 编译器。用于调试程序并了解崩溃位置的工具。 |
| `getent` | 显示指定键在名称切换库中的条目。 |
| `getkeycodes` | 显示内核扫描码到键码的映射表。 |
| `getopt` | 解析位置参数的工具。 |
| `gpasswd` | 允许管理员更改组密码。 |
| `gpg` | 根据 OpenPGP 标准启用加密和签名服务。 |
| `gpgsplit` | 用于将 OpenPGP 消息拆分为数据包。 |
| `gpgv` | 用于验证 OpenPGP 签名。 |
| `gpm` | 为 Linux 控制台启用剪切粘贴功能和鼠标服务器。 |
| `gprof` | 显示图表分析数据。 |
| `grep` | 在输入文件中搜索给定模式并显示相关行。 |
| `groff` | 作为 `groff` 文档格式系统的前端。 |
| `groffer` | 显示 `groff` 文件和帮助页（man pages）。 |
| `groupadd` | 用于添加新的用户组。 |
| `groupdel` | 用于删除用户组。 |
| `groupmod` | 用于修改组定义。 |
| `groups` | 显示用户所属的组。 |
| `grpck` | 验证组文件的完整性。 |
| `grconv` | 从组或已存在的 `gshadow` 创建 `gshadow` 文件。 |
| `gs` | 调起 Ghostscript，它是 Adobe PostScript 和 PDF 语言的解释器和预览器。 |
| `gunzip` | 用于压缩/解文件的工具。 |
| `gzip` | 用于在本地压缩可执行文件，并让它们在以后阶段自动解压并运行。 |
| `gzip` | 与 `gzip` 相同。 |

## Linux 命令 – H

| Command | Description |
|---|---|
| `halt` | 用于停止机器的命令。 |
| `hash` | 显示 shell 中执行命令的路径。 |
| `hdparm` | 显示/配置 SATA/IDE 设备的参数。 |
| `head` | 显示每个指定文件的前 10 行。 |
| `help` | 显示内置命令的帮助信息。 |
| `hexdump` | 以十六进制、十进制或 ASCII 格式显示指定文件的输出。 |
| `history` | 显示命令历史。 |
| `host` | 执行 DNS 查询的工具。 |
| `hostid` | 以十六进制格式显示主机的数字 ID。 |
| `hostname` | 显示/设置系统主机名。 |
| `htdigest` | 管理 Apache Web 服务器使用的用户认证文件。 |
| `htop` | 命令行行的交互式进程查看器。 |
| `hwclock` | 显示或配置系统的硬件时钟。 |

## Linux 命令 – I

| Command | Description |
|---|---|
| `iconv` | 将文本文件从一种编码转换为另一种。 |
| `id` | 显示指定用户的 ID 和组信息。 |
| `if` | 条件执行命令。 |
| `ifconfig` | 用于配置网络接口。 |
| `ifdown` | 停止网络接口。 |
| `ifup` | 启动网络接口。 |
| `imapd` | IMAP（交互式邮件访问协议）服务器守护进程。 |
| `import` | 捕获 X 服务器屏幕并保存为图像。 |
| `inetd` | 扩展互联网服务守护进程，它启动提供互联网服务的程序。 |
| `info` | 用于读取 Info 格式的文档。 |
| `init` | Systemd 系统和服务守护管理器。 |
| `insmod` | 向 Linux 内核插入模块的程序。 |
| `install` | 用于将文件复制到指定位置并在安装过程中设置属性。 |
| `iostat` | 显示 CPU、I/O 设备、分区、网络文件系统的统计信息。 |
| `ip` | 显示/操作路由、设备、策略、路由和隧道。 |
| `ipcrm` | 用于删除 System V 进程通信（IPC）对象和相关数据结构。 |
| `ipcs` | 显示调用进程具有读取权限的 IPC 设施信息。 |
| `iptables` | IPv4 包过滤和 NAT 的管理工具。 |
| `iptables-restore` | 用于从输入或文件中指定的数据恢复 IP tables。 |
| `iptables-save` | 将 IP table 内容导出到标准输出。 |
| `isodump` | 显示 `iso9660` 镜像内容以验证目录内容完整性的工具。 |
| `isoinfo` | 用于对 `iso9660` 镜像进行类似目录列出的工具。 |
| `isosize` | 显示指定文件中包含的 `iso9660` 文件系统的长度。 |
| `isovy` | 验证 `iso9660` 镜像的完整性。 |
| `ispell` | 基于 CLI 的拼写检查工具。 |

## Linux 命令 – J

| Command | Description |
|---|---|
| `jobs` | 显示活动作业列表及其状态。 |
| `join` | 对于每对输入行，使用命令字段将它们连接并显示到标准输出。 |

## Linux 命令 – K

| Command | Description |
|---|---|
| `kbd_mode` | 设置键盘模式。不带参数时，显示当前键盘模式。 |
| `kbdrate` | 重置键盘重复率和延迟时间。 |
| `kill` | 向一个多个进程发送杀死（终止）信号。 |
| `killall` | 杀死运行指定命令的进程。 |
| `killall5` | SystemV `kill` 命令。杀死除其所依赖之外的所有进程。 |
| `klogd` | 控制并优先处理显示在控制台上的内核消息，并通过 `syslog` 记录它们。 |
| `kudzu` | 用于通过与现有数据库比较检测新和增强的硬件。仅用于 RHEL 及其衍生版。 |

## Linux 命令 – L

| Command | Description |
|---|---|
| `last` | 通过从 `/var/log/wtmp` 文件获取数据，显示系统最近的登录列表。 |
| `lastb` | 通过从 `/var/log/btmp` 文件获取数据，显示失败的登录尝试列表。 |
| `lastlog` | 显示所有用户或指定用户最近的登录信息。 |
| `ld` | Unix 链接器，合并存档和对象文件。它将它们放入输出文件，解析外部引用。 |
| `ldconfig` | 配置动态链接器绑定。 |
| `ldd` | 显示共享对象依赖。 |
| `less` | 分页显示文件内容。它比 `more` 命令更高级。 |
| `lesskey` | 用于指定 `less` 命令的键绑定。 |
| `let` | 用于对 shell 变量进行整数运算。 |
| `lftp` | 具有额外功能的 FTP 工具。 |
| `lftpget` | 使用 `lftp` 获取 HTTP、FTP 以及 `lftp` 支持的其他协议 URL。 |
| `link` | 在两个文件之间创建链接。类似于 `In` 命令。 |
| `ln` | 创建文件链接。可以是硬链接（同一个文件的两个名称）或软链接（第一个文件的快捷方式）。 |
| `loadkeys` | 加载键盘翻译表。 |
| `local` | 用于创建函数变量。 |
| `locale` | 显示当前或所有 locale 信息。 |
| `locate` | 通过名称查找文件。 |
| `lockfile` | 创建信号文件，用于限制对文件的访问。 |
| `logger` | 在系统日志中创建条目。 |
| `login` | 在系统中创建新会话。 |
| `logname` | 显示当前用户的用户名。 |
| `logout` | 通过更改 `utmp` 和 `wtmp` 文件执行注销操作。 |
| `logrotate` | 用于系统日志文件的自动轮转、压缩、删除和发送。 |
| `look` | 显示文件中包含给定字符串开头的行。 |

| `lsetup` | 设置并控制循环设备。 |
| `ipadmin` | 用于配置 CUPS（通用 UNIX 打印系统）提供的打印机和类队列。 |
| `lpc` | 行打印机控制程序，对 CUPS 打印机和类队列提供有限的控制。 |
| `ipinfo` | 显示 CUPS 服务器知的可用设备和驱动程序列表。 |
| `ipmove` | 将一个或多个打印作业移动到新目标。 |
| `ip` | 显示指定打印机的当前打印队列状态。 |
| `ipr` | 用于提交文件打印。 |
| `iprint` | 用于打印文件。 |
| `iprintd` | 用于终止打印作业。 |
| `iprintq` | 列出打印队列。 |
| `iprm` | 取消打印作业。 |
| `ipstat` | 显示当前类、作业和打印机的状态信息。 |
| `ls` | 显示当前目录的文件列表。 |
| `lsattr` | 显示 Linux `ext2` 文件系统上的文件属性。 |
| `lsblk` | 列出所有可用或指定的块设备的信息。 |
| `lsmod` | 显示 Linux 内核中模块的状态。 |
| `lsof` | 列出打开的文件。 |
| `lci` | 列出所有 PCI 设备。 |
| `lsusb` | 列出 USB 设备。 |

## Linux 命令 – M

| Command | Description |
| --- | --- |
| `m4` | 宏处理器。 |
| `mail` | 用于编写、接收、发送、转发和回复电子邮件的实用。 |
| `mailq` | 显示列出所有等待交付的邮件（sendmail 队列）。 |
| `mailstats` | 显示当前邮件统计数据。 |
| `mailto` | 用于发送带有 MIME 格式多媒体内容的邮件。 |
| `make` | 用于维护程序组的工具，需要时重新编译它们。 |
| `makedbm` | 创建 NIS（网络服务）数据库映射。 |
| `makemap` | 创建 sendmail 中键值映射查找使用的数据库映射。 |
| `man` | 显示 Linux 命令的手帮助页。 |
| `manpath` | 确定手册页的搜索路径。 |
| `mattrib` | 用于更改 MS-DOS 文件属性标记。 |
| `mbadblocks` | 检查 MS-DOS 文件系统的坏块。 |
| `mcat` | 导出原始磁盘镜像。 |
| `mcd` | 用于更改 MS-DOS 目录。 |
| `mcopy` | 从 Unix 或向 拷贝 MS-DOS 文件。 |
| `md5sum` | 用于检查文件的 MD5 校验和。 |
| `mdel, mdeltree` | 用于删除 MS-DOS 文件。`mdeltree` 递归删除 MS-DOS 目录及其内容。 |

| `mdir` | 用于显示 MS-DOS 目录。 |
| `mdu` | 用于显示 MS-DOS 目录占据的空间。 |
| `merge` | 三路文件合并。包括从 `file2` 和 `file3` 到 `file1` 的所有更改。 |
| `mesg` | 允许/不允许 osends 向你的终端发送消息。 |
| `metamail` | 使用 MIME 类型元数据发送和显示富文本或多媒体邮件。 |
| `metasend` | 发送非文本邮件的接口。 |
| `mformat` | 用于向低格式化的软磁盘上添加 MS-DOS 文件系统。 |
| `mimencode` | 在 MIME 多媒体邮件编码格式之间进行转换。 |
| `minfo` | 显示 MS-DOS 文件系统的参数。 |
| `mkdir` | 用于创建目录。 |
| `mkdosfs` | 在 Linux 下创建 MS-DOS 文件系统。 |
| `mke2fs` | 用于创建 `ext2/ext3/ext4` 文件系统。 |
| `mkfifo` | 用于创建给定名称的命名管道 (FIFOs)。 |
| `mkfs` | 在磁盘分区上构建 Linux 文件系统。 |
| `mkfs.ext3` | 与 `mke2fs` 相同，创建一个 `ext3` Linux 文件系统。 |
| `mkisofs` | 用于创建 `ISO9660/JOLIET/HFS` 混合文件系统。 |

| `mklost+found` | 在挂载的 `ext2` 文件系统上创建 `lost-found` 目录。 |
| `mkmanifest` | 创建文件名及其 DOS 8.3 等效名的列表。 |
| `mknod` | 用指定的名称创建 FIFO、块（缓冲）特殊文件、字符（无缓冲）特殊文件。 |
| `mkraid` | 用于设置 RAID 设备列。 |
| `mkswap` | 设置 Linux 交换区。 |
| `mtemp` | 创建临时文件或目录。 |
| `mlabel` | 创建 MS-DOS 卷标签。 |
| `mmd` | 创建 MS-DOS 子目录。 |
| `mmount` | 挂载 MS-DOS 磁盘。 |
| `mmove` | 移动或重命名 MS-DOS 文件或子目录。 |
| `mmv` | 批量移动和重命名文件。 |
| `modinfo` | 显示 Linux 内核模块的信息。 |
| `modprobe` | 从 Linux 内核中添加或删除模块。 |
| `more` | 分页显示文件内容。 |
| `most` | 浏览或分页文本。 |
| `mount` | 挂载文件系统。 |
| `mounted` | NFS 挂载守护进程。 |
| `mpartition` | 分区 MS-DOS 磁盘。 |
| `mpg123` | 命令行 mp3 播放器。 |
| `mpg321` | 类似于 `mpg123`。 |

| `mrd` | 删除 MS-DOS 子目录。 |
| `mren` | 重命名现有的 MS-DOS 文件。 |
| `mshowfat` | 显示分配给文件的 FAT 簇。 |
| `mt` | 控制磁带驱动器操作。 |
| `mtools` | 访问 MS-DOS 磁盘的工具。 |
| `mtoolstest` | 测试并显示 `mtools` 配置。 |
| `mtr` | 网络诊断工具。 |
| `mtype` | 显示 MS-DOS 文件的内容。 |
| `mv` | 移动/重命名文件或目录。 |
| `mzip` | 更改保护模式并弹出磁盘 Zip/Jaz 驱动器。 |

## Linux 命令 – N

| Command | Description |
|---|---|
| `named` | 互联网域名服务器。 |
| `name` | 遵循路径直到找到终端点。 |
| `nameif` | 根据 MAC 地址为网络接口命名。 |
| `nc` | Netcat 工具。任意的 TCP 和 UDP 连接和监听。 |
| `netstat` | 显示网络信息。 |
| `newaliases` | 重建邮件别名数据库。 |
| `newgrp` | 登录新组。 |
| `newusers` | 批量更新/创建新用户。 |

| `nfsd` | 用于控制 Linux 服务器的特殊文件系统。 |
| `nfsstat` | 列出 NFS 统计。 |
| `nice` | 使用修改后的调度优先级运行程序。 |
| `nl` | 在显示文件内容时显示行号。 |
| `nm` | 列出对象文件的符号。 |
| `nohup` | 运行忽略挂断的命令。 |
| `notify-send` | 用于发送桌面通知的程序。 |
| `nslookup` | 用于 DNS 查询。阅读此获取更多信息。 |
| `nsupdate` | 动态 DNS 更新工具。 |

## Linux 命令 – O

| Command | Description |
|---|---|
| `objcopy` | 复制并翻译对象文件。 |
| `objdump` | 显示对象文件的信息。 |
| `od` | 以八进制和其他格式转储文件。 |
| `op` | 操作员访问，允许系统管理员授予用户访问某些操作的权限。 |
| `open` | 使用默认应用程序打开文件。 |
| `openvt` | 在新的虚拟终端 (VT) 上启动程序。 |

## Linux 命令 – P

| Command | Description |
| --- | --- |
| `passwd` | 修改用户密码。 |
| `paste` | 合并文件。向标准输出写入制表分隔的文件。 |
| `patch` | 将补丁文件（包含 `diff` 程序差异）应用于原始文件。 |
| `pathchk` | 检查文件名是否有效或通用。 |
| `perl` | Perl 语言解释器。 |
| `pgrep` | 在所有进程中列出符合标准的 PID。 |



| `pidof` | 查找运行程序的 PID。 |
| `ping` | 向网络主机发送 ICMP 请求。 |
| `pinky` | 轻量级 `finger`。 |
| `pkill` | 根据名称和其他属性向进程发送信号。 |
| `pmap` | 报告进程的内存映射。 |
| `popd` | 弹出栈顶目录并进入栈的新目录。 |
| `portmap` | 将 RPC 程序号转换为端口。 |
| `poweroff` | 关机。 |
| `pppd` | 点对点协议守护进程。 |
| `pr` | 为了打印转换（列或分页）文本。 |
| `printaliases` | 打印当前系统别名。 |
| `printcap` | 打印机能力数据库。 |

# Linux 命令终极 A 到 Z 列表

| `printf` | 显示所有或指定的环境变量的值。<br>根据指定的格式格式化参数。 |
| `ps` | 报告当前进程的快照。 |
| `ptx` | 生成文件内容的置换索引。 |
| `pushd` | 将给定目录添加到栈顶并进入该目录。 |
| `pv` | 监控管道中数据的进度。 |
| `pwck` | 验证密码文件的完整性。 |
| `pwconv` | 根据 `passwd` 和可选的 `shadow` 创建 `shadow`。 |
| `pwd` | 显示当前目录。 |
| `python` | |

## Linux 命令 – Q

| 命令 | 说明 |
|---|---|
| `quota` | 显示用户或组的磁盘使用情况和空间限制。无参数时仅显示用户配额。 |
| `quotacheck` | 用于扫描文件系统的磁盘使用情况。 |
| `quotactl` | 修改磁盘配额。 |
| `quotaoff` | 禁止文件系统配额强制。 |
| `quotaon` | 启用文件系统配额强制。 |
| `quotastats` | 显示从内核收集的配额系统统计报告。 |

## Linux 命令 – R

| 命令 | 说明 |
| --- | --- |
| `raidstart` | 启动/停止 RAID 设备。 |
| `ram` | 用于以原始模式访问 RAM 磁盘的 RAM 设备。 |
| `ramsize` | 显示 RAM 磁盘的使用信息。 |
| `ranlib` | 为存档内容生成索引并存储在存档中。 |
| `rar` | 在 Linux 中创建和管理 RAR 文件。 |
| `rarpd` | 响应反向地址解析协议 (RARP) 请求。 |
| `rcp` | 远程复制命令，用于在远程计算机之间复制文件。 |
| `rdate` | 通过从远程机器获取信息来设置系统日期。 |
| `rdev` | 设置或查询 RAM 磁盘大小、镜像根设备或视频模式。 |
| `rdist` | 远程文件发布客户端，在多个主机上保持相同的文件副本。 |
| `rdistd` | 启动 `rdist` 服务器。 |
| `read` | 从文件描述符读取。 |
| `readarray` | 从文件中读取行到数组变量中。 |
| `readcd` | 读/写光盘。 |
| `readelf` | 显示有关 ELF（可执行和链接格式）文件的信息。 |
| `readlink` | 显示符号链接的值或规范名称。 |

# Linux 命令终极 A 到 Z 列表

| `readonly` | 将函数和变量标记为只读。 |
| `reboot` | 重启机器。 |
| `reject` | 接受/拒绝发送到指定目的地的打印作业。 |
| `remsync` | 通过电子邮件同步远程文件。 |
| `rename` | 重命名一个或多个文件。 |
| `renice` | 更改活动进程的优先级。 |
| `repquota` | 报告指定文件系统的磁盘情况和配额。 |
| `reset` | 初始化终端。 |
| `resize2fs` | 用于调整 ext2/ext3/ext4 文件系统的大小。 |
| `restore` | 从使用 `dump` 创建的备份恢复文件。 |
| `return` | 退出 shell 函数。 |
| `rev` | 显示文件内容，反转每行字符的顺序。 |
| `reexec` | `exec` 服务器的远程执行客户端。 |
| `rexecd` | 远程执行服务器。 |
| `richtext` | 在 ASCII 终端上查看 "richt"。 |
| `rlogin` | 用于连接本地主机系统与远程主机。 |
| `rlogind` | 作为 `rlogin` 的服务器。它方便基于信任主机的特权数字进行远程登录和验证。 |
| `rm` | 默认删除指定的文件和目录。 |
| `mail` | 处理通过 `uucp` 接收的远程邮件。 |
| `rmdir` | 用于删除空目录。 |

# Linux 命令终极 A Z 列表

| `rmmod` | 从 Linux 内核移除模块的程序。 |
| `rndc` | 域名服务器控制实用。通过 TCP 连接向 BIND DNS 服务器发送命令。 |
| `rootflags` | 显示/设置内核镜像的标志。 |
| `route` | 显示/更改 IP 路由表。 |
| `routed` | 守护进程，在启动时调用，用于管理互联网路由表。 |
| `rpcgen` | RPC 协议编译器。解析用 RPC 语言编写的文件。 |
| `rpcinfo` | 显示 RPC 信息。向 RPC 服务器发起 RPC 调用并报告结果。 |
| `rpm` | Linux 发行版的包管理器。最初为 RedHat Linux 开发。 |
| `rsh` | 远程 shell。连接到指定主机并执行命令。 |
| `rshd` | 作为 `rsh` 和 `rcp` 命令服务器的守护进程。 |
| `rsync` | 用于远程和本地复制文件的多功能工具。 |
| `runlevel` | 显示之前的和当前的 SysV 运行级别。 |
| `rup` | 远程显示。显示本地网络上所有或指定主机的当前系统状态。 |
| `runtime` | 显示本地网络机器运行时间和登录详情。 |
| `users` | 显示登录到主机或本地网络上所有机器的用户列表。 |
| `usersd` | `usersd` 守护进程作为服务器，响应 `users` 命令的查询。 |
| `r` | 向本地网络上的所有用户发送消息。 |
| `rwho` | 报告谁登录了本地网络上的主机。 |
| `rhod` | 作为 `rwho` 和 `route` 命令的服务器。 |

## Linux 命令 – S

| 命令 | 说明 |
|---|---|
| `sane-find-scanner` | 寻找 SCSI 和 USB 扫描仪并确定它们的设备文件。 |
| `scanadf` | 从带有自动文档馈器 (ADF) 的扫描仪上检索多个图像。 |
| `scanimage` | 从图像采集设备（扫描仪或相机）读取图像并以 PNM (Portable AnyMap) 格式显示在标准输出。 |
| `scp` | 使用 SSH 安全地在网络主机之间复制文件。 |
| `screen` | 窗口管理器，通过 ANSI/VT100 终端仿真启用多个伪终端。 |
| `script` | 用于对终端会话期间屏幕显示的所有内容制作记录。 |
| `sdiff` | 并排显示两个文件并突出显示差异。 |

# Linux 命令终极 A 到 Z 列表

| `sed` | 用于过滤和转换文本的流编辑器（来自文件或管道输入）。 |
| `select` | 同步 I/O 多路用 |
| `sendmail` | 它是邮件路由器或 MTA（邮件传输代理）。`sendmail` 支持使用必要的协议向一个或多个接收者发送邮件。 |
| `sensors` | 显示所有传感器芯片的当前读数。 |
| `seq` | 显示数字的序列。 |
| `set` | 用于操作 shell 变量。 |
| `setfdrm` | 设置用户提供的磁盘扇区。 |
| `keycodes` | 扫描码表。 |
| `setleds` | 显示 LED 设置。 |
| `metamode` | 设置元模式。 |
| `setquota` | 为用户和组设置配额。 |
| `setsid` | 在新会话运行程序。 |
| `setterm` | 设置终端属性。 |
| `sftp` | 安全文件传输程序。 |
| `sh` | 命令解释器（shell）。 |
| `sha1sum` | 计算并检查 160 位 SHA1 校验和。 |

# Linux 命令终极 A To Z 列表

| `shift` | 位置参数。 |
| `shellopt` | shell 选项。 |
| `showkey` | 检查的代码并以可打印形式显示。 |
| `showmount` | 显示 NFS 服务器挂载信息。 |
| `shred` | 覆盖文件内容（可选删除），使其难以恢复。 |
| `shutdown` | 关机。 |
| `size` | 列出指定文件的大小。 |
| `kill` | 向进程发送信号。 |
| `slabtop` | 实时显示内核缓存信息。 |
| `slattach` | 将网络接口附加到串口。 |
| `sleep` | 暂停执行指定的时间（秒）。 |
| `slocate` | 通过搜索文件名数据库显示匹配。 |
| `snice` | 重置进程优先级。 |
| `sort` | 文件行排序。 |
| `source` | 从文件运行命令。 |
| `split` | 将文件分成固定大小的部分。 |
| `ss` | 显示套接统计，类似于 `netstat`。 |
| `ssh` | 用于登录远程机器的 SSH 客户端。提供主机间的加密通信。 |

# Linux 命令终极 A To Z 列表

| `ssh-add` | 将私钥身份添加到代理。 |
| `ssh-agent` | 持用于公钥认证的私钥。 |
| `ssh-keygen` | 生成、管理、转换 ssh 密钥。 |
| `ssh-keyscan` | 收集 ssh 公钥。 |
| `sshd` | ssh 程序的服务器。 |
| `stat` | 显示文件或文件系统状态。 |
| `statd` | 监听来自其他主机的重启通知，并管理本地系统重启时通知的主机列表。 |
| `strace` | 跟踪系统调用和信号。 |
| `strfile` | 创建存储字符串的随机访问文件。 |
| `strings` | 搜索指定文件并打印任何至少四个字符且后跟不可打印字符的可打印字符串。 |
| `strip` | 从对象文件中删除符号。 |
| `stty` | 修改并打印终端行设置。 |
| `su` | 更改用户 ID 或变为超级用户。 |
| `sudo` | 以超级用户身份执行命令。 |
| `sum` | 计算文件的校验和并计数。 |
| `suspend` | 暂停当前 shell 的执行。 |
| `swapoff` | 禁用分页和交换设备。 |
| `swapon` | 启用分页和交换设备。 |
| `symlink` | 为文件创建符号链接。 |

# Linux 命令终极 A 到 Z 列表

| `sync` | 将缓存的写入同步到持久性存储器。 |
| `sysctl` | 在运行时配置内核参数。 |
| `syslogd` | Linux 系统日志工具。提供 `syslogd` 和 `klogd` 功能。 |
| `syslog` | 读取系统消息并将其记录到控制台和日志文件中。 |

## Linux 命令 – T

| 命令 | 描述 |
| --- | --- |
| `tac` | 反序连接并打印文件。`cat` 命令的相反命令。 |
| `tail` | 显示每个指定文件的最后 10 行。 |
| `tailf` | 跟踪日志文件的增长。（已弃用的命令） |
| `talk` | 一种双向的面向屏幕的通信工具，允许两个用户同时交换消息。 |
| `talkd` | 用于 `talk` 的远程用户通信服务器。 |
| `tar` | GNU 版本的 `tar` 归档工具。用于从单个存档中存储和提取多个文件。 |
| `taskset` | 设置/检索进程的 CPU 亲和性。 |
| `tcpcd` | 互联网服务的访问控制工具。 |
| `tcpdump` | 倾储网络上的流量。显示网络接口上匹配布尔表达式的数据包内容描述。 |
| `tcpslice` | 提取 `tcpdump` 文件的片段或合并它们。 |
| `tee` | 从标准输入读取并写入到标准输出和文件。 |
| `telinit` | 更改 SysV 运行级别。 |
| `telnet` | Telnet 协议用户界面。用于 `telnet` 与另一个主机交互。 |
| `telnetd` | telnet 协议的服务器。 |
| `test` | 检查文件类型并比较值。 |
| `tftp` | 互联网 TFTP（简单文件传输协议）的用户界面。 |
| `tftpd` | TFTP 服务器。 |
| `time` | 运行程序并总结系统资源使用。 |
| `timeout` | 带时间限制执行命令。 |
| `times` | 显示 shell 及其子进程的累计用户和系统时间。 |
| `tload` | 向指定的 `tty` 显示当前系统负载平均图表。 |
| `tmpwatch` | 递归删除指定时间内未被访问的文件和目录。 |
| `top` | 显示系统上运行进程的实时视图。 |
| `touch` | 更改文件的访问和修改时间。 |
| `tput` | 修改终端相关的属性、颜色等。 |
| `tr` | 从标准输入翻译、压缩或删除字符并显示在标准输出。 |
| `tracepath` | 追踪到网络主机的路径，并发现此路径上的 MTU（最大传输单元）。 |
| `traceroute` | 追踪数据包到达网络主机经过的路由。 |
| `trap` | `trap` 函数响应硬件信号。它定义并创建在 shell 接收到信号时运行的处理器。 |
| `proff` | `groff` 文本格式系统的 `proff` 处理器。 |
| `TRUE` | 以表示成功的状态码退出。 |
| `tset` | 初始化终端。 |
| `tsort` | 执行拓扑排序。 |
| `tty` | 显示连接到标准输入的终端文件名。 |
| `tune2fs` | 调整 ext2/ext3/ext4 文件系统上的可调文件系统参数。 |
| `tunelp` | 为行打印设备设置各种参数。 |
| `type` | 为命令类型编写描述。 |

## Linux 命令 – U

| 命令 | 描述 |
|---|---|
| `ul` | 文字下划线。 |
| `ulimit` | 获取并设置调用进程的用户限制。 |
| `umask` | 设置文件创建掩码。 |
| `umount` | 卸载指定的文件系统。 |
| `unalias` | 指定名称的别名定义。 |
| `unname` | 显示系统信息。 |
| `uncompress` | 解压缩用 `compress` 命令压缩的文件。 |
| `unexpand` | 将指定文件的空格转换为制表符。 |
| `unicode_start` | 将键盘和控制台设置为 Unicode 模式。 |
| `unicode_stop` | 将键盘和控制台退出 Unicode 模式。 |
| `uniq` | 报告或忽略重复行。 |
| `units` | 将单位从一个标量转换为另一个标量。 |
| `unrar` | 从 RAR 存档中提取文件。 |
| `unset` | 移除变量或函数名。 |
| `unshar` | 解包 shell 存档脚本。 |
| `until` | 继续执行命令直到给定条件为真。 |
| `uptime` | 系统运行了多久。 |
| `useradd` | 创建新用户或更新默认信息。 |
| `userdel` | 删除用户账户及相关文件。 |
| `usermod` | 修改用户账户。 |
| `users` | 显示机器上活动用户的列表。 |
| `usleep` | 以微秒间隔挂起执行。 |
| `uudcode` | 解码二进制文件。 |
| `uuencode` | 编码二进制文件。 |
| `uuidgen` | 创建一个新的 UUID（通用唯一标识符）表。 |

## Linux 命令 – V

| 命令 | 描述 |
|---|---|
| `yacc` | GNU 项目解析生成器。 |
| `yes` | 重复输出指定的字符串直到被杀死。 |
| `ybind` | 帮助客户端进程连接到 NIS 服务器的守护进程。 |
| `ypcat` | 显示指定参数的 NIS map（数据库）。 |
| `vdir` | 类似于 `ls -l`，列出目录内容。 |
| `vi` | 文本编辑器。 |
| `vidmode` | 设置视频模式。作为 `vi` 的替代方案，显示 man 页面。 |
| `vim` | 改进的 `vi`，一种基于文本的编辑器。 |
| `vmstat` | 显示进程、内存、分页、块 IO、磁盘和 CPU 活动的信息。 |
| `volname` | 返回 ISO-960 卷名。 |

## Linux 命令 – W

| 命令 | 描述 |
|---|---|
| `w` | 显示登录的用户及其正在做什么。 |
| `wait` | 等待指定的进程 ID 终止。 |
| `wall` | 在所有终端显示消息。 |
| `warnquota` | 向超过磁盘配额的用户发送邮件。 |
| `watch` | 重复运行命令直到中断并显示其输出和错误。 |
| `wc` | 计算每个文件的换行符、单词和字节数。 |
| `wget` | 非交互式文件下载工具。 |
| `whatis` | 显示单行手册页描述。 |
| `whereis` | 定位命令的二进制、源和帮助页文件。 |
| `which` | 对于给定命令列出将执行的文件路径。 |
| `while` | 条件执行命令（`while` 循环）。 |



| `who` | 显示登录的用户。 |

| `whoami` | 显示当前有效用户 ID 的用户名。 |

| `whois` | 在 WHOIS 数据库中查找对象 |

| `write` | 在其他用户的终端上显示消息。 |

## Linux 命令 – X

| 命令 | 描述 |
|---|---|
| `xargs` | 使用初始参数运行命令，然后从标准输入读取剩余参数。 |
| `xdg-open` | 用于用用户喜欢的应用程序打开文件或 URL。 |
| `xinetd` | 扩展互联网服务守护。工作类似于 `inetd`。 |
| `xz` | 压缩/解压缩 `.xz` 和 `.lzma` 文件。 |

## Linux 命令 – Y

| 命令 | 描述 |
|---|---|
| | |
| `yacc` | GNU 项目解析生成器。 |
| `yes` | 重复输出指定的字符串直到被杀死 |
| `ybind` | 帮助客户端进程连接到 NIS 服务器的守护进程。 |
| `ypcat` | 显示指定 `MapName` 参数的 NIS map（数据库）。 |
| `ypinit` | 在 NIS 服务器上设置 NIS maps。 |
| `ypmatch` | 显示 NIS map 中指定键的值。 |
| `yppasswd` | 更改 NIS 登录密码。 |
| `ypasswdd` | 作为 `yppasswd` 命令的服务器接收并执行请求。 |
| `ypoll` | 显示 NIS 服务器上当前使用的 NIS map 编号或版本。 |
| `ypush` | 强制从属 NIS 服务器复制更新的 NIS maps。 |
| `yps`erv` | 系统启动时激活的守护进程。它在本地 NIS maps 中查找信息。 |
| `ypset` | 将客户端（运行 `ypbind`）指向指定的（运行 `yps`erv`）。 |
| `ytest` | 调用各种函数来检查 NIS 服务的配置。 |
| `ypwhich` | 显示给定 map 的 NIS 服务器或主服务器的主机。 |
| `ypxfr` | 将 NIS map 从服务器传输到本地主机。 |

## Linux 命令 – Z

| 命令 | 描述 |
|---|---|
| `zcat` | 用于压缩/解压文件。类似于 `gzip` |
| `zcmp` | 比较压缩文件。 |
| `zdiff` | 逐行比较压缩文件。 |
| `zdump` | 显示所提时区的时间。 |
| `zforce` | 为所有 gzipped 文件添加 `.gz` 扩展名。 |
| `zgrep` | 对压缩文件执行 `grep` 搜索。 |
| `zic` | 使用指定的输入文件创建时间转换信息文件。 |
| `zip` | 文件压缩和打包工具。 |
| `zless` | 在终端上逐屏地显示压缩文件的信息（使用 `less` 命令）。 |
| `zmore` | 在终端上逐页页地显示压缩文件的输出（使用 `more` 命令）。 |
| `znew` | 将 `.z` 文件重新压缩为 `.gz` 文件。 |

以上就是不同 Linux 命令的汇编。我希望这些 A-Z 的 Linux 命令能在某些方面对你有所帮助。我花费了几周时间从各种来源收集并测试了这些 Linux 命令。如果你发现某些命令缺失或存在差异，请提供你的宝贵反馈，帮助我完善整个列表。我期待你的反馈。

> 延伸阅读：`Windows` `CMD` 命令 A 到 Z 终列表

## 你需要知道的

Aditya Tiwari

## Aditya Tiwari

Aditya 喜欢涵盖与微软、`Windows` 10 以及有趣的配件相关的话题。当他不工作时，你会发现他正在 YouTube 上疯狂狂刷随机视频（在他已经在 Netflix 上浪费了一个小时寻找好剧之后）。通过以下方式联系他：

[email protected]

f youtube
