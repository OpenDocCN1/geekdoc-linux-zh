
## signore
参见 ignored。 (别名 ignored, sig_ignore)。

## sigmask
参见 blocked。 (别名 blocked, sig_block)。

## size
如果进程弄脏了所有可写页面并被换出，所需的交换空间的大致数量。此数字非常粗略！

## slice
如果已包含 systemd 支持，则显示进程所属的 slice 单元。

## spid
参见 lwp。 (别名 lwp, tid)。

## stackp
进程堆栈底部（起始）地址。

## start
命令启动的时间。如果进程启动于 24 小时以内，输出格式为 “HH:MM:SS”，否则为 “Mmmdd”（其中 Mmm 是三位数的月份名称）。另见 lstart, bsdstart, start_time 和 sti。

## start_time
进程的启动时间或日期。如果进程不是在调用 ps 的同一年启动，则只显示年份；如果不是在同一天启动，则显示 “MmmDD”；否则显示 “HH:MM”。另见 bsdstart, start, lstart 和 sti。

## stat
单字符进程状态。参见 PROCESS STATE CODES 部分了解不同值及其含义。如果您只想显示第一个字符，请另见 s 或 state。

## state
参见 s。 (别名)。

## suid
保存的用户 ID。 (别名 svuid)。

## supgid
补充组（如果有的话）的组 ID。参见 man 2 getgroups。

## supgrp
补充组（如果有的话）的组名称。参见 man 2 getgroups。

## suser
保存的用户名。如果可以获取且字段宽度允许，则显示文本形式的用户 ID，否则显示十进制表示。 (别名 suser)。

## svgid
参见 sgid。 (别名 sgid)。

## svuid
参见 suid。 (别名 suid)。

## sz
进程核心映像的物理页面大小。这包括文本、数据和堆栈空间。设备映射目前被排除在外；此行为可能会更改。参见 vsz 和 rss。

## tgid
代表任务所属线程组的数字 (别名 pid)。它是线程组组长的进程 ID。

## thcount
参见 nlwp。 (别名 nlwp)。进程拥有的内核线程数量。

## tid
代表可调度实体的唯一编号 (别名 lwp, spid)。此值也可能显示为：进程 ID (pid)；进程组 ID (pgrp)；会话组长的会话 ID (sid)；线程组组长的线程组 ID (tgid)；以及进程组组长的 tty 进程组 ID (tpgid)。

## time
累计 CPU 时间，格式为 "[DD-]HH:MM:SS"。 (别名 cputime)。

## tname
控制 tty（终端）。 (别名 tt, tty)。

## tpgid
进程连接到的 tty（终端）上前台进程组的 ID，如果进程未连接到 tty，则为 -1。

## trs
文本驻留集大小，即分配给可执行代码的物理内存量。

## tt
控制 tty（终端）。 (别名 tname, tty)。

## tty
控制 tty（终端）。 (别名 tname, tt)。

## ucmd
参见 comm。 (别名 comm, ucomm)。

## ucomm
参见 comm。 (别名 comm, ucmd)。

## uid
参见 euid。 (别名 euid)。

## uname
参见 euser。 (别名 euser, unamer)。

## unit
如果已包含 systemd 支持，则显示进程所属的单元。

## user
参见 euser。 (别名 euser, uname)。

## usern
描述进程所属命名空间的唯一 inode 号。参见 man 7 user_namespaces。

## utsn
描述进程所属命名空间的唯一 inode 号。参见 man 7 user_namespaces。

## uunit
如果已包含 systemd 支持，则显示进程所属的用户单元。

## vsize
参见 vsz。 (别名 vsz)。

## vsz
进程的虚拟内存大小，单位为 KiB（1024 字节）。设备映射目前被排除在外；此行为可能会更改。 (别名 vsize)。

## wchan
进程正在休眠的内核函数名称，如果进程正在运行则为 “-”，如果进程是多线程且 ps 未显示线程则为 “*”。

## ENVIRONMENT VARIABLES

以下环境变量可能会影响 ps：

- COLUMNS
  覆盖默认显示宽度。
- LINES
  覆盖默认显示高度。
- PS_PERSONALITY
  设置为 posix, old, linux, bsd, sun, digital... 之一（参见下文 PERSONALITY 部分）。
