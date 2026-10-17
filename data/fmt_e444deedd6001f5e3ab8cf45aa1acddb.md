
| 代码 | 标题 |
|---|---|
| %cpu | %CPU |
| %mem | %MEM |
| alarm | ALARM |
| args | COMMAND |
| blocked | BLOCKED |
| bsdstart | START |
| bsdtime | TIME |
| c | C |
| caught | CAUGHT |
| cmd | CMD |
| comm | COMMAND |
| command | COMMAND |
| cputime | TIME |
| drs | DRS |
| dsiz | DSIZ |
| egid | EGID |
| egroup | EGROUP |
| eip | EIP |
| esp | ESP |
| etime | ELAPSED |
| euid | EUID |
| euser | EUSER |
| f | F |
| fgid | FGID |
| fgroup | FGROUP |
| flag | F |
| flags | F |
| fname | COMMAND |
| fsgid | FSGID |
| fsgroup | FSGROUP |
| fsuid | FSUID |
| fsuser | FSUSER |
| fuid | FUID |
| fuser | FUSER |
| gid | GID |
| group | GROUP |
| ignored | IGNORED |
| intpri | PRI |
| lim | LIM |
| longtname | TTY |
| lstart | STARTED |
| m_drs | DRS |
| m_trs | TRS |
| maj_flt | MAJFLT |
| majflt | MAJFLT |
| min_flt | MINFLT |
| minflt | MINFLT |
| ni | NI |
| nice | NI |
| nwchan | WCHAN |
| opri | PRI |
| pagein | PAGEIN |
| pcpu | %CPU |
| pending | PENDING |

| 字段 | 格式 |
|---|---|
| `pgid` | `PGID` |
| `pgrp` | `PGRP` |
| `pid` | `PID` |
| `pmem` | `%MEM` |
| `ppid` | `PPID` |
| `pri` | `PRI` |
| `rgid` | `RGID` |
| `rgroup` | `RGROUP` |
| `rss` | `RSS` |
| `rssize` | `RSS` |
| `rsz` | `RSZ` |
| `ruid` | `RUID` |
| `ruser` | `RUSER` |
| `s` | `S` |
| `sess` | `SESS` |
| `session` | `SESS` |
| `sgi_p` | `P` |
| `sgi_rss` | `RSS` |
| `sgid` | `SGID` |
| `sgroup` | `SGROUP` |
| `sid` | `SID` |
| `sig` | `PENDING` |
| `sig_block` | `BLOCKED` |
| `sig_catch` | `CATCHED` |
| `sig_ignore` | `IGNORED` |
| `sig_pend` | `SIGNAL` |
| `sigcatch` | `CAUGHT` |
| `signore` | `IGNORED` |
| `sigmask` | `BLOCKED` |
| `stack` | `STACK` |
| `start` | `STARTED` |
| `start_stack` | `STACKP` |
| `start_time` | `START` |
| `stat` | `STAT` |
| `state` | `S` |
| `stime` | `STIME` |
| `suid` | `SUID` |
| `suser` | `SUSER` |
| `svgid` | `SVGID` |
| `svgroup` | `SVGROUP` |
| `svuid` | `SVUID` |
| `svuser` | `SVUSER` |
| `sz` | `SZ` |
| `time` | `TIME` |
| `timeout` | `TMOUT` |
| `tmout` | `TMOUT` |
| `tname` | `TTY` |
| `tpgid` | `TPGID` |
| `trs` | `TRS` |
| `trss` | `TRSS` |
| `tsiz` | `TSIZ` |
| `tt` | `TT` |
| `tty` | `TT` |
| `tty4` | `TTY` |
| `tty8` | `TTY` |
| `ucomm` | `COMMAND` |
| `uid` | `UID` |
| `uid_hack` | `UID` |
| `uname` | `USER` |
| `user` | `USER` |
| `vsize` | `VSZ` |
| `vsz` | `VSZ` |
| `wchan` | `WCHAN` |

#### 环境变量

