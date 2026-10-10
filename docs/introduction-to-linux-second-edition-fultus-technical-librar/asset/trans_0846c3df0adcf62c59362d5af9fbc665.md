
## A.1 推荐书籍

- 蒂姆·豪斯（Tim Howes）等人合著的《理解与部署 LDAP 目录服务》，出版社：Sams，ISBN 0672323168
- 布莱恩·科斯塔利斯（Brian Costales）和埃里克·奥尔曼（Eric Allman）合著的《Sendmail》，出版社：O'Reilly UK，ISBN 1565922220
- 杰夫·穆利根（Geoff Mulligan）著的《清除垃圾邮件：电子邮件处理与过滤》，出版社：艾迪生·韦斯利出版公司（Addison Wesley Publishing Company），ISBN 0201379570
- 黛安娜·穆雷特（Dianna Mullet）和凯文·穆雷特（Kevin Mullet）合著的《管理 IMAP》，出版社：O'Reilly UK，ISBN 059600012X

## A.2 有用网站

### A.2.1 通用信息

- Linux 文档项目：<http://www.lfdp.org/> 所有文档、man 手册页、HOWTO 指南、常见问题解答（FAQs）
- LinuxQuestions.org <http://www.linuxquestions.org/>：论坛、下载、文档及其他更多资源
- Linux 版谷歌搜索 <http://www.google.com/linux>：专用搜索引擎
- Google Groups <http://groups.google.com/>：所有新闻组帖子的存档，包括 comp.os.linux 层级
- Slashdot <http://slashdot.org/>：每日新闻
- O'Reilly <http://www.oreilly.com/>：关于 Linux 系统与网络管理、Perl、Java 等方面的书籍……
- POSIX <http://www.posix.com/posix.html>：标准规范
- Linux HQ <http://www.linuxhq.com/>：维护了各种版本 Linux 内核的源代码、补丁和文档的完整数据库。

### A.2.2 特定架构参考

- AlphaLinux <http://www.alphalinux.org/>：基于 Alpha 架构的 Linux（例如 Digital Workstation）
- Linux-MIPS <http://www.linux-mips.org/>：基于 MIPS 架构的 Linux（例如 SGI Indy）
- 行路中的 Linux <http://tldp.org/LDP/Mobile-Guide/html/index.html>：在笔记本电脑、PDA、移动电话上安装和运行 Linux 的具体指南。包含各种型号的配置示例文件。
- MkLinux <http://www.mklinux.org/>：在苹果 Mac 上运行的 Linux

### A.2.3 发行版

- Fedora 项目 <http://fedora.redhat.com/>：由 RedHat 赞助的社区操作系统项目。
- Mandriva <http://www.mandriva.com/>
- Ubuntu <http://www.ubuntu.com/>
- Debian <http://www.debian.org/>
- TurboLinux <http://www.turbolinux.com/>
- Slackware <http://www.slackware.com/>
- SUSE <http://www.suse.de/>
- LinuxISO <http://www.linuxiso.org/>：所有发行版的 CD 镜像。
- Knoppix <http://www.knoppix.org/>：可以直接从 CD 运行的发行版，无需安装即可使用。
- DistroWatch.com <http://www.distrowatch.com/>：寻找符合你风格偏好的 Linux 发行版。
- ...

### A.2.4 软件

- Freshmeat <http://freshmeat.net/>：新软件、软件存档
- OpenSSH <http://www.openssh.org/>：安全 Shell（Secure SHell）站点
- OpenOffice <http://www.openoffice.org/>：兼容 Microsoft Office 的办公套件
- KDE <http://www.kde.org/>：K 桌面环境站点
- GNU <http://www.gnu.org/>：GNU 项目及 GNU 软件
- Gnome <http://www.gnome.org/>：官方 Gnome 站点
- RPM Find <http://www.rpmfind.net/>：所有 RPM 软件包
- Samba <http://www.samba.org/>：Microsoft Windows 文件和打印服务
- OpenLDAP 项目主页 <http://www.openldap.org/>：OpenLDAP 服务器/客户端/工具，FAQ 及其他文档。
- Sendmail 主页 <http://www.sendmail.org/>：对 Sendmail 功能进行详尽的技术讨论，包含配置示例。
- Netfilter <http://netfilter.samba.org/>：包含关于 iptables 的各类信息：HOWTO、FAQ、指南等……
- GIMP 官方网站 <http://www.gimp.org/>：关于 GNU 图像操作程序（GNU Image Manipulation Program）的所有信息。
- SourceForge.net <http://sourceforge.net/>：开源软件开发站点。
- vim 主页 <http://www.vim.org/>

# 附录 B
## DOS 与 Linux 命令

在本附录中，我们将 DOS 命令与其等效的 Linux 命令进行了匹配。

作为给具有 Windows 背景的新用户的一种额外导航辅助手段，下表列出了 MS-DOS 命令及其对应的 Linux 命令。请注意，Linux 命令通常有许多选项。请阅读该命令的 Info 文档或 man 手册页以了解更多信息。

| DOS 命令 | Linux 命令 |
| :--- | :--- |
| <command> /? | man <command> |
| cd | cd |
| chdir | pwd |
| cls | clear |
| copy | cp |
| date | date |
| del | rm |
| dir | ls |
| echo | echo |
| edit | vim（或其他编辑器） |
| exit | exit |
| fc | diff |
| find | grep |
| format | mke2fs 或 mformat |
| mem | free |
| mkdir | mkdir |
| more | more 或 even less |
| move | mv |
| ren | mv |
| time | date |