- CMD_ENV
  设置为 posix, old, linux, bsd, sun, digital... 之一（参见下文 PERSONALITY 部分）。
- I_WANT_A_BROKEN_PS
  强制使用过时的命令行解释。
- LC_TIME
  日期格式。
- PS_COLORS
  目前不支持。
- PS_FORMAT
  默认输出格式覆盖。您可以将其设置为 -o 选项使用的类型格式化字符串。DefSysV 和 DefBSD 值特别有用。
- PS_SYSMAP
  默认符号表 (System.map) 位置。
- PS_SYSTEM_MAP
  默认符号表 (System.map) 位置。
- POSIXLY_CORRECT
  不要找借口忽略不良的“特性”。
- POSIX2
  当设置为 “on” 时，其行为与 POSIXLY_CORRECT 相同。
- UNIX95
  不要找借口忽略不良的“特性”。
- _XPG
  取消 CMD_ENV=irix 的非标准行为。

通常，设置这些变量是一个坏主意。唯一的例外是 CMD_ENV 或 PS_PERSONALITY，在常规系统中可以将其设置为 Linux。如果没有该设置，ps 将遵循 Unix98 标准中无用且糟糕的部分。

## PERSONALITY

- 390 类似于 OS/390 OpenEdition ps
- aix 类似于 AIX ps
- bsd 类似于 FreeBSD ps（完全非标准）
- compaq 类似于 Digital Unix ps
- debian 类似于旧版 Debian ps
- digital 类似于 Tru64（曾为 DigitalUnix，曾为 OSF/1）ps
- gnu 类似于旧版 Debian ps
- hp 类似于 HP-UX ps
- hpux 类似于 HP-UX ps
- irix 类似于 Irix ps
- linux ****** 推荐 ******
- old 类似于原始 Linux ps（完全非标准）
- os390 类似于 OS/390 Open Edition ps
- posix 标准
- s390 类似于 OS/390 Open Edition ps
- sco 类似于 SCO ps
- sgi 类似于 Irix ps
- solaris2 类似于 Solaris 2+（SunOS 5）ps
- sunos4 类似于 SunOS 4（Solaris 1）ps（完全非标准）
- svr4 标准
- sysv 标准
- tru64 类似于 Tru64（曾为 Digital Unix，曾为 OSF/1）ps
- unix 标准
- unix95 标准
- unix98 标准

## SEE ALSO

(1), (1), (1), (5)。

## STANDARDS

此 ps 符合以下标准：

1. 单一 Unix 规范第 2 版
2. Open Group 技术标准基础规范，第 6 版
3. IEEE Std 1003.1, 2004 版
4. X/Open 系统接口扩展 [XSI]
5. ISO/IEC 9945:2003

## AUTHOR

ps 最初由 Branko Lankester 编写。Michael K. Johnson 对其进行了重大重写以使用 proc 文件系统，并在过程中更改了一些内容。Michael Shields 添加了 pid-list 功能。Charles Blake 添加了多级排序、dirent 风格的库、设备名称到数字的 mmaped 数据库、直接在 System.map 上进行的近似二进制搜索，以及许多代码和文档清理工作。David Mossberger-Tang 为 psupdate 编写了通用 BFD 支持。Albert Cahalan 重写了 ps 以全面支持 Unix98 和 BSD，并包含一些针对过时和外来的语法的丑陋补丁。

请将 bug 报告发送至 bug-utils@gnu.org。无需订阅，也不建议订阅。

## PS2ASCII

### NAME

ps2ascii - 从 PostScript 或 PDF 到 ASCII 的 Ghostscript 转换器

### SYNOPSIS

ps2ascii [ input.ps [ output.txt ] ] ps2ascii input.pdf [ output.txt ]

### DESCRIPTION

ps2ascii 使用 gs 从 PostScript (tm) 或 Adobe Portable Document Format (PDF) 文件中提取 ASCII 文本。如果未指定命令行中的文件，gs 从标准输入读取；但 PDF 输入应来自明确命名的文件，而不是标准输入。如果未指定输出文件，ASCII 文本将写入标准输出。

ps2ascii 不查看字体编码，而且处理字距调整的效果不太好，因此对于 PostScript（目前不包括 PDF），您可能会考虑使用 pstops（见下文）。