以下环境变量可能会影响`ps`：

| 环境变量 | 描述 |
|---|---|
| `COLUMNS` | 覆盖默认显示宽度 |
| `LINES` | 覆盖默认显示高度 |
| `PS_PERSONALITY` | 设置为posix、old、linux、bsd、sun、digital之一 |
| `CMD_ENV` | 设置为posix、old、linux、bsd、sun、digital之一 |
| `I_WANT_A_BROKEN_PS` | 强制使用过时的命令行解释方式 |
| `LC_TIME` | 日期格式 |
| `PS_FORMAT` | 覆盖默认输出格式 |
| `PS_SYSMAP` | 默认名称列表（System.map）的位置 |
| `PS_SYSTEM_MAP` | 默认名称列表（System.map）的位置 |
| `POSIXLY_CORRECT` | 不要为忽略不良特性寻找借口 |
| `UNIX95` | 不要为忽略不良特性寻找借口 |
| `_XPG` | 取消`CMD_ENV=irix`的非标准行为 |

一般来说，设置这些变量不是一个好主意。两个例外是`CMD_ENV`（或`PS_PERSONALITY`），用于设置所需的默认风格；以及`POSIXLY_CORRECT`（或`UNIX95`），为符合UNIX98标准应予以设置。

| PS_PERSONALITY | 描述 |
|---|---|
| `none` | “做正确的事” |
| `aix` | 类似AIX ps |
| `bsd` | 类似FreeBSD ps |
| `compaq` | 类似Digital UNIX ps |
| `debian` | 类似旧版Debian ps |
| `digital` | 类似Digital UNIX ps |
| `gnu` | 类似旧版Debian ps |
| `hp` | 类似HP-UX ps |
| `hpux` | 类似HP-UX ps |
| `irix` | 类似Irix ps |
| `linux` | 仅为方便而偏离POSIX98 |
| `old` | 类似原始Linux ps |
| `posix` | 标准 |
| `sco` | 类似SCO ps |
| `sgi` | 类似Irix ps |
| `sun` | 类似SunOS 4 ps |
| `sunos` | 类似SunOS 4 ps |
| `sysv` | 标准 |
| `unix` | 标准 |
| `unix95` | 标准 |
| `unix98` | 标准 |

##### 示例

使用标准语法查看系统上的每个进程：

- `ps -e`

使用BSD语法查看系统上的每个进程：

- `ps ax`

查看除root（真实ID和有效ID）之外的所有进程：

- `ps -U root -u root`

以用户自定义格式查看所有进程：

- `ps -eo pid,tt,user,pmem,tmout,f,wchan`

使用AIX字段描述符的另类显示：

- `ps -o '%u : %U : %p : %P : %a'`

仅输出syslogd的进程ID：

- `ps -C syslogd -o pid=`

##### 另请参阅

`top(1)` `pstree(1)` `proc(5)`

#### 标准

此`ps`可设置为符合单一UNIX规范版本2。

#### 作者

`ps`最初由Branko Lankester编写。 <lankeste@fwi.uva.nl>

Michael K. Johnson <johnsonm@redhat.com>对其进行了重大重写，以使用proc文件系统，并在过程中更改了一些内容。

Michael Shields <shields@msrl.com>添加了pid-list功能。

Charles Blake <cblake@bbn.com>添加了多级排序、dirent风格库、设备名称到编号的映射数据库、直接在System.map上进行近似二分搜索，以及许多代码和文档的清理工作。

David Mosberger-Tang为psupdate编写了通用BFD支持。

Albert Cahalan <acahalan@cs.uml.edu>重写了`ps`，以全面支持UNIX98和BSD，并针对过时和外部语法进行了一些不优雅的临时处理。

Michael K. Johnson <johnsonm@redhat.com>是当前的维护者。

请将缺陷报告发送至 <procps-bugs@redhat.com>。

#### PWD

##### 名称

`pwd` — 输出当前/工作目录的名称。

##### 概要

```