表 11.2. DOS/Linux 命令概览

# 附录 C
## Shell 特性

本文档概述了常见的 shell 特性（在所有 shell 变体中相同）以及不同的 shell 特性（特定于特定 shell 的特性）。

### C.1 通用特性

以下特性是所有 shell 的标准配置。请注意，stop、suspend、jobs、bg 和 fg 命令仅在支持任务控制（job control）的系统上可用。

| 命令 | 含义 |
|---|---|
| > | 重定向输出 |
| >> | 追加到文件 |
| < | 重定向输入 |
| << | “Here” 文档（重定向输入） |
| | | 管道输出 |
| & | 在后台运行进程。 |
| ; | 在同一行上分隔命令 |
| * | 匹配文件名中的任意字符 |
| ? | 匹配文件名中的单个字符 |
| [1] | 匹配包含在括号内的任意字符 |
| ( ) | 在子 shell 中执行 |
| ' ' | 替换括号内命令的输出 |
| " " | 部分引用（允许变量和命令扩展） |
| ' ' | 完全引用（不扩展） |
| \ | 引用后一个字符 |
| $var | 使用变量的值 |
| `$$` | 进程 ID |
| `$0` | 命令名称 |
| `$n` | 第 n 个参数（n 从 0 到 9） |
| `$*` | 所有参数作为一个简单的单词 |
| `#` | 注释开始 |
| `bg` | 后台执行 |
| `break` | 跳出循环语句 |
| `cd` | 更改目录 |
| `continue` | 继续程序循环 |
| `echo` | 显示输出 |
| `eval` | 计算参数 |
| `exec` | 执行一个新的 shell |
| `fg` | 前台执行 |
| `jobs` | 显示活动任务 |
| `kill` | 终止运行中的任务 |
| `newgrp` | 更改到新的组 |
| `shift` | 移位位置参数 |
| `stop` | 挂起后台任务 |
| `suspend` | 挂起前台任务 |
| `time` | 对命令计时 |
| `umask` | 设置或列出文件权限 |
| `unset` | 擦除变量或函数定义 |
| `wait` | 等待后台任务完成 |

表 C. 1. 通用 Shell 特性

### C.2 差异化特性

下表显示了标准 shell (sh)、Bourne Again Shell (bash)、Korn shell (ksh) 和 C shell (csh) 之间的主要差异。

#### Shell 兼容性

由于 Bourne Again **Shell** 是 sh 的超集，所有 sh 命令在 **bash** 中也将有效 - 反之则不成立。**bash** 拥有更多自身的特性，并且如下表所示，还引入了许多其他 shell 的特性。

由于 Turbo C shell 是 csh 的超集，所有 csh 命令在 tesh 中都有效，但反之则不成立。

| sh | bash | ksh | csh | 含义/操作 |
|---|---|---|---|---|
| $ | $ | $ | % | 默认用户提示符 |
| > | > | > | >! | 强制重定向 |
| > file 2>&1 | &> file 或 > file 2>&1 | > file 2>&1 | >& file | 将 stdout 和 stderr 重定向到文件 |
| | { } | | { } | 展开列表中的元素 |
| `command` | `command` 或 $(command) | $(command) | `command` | 替换括号内 **command** 的输出 |
| $HOME | $HOME | $HOME | $home | 主目录 |
| | ~ | ~ | ~ | 主目录符号 |
| | --, -, dirs | --, - | = -, =N | 访问目录堆栈 |
| var=value | VAR=value | var=value | set var=value | 变量赋值 |
| export var | export VAR=value | export var=val | setenv var val | 设置环境变量 |
| | ${nnnn} | ${nn} | | 可以引用超过 9 个参数 |
| "$@" | "$@" | "$@" | | 所有参数作为单独的单词 |
| $# | $# | $# | $argv | 参数数量 |
| $? | $? | $? | $status | 最近执行的命令的退出状态 |
| $$ | $$ | $$ | | 最近后台化的进程的 PID |
| `$-` | `$-` | `$-` | | 当前选项 |
| `. file` | source file 或 . file | . file | source file | 读取文件中的命令 |
| | `alias x='y'` | `alias x=y` | `alias x y` | 名称 x 代表命令 y |
| case | case | case | switch 或 case | 选择备选方案 |
| done | done | done | end | 结束循环语句 |
| esac | esac | esac | endsw | 结束 **case** 或 **switch** |
| `exit n` | `exit n` | `exit n` | `exit (expr)` | 以特定状态退出 |
| for/do | for/do | for/do | foreach | 循环遍历变量 |
| | `set -f` `set -o nulglob` `dotglob` `nocaseglob` `noglob` | | `noglob` | 在文件名生成时忽略替换字符 |
| hash | hash | `alias -t` | `hashstat` | 显示已缓存的命令（跟踪的别名） |
| `hash cm ds` | `hash cm ds` | `alias -t cm ds` | `rehash` | 记住命令位置 |
| `hash -r` | `hash -r` | | `unhash` | 忘记命令位置 |
| | history | history | history | 列出以前的命令 |
| | ArrowUp+Enter 或 `!!` | | `!!` | 重做上一个命令 |
| | `!str` | `! str` | `!str` | 重做最后一个以 "str" 开头的命令 |
| | `!cmd:s/x/y/` | `! x=y cmd` | `!cmd:s/x/y/` | 在最近的以 "cmd" 开头的命令中用 "y" 替换 "x"，然后 |

