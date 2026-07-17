# FreeBSD 101 技巧指南



![](img/cover_image.jpg)


# 介绍

# FreeBSD-101-技巧

一个 FreeBSD 技巧集。

## 项目主页

[`github.com/NanXiao/FreeBSD-101-Hacks`](https://github.com/NanXiao/FreeBSD-101-Hacks)

## 获取系统版本

## 获取系统版本

`FreeBSD` 有 `2` 个版本：内核（kernel）和用户态空间（userland）。使用 `freebsd-version -ku` 可以同时输出这两个版本：

```
### freebsd-version -uk
10.3-RELEASE-p4
10.3-RELEASE-p5
```

第一个是内核版本信息。你可以看到内核和用户态的版本都是 `10.3`，但内核补丁级别是 `p4`，而用户态是 `p5`。这是因为在某些情况下，只有用户态需要补丁而内核不需要，因此内核补丁级别不会改变。如果没有使用该选项，`freebsd-version` 仅打印用户态版本：

```
### freebsd-version
10.3-RELEASE-p5
```

`uname -r` 命令也会输出内核版本：

```
### uname -r
10.3-RELEASE-p4
```

参考自：

[为什么“freebsd-version”和“freebsd-version -k”的输出不同？](http://stackoverflow.com/questions/3780013/why-the-outputs-of-freebsd-version-and-freebsd-version-k-are-different)。

## 通过 SSH 启用 root 登录

## 通过 SSH 启用 root 登录

默认情况下，`FreeBSD` 不允许 `root` 用户通过 `SSH` 登录，要启用它，你需要修改 `SSH` 守护进程文件（`/etc/sshd_config`）：

找到以下项：

```
PermitRootLogin no
```

修改为：

```
PermitRootLogin yes
```

重启服务：

```bash
service sshd restart
```

参考自：

[在 FreeBSD 上启用 root 登录](https://allen.me/2011/07/22/how-to-enable-root-login-free)

## 配置代理

## 配置代理

如果 `FreeBSD` 位于代理之后，可能需要配置代理。

对于 `csh` 或 `tcsh`，在 `/etc/cshrc` 中设置：

```csh
setenv http_proxy http://proxy:port
```

对于 `sh`，在 `/etc/profile` 中设置：

```sh
export http_proxy=http://proxy:port
```

参考自：

[在 FreeBSD 中使用 Subversion](https://www.rhyous.com/2012/04/13/using-subversion-freebs)

## 关机

## 关机

与某些 `Linux` 发行版相比，`shutdown` 命令现在会停止 `FreeBSD`：

```bash
### shutdown -h now
```

参考自：

[FreeBSD 手页](https://www.freebsd.org/cgi/man.cgi)

## 重启

## 重启

如果你想立即重启 `FreeBSD`，可以使用以下方法：

(1) 直接运行 `reboot` 命令：

```bash
### reboot
```

(2) 使用 `shutdown` 命令：

```bash
### shutdown -r
```

`-r` 代表重启。

## 升级系统

## 升级系统

你应该定期使用 `freebsd-update` 工具来保持系统安全不不过时。例如，更新 `10.3` 版本：

```bash
### freebsd-update -r 10.3
```

安装补丁后，检查系统版本：

```bash
### freebsd-version -ku
10.3-RELEASE-p4
10.3-RELEASE-p5
```

你应该更新 `FreeBSD` 团队发布的补丁：

```bash
### freebsd-update fetch
```

安装完成后，再次检查系统：

```bash
### freebsd-version -ku
10.3-RELEASE-p4
10.3-RELEASE-p5
```

好了！你的系统已刷新！

参考自：

[FreeBSD)

## 升级到新版本

## 升级到新版本

本文以从 `10.2-RELEASE` 升级到 `10.3-RELEASE` 为例，但你必须注意此教程可能不适用于其他版本。因此请阅读相关的发行说明。

(1) 检查当前版本：

```bash
### freebsd-version -ku
10.2-RELEASE
10.2-RELEASE
```

(2) 运行 `freebsd-update upgrade` 命令将系统升级到新版本：

```bash
# freebsd-update upgrade -r 10.3-RELEASE
......
要安装下载的升级，请运行 "/usr/sbin/freebsd-update install"。
```

(3) `freebsd-update upgrade -r 10.3-RELEASE` 的最后日志提示执行 `freebsd-update install`：

```
# freebsd-update install
src component not installed, skipped
Installing updates...
内核更新已安装。请重启并再次运行
"/usr/sbin/freebsd-update install" 以完成更新安装。
```

(4) 重启系统并再次执行 `freebsd-update install`：

```bash
### reboot
# freebsd-update install
src component not installed, skipped
Installing updates... done.
```

(5) 现在检查版本：

```bash
### freebsd-version -ku
10.3-RELEASE-p4
10.3-RELEASE-p5
```

你的系统现在已升级到 `10.3-RELEASE`。

## 安装软件

## 安装软件





如果你对需要的软件没有特定要求，可以使用 `pkg` 工具在 `FreeBSD` 上安装预编译的包，这看起来就像在 `GNU/Linux` 离盒上使用 `yum` 或 `apt-get` 一样。例如，在你的主机上安装 `python`：

```
# pkg install python 
......
```

请注意，某些标准 Python 模块作为独立的 ports 提供的，因为它们需要额外的依赖项。它们可以通过以下方式获取：

bsddb           databases/py-bsddb
gdbm            databases/py-gdbm
sqlite3         databases/py-sqlite3
tkinter         x11-toolkits/py-tkinter

现在你可以运行 `python` 了：

```
### python
Python 2.7.11 (default, Jun  5 2016, 01:23:11)
[GCC 4.2.1 Compatible FreeBSD Clang 3.4.1 (tags/RELEASE_34/dot1-final 208032)] on freebsd10
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

但安装 `python` 最后的日志提示我们还需要安装其他 `4` 个包：`py-bsddb`、`py-gdbm`、`py-sqlite3` 和 `py-tkinter`，否则 `import sqlite3` 将报错：

```
>>> import sqlite3
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/usr/local/lib/python2.7/sqlite3/__init__.py", line 24, in <module>
    from dbapi2 import *
  File "/usr/local/lib/python2.7/sqlite3/dbapi2.py", line 28, in <module>
    from _sqlite3 import *
ImportError: No module named _sqlite3
```

引入了另一种安装方法：使用 ports。这种方法将从源代码下载、编译并安装，这种方法的优点是如果你需要，可以进行一些自定义。你可以在 `/usr/ports` 目录下找到所有的 ports。现在你开始安装 `py-bsddb`（按照此方法设置 `py-gdbm`、`py-sqlite3` 和 `py-tkinter`）：

```
### cd /usr/ports/databases/py-bsddb
### make install clean
```

在全部安装完成后，我们现在可以在 `python` 中使用 `sqlite` 了：

```
### python
Python 2.7.11 (default, Jun  5 2016, 01:23:11)
[GCC 4.2.1 Compatible FreeBSD Clang 3.4.1 (tags/RELEASE_34/dot1-final 208032)] on freebsd10
Type "help", "copyright", "credits" or "license" for more information.
>>> import sqlite3
```

另一种方法是从 `DVD` 安装：

(1) 将 `DVD` 放入驱动器；

(2) 挂载 `DVD`：

```
mkdir -p /dist
mount -t cd9660 /dev/cd0 /dist
```

(3) 安装包（例如 `xorg`）：

```
env REPOS_DIR=/dist/packages/repos pkg install xorg
```

引用：

- [Packages and Ports: Adding Software in FreeBSD](https://www.freebsd.org/doc/en_US.ISO8859-1/articles/linux-users/software.html)
- [Get started with FreeBSD: A brief intro for Linux users](http://www.infoworld.com/article/2858288/unix/intro-to-freebsd-for-linux-users.html)
- [FreeBSD 10 install packages from DVD](https://forums.freebsd.org/threads/44430/#post-300633)

## 搜索软件

如果你想搜索特定的应用程序，可以使用 `pkg search` 命令。例如：

```
### pkg search lsof
lsof-4.90.b,8                  Lists information about open files (similar to fstat(1))
p5-Unix-Lsof-0.0.5_2           Unix::Lsof -- a wrapper to the Unix lsof utility
```

如果你想知道软件在 ports 树中的路径，可以使用 `-o` 选项：

```
### pkg search -o lsof
sysutils/lsof                  Lists information about open files (similar to fstat(1))
sysutils/p5-Unix-Lsof          Unix::Lsof -- a wrapper to the Unix lsof utility
```

万情况下 Ports Collection 已经安装，你可以使用 `whereis` 命令：

```
### whereis lsof
lsof: /usr/local/sbin/lsof /usr/local/man/man8/lsof.8.gz /usr/ports/sysutils/lsof
```

另一个技巧方法是使用 `echo` 命令：

```
### echo /usr/ports/*/*lsof*
/usr/ports/distfiles/lsof_4.90B.freebsd.tar.bz2 /usr/ports/sysutils/lsof
```

引用：

- [Finding Software](https://www.freebsd.org/doc/handbook/ports-finding.html)

## 移除软件

安装应用程序后，你可以使用 `pkg delete` 删除它：

[content] (注：此处原文未提供具体移除操作文本，根据指令保持格式逻辑)





`FreeBSD-STABLE` 独立于 `FreeBSD-CURRENT`，适用于生产版本。它主要接受错误修复和安全更新。

你应该注意到，分支不是一个点，而是持续的开发流。而 `FreeBSD RELEASE` 版本是一个点，它只是 `FreeBSD-STABLE` 分支在某个时刻的快照。

引用：
[跟踪开发分支](https://www.freebsd.org/doc/handbook/current-stable.html);
[发布工程](http://www.over-yonder.net/~fullermd/rants/bsd4linux/05).

## 更新 Ports 集合

位于 `/usr/ports` 下的内容被称为 Ports 集合（Ports Collection），我们可以使用 `portsnap` 命令来更新它：

(1) 如果是第一次使用 `portsnap`，你应该运行以下命令：

```
### portsnap fetch extract
```

否则，你可能会遇到如下所示的错误：

```
......
/usr/ports was not created by portsnap.
You must run 'portsnap extract' before running 'portsnap update'.
```

(2) 此后，你只需要执行 `portsnap fetch update` 即可更新 Ports 集合。

引用：
[使用 Ports 集合](https://www.freebsd.org/doc/handbook/ports-using.html);
[关于使用 portsnanp 升级源码树的问题](https://lists.freebsd.org/pipermail/freebsd-questions/2016-June/272255.html).

## 安装 port 时接受默认选项

在编译和安装 port 过程中，如果你厌倦了提示并想使用所有默认选项，可以利用 `BATCH`：

```
### make install clean BATCH=yes 
```

引用：
[如何在安装 FreeBSD port 时避免提示？](http://unix.stackexchange.com/questions/5257/how-can-i-avoid-the-prompts-when-installing-a-freebsd-port).

## 启用 ls 彩色输出

`ls -G` 可以让 `ls` 输出彩色。如果你使用 `csh`，可以在 `.cshrc` 中添加以下语句：

```
alias ls        ls -G
```

引用：
[FreeBSD: 启用彩色 ls 输出](https://www.cyberciti.biz/tips/freebsd-how-to-enable-colorized-ls-output.html).

## 清晰的目录结构

`FreeBSD` 在基础操作系统和用户添加的应用程序之间有清晰的分，这意味着所有不属于基础系统的内容都在 `/usr/local` 目录下，而 `/usr/local` 目录的结构在很大程度上镜像了 `/` 或 `/usr` 目录中的结构。

例如，从源码树或通过 `package` 命令安装的应用将位于 `/usr/local/bin` 或 `/usr/local/sbin`，对应于 `/bin``/sbin`/`/usr/bin` 和 `/usr/local/sbin`；`/etc` 目录包含基础系统的配置文件，而 `/usr/local/etc` 则用于用户添加的应用程序。

引用：
[给 Linux 用户的 FreeBSD 对比介绍](https://www.digitalocean.com/community/tutorials/a-comparative-introduction-to-freebsd-for-linux-users);
[目录结构](https://www.freebsd.org/doc/handbook/dirstructure.html);
[我喜欢 FreeBSD 的十件事](https://bsdmag.org/download/the_begginers_guide/).

## 修改 shell

如果你之前在 `Linux` 上工作，你可能会怀念 `Bash`，并且不习惯 `FreeBSD` 默认提供的 `csh`。你可以按照以下指令将 shell 改为 `Bash`：

(1) `Bash` 必须已经安装在你的 `FreeBSD` 上，并且其完整路径也应包含在 `/etc/shells` 中。例如：

```
 # pkg install bash
Updating FreeBSD repository catalogue...
FreeBSD repository is up-to-date.
All repositories are up-to-date.
The following 1 package(s) will be affected (of 0 checked):

New packages to INSTALLED:
        bash: 4.3.42_1
......
```

你会发现 `Bash` 路径自动显示在 `/etc/shells` 中：

```
 # cat /etc/shells
# $FreeBSD: releng/10.3/etc/shells 59717 2000-04-27 21:58:46Z ache $
#
# List of acceptable shells for chpass(1).
# Ftpd will not allow users to connect who are not using
# one of these shells.

/bin/sh
/bin/csh
/bin/tcsh
/usr/local/bin/bash
/usr/local/bin/rbash
```

(2) 执行 `chsh -s /usr/local/bin/bash`：

```
### chsh -s /usr/local/bin/bash
chsh: user information updated
```

重新登录后，你会发现 shell 现在是 `bash` 了：

```
### echo $SHELL
/usr/local/bin/bash
```

引用：
[Shells](https://www.freebsd.org/doc/handbook/shells.html).

## 修改 PATH 变量

在 `csh` 中，如果你想更改 `$PATH` 环境变量，你应该修改 `.cshrc` 文件：

```
### cat .cshrc
......
set path = (/sbin /bin /usr/sbin /usr/bin /usr/games /usr/local/sbin /usr/local/bin $HOME/bin $HOME/gocode/bin)
......
```

例如，将 `/usr/local/go/bin` 添加到 `$PATH` 中：

```
### cat .cshrc
......
set path = (/sbin /bin /usr/sbin /usr/bin /usr/games /usr/local/sbin /usr/local/bin $HOME/bin $HOME/gocode/bin /usr/local/go/bin)
......
```

然后执行 `source .cshrc` 命令，你会发现新的 `$PATH` 生效了：

```
### source .cshrc
### echo $PATH
/sbin:/bin:/usr/sbin:/usr/bin:/usr/games:/usr/local/sbin:/usr/local/bin:/root/bin:/root/gocode/bin:/usr/local/go/bin
```

引用：
[杂项与技巧](http://www.freebsdmadeeasy.com/tutorials/freebsd/freebsd-tricks.php).

## 为 bash 着色

(1) 在你的 `$HOME` 目录下创建 `..dir_colors` 文件：





# 下面每种可着色的终端类型都应有一个对应的 TERM 条目

```
TERM ansi
TERM color-xterm
TERM con132x25
TERM con132x30
TERM con132x43
TERM con132x60
TERM con80x25
TERM con80x28
TERM con80x30
TERM con80x43
TERM con80x50
TERM con80x60
TERM cons25
TERM console
TERM cygwin
TERM dtterm
TERM Eterm
TERM gnome
TERM konsole
TERM kterm
TERM linux
TERM linux-c
TERM mach-color
TERM putty
TERM rxvt
TERM rxvt-cygwin
TERM rxvt-cygwin-native
TERM rxvt-unicode
TERM screen
TERM screen-bce
TERM screen-w
TERM screen.linux
TERM vt100
TERM xterm
TERM xterm-256color
TERM xterm-color
TERM xterm-debian
```

# 下面是基础文件类型的颜色初始化字符串。颜色初始化
# 字符串由一个或多个以下数字代码组成：
# 属性代码：
# `00=none` `01=bold` `04=underscore` `05=blink` `07=reverse` `08=concealed`
# 文字颜色代码：
# `30=black` `31=red` `32=green` `33=yellow` `34=blue` `35=magenta` `36=cyan` `37=white`
# 背景颜色代码：
# `40=black` `41=red` `42=green` `43=yellow` `44=blue` `45=magenta` `46=cyan` `47=white`

NORMAL 00           # 全局默认，尽管所有内容都应该是某种状态
FILE 00             # 普通文件
DIR 01;34           # 目录
LINK 01;36          # 符号链接。（如果你将此设置为 'target' 而不是
                    # 数值，则颜色将匹配所指向的文件）
FIFO 40;33          # 管道
SOCK 01;35          # 套接字
DOOR 01;35          # 门
BLK 40;33;01        # 块设备驱动
CHR 40;33;01        # 字符设备驱动
ORPHAN 01;05;37;41  # 孤立符号链接
MISSING 01;05;37;41 # ... 以及它们指向的文件

# 这用于具有执行权限的文件：
EXEC 01;32

# 在下方列出任何希望 ls 着色的文件扩展名，如 '.gz' 或 '.tar'。
# 放入扩展名、一个空格和颜色初始化字符串。
# （以及任何你想在 '# ' 之后添加的注释）

.cmd 01;32 # 可执行文件（亮绿色）
.exe 01;32
.com 01;32
.btm 01;32
.bat 01;32
.sh  01;32
.csh 01;32

.tar 01;31 # 归档/压缩（亮红色）
.tgz 01;31
.arj 01;31
.taz 01;31
.lzh 01;31
.zip 01;31
.z   01;31
.Z   01;31
.gz  01;31
.bz2 01;31
.bz  01;31
.tbz2 01;31
.tz  01;31
.deb 01;31
.rpm 01;31
.rar 01;31        # app-arch/rar
.ace 01;31        # app-arch/unace
.zoo 01;31        # app-arch/zoo
.cpio 01;31       # app-arch/cpio
.7z  01;31        # app-arch/p7zip
.rz  01;31        # app-arch/rzip

.jpg 01;35 # 图像格式
.jpeg 01;35
.gif 01;35
.bmp 01;35
.ppm 01;35
.tga 01;35
.xbm 01;35
.xpm 01;35
.tif 01;35
.tiff 01;35
.png 01;35
.mng 01;35
.xcf 01;35
.pcx 01;35
.mpg 01;35
.mpeg 01;35
.m2v 01;35  # 仅 MPEG-2 视频
.avi 01;35
.mkv 01;35  # Matroska (http://matroska.org/)
.ogm 01;35  # Ogg 文件
.mp4 01;35  # MPEG-4 的“官方”容器
.m4v 01;35  # 仅 MPEG-4 视频
.mov 01;35  # QuickTime 
.flv 01;35  # Adobe Flash 视频
.wmv 01;35  # Windows Media Video
.3gp 01;35   # 3 视频





```
### swapinfo -m
Device          1M-blocks     Used    Avail Capacity
/dev/da0p3           1023        0     1023     0%
```

引用：

[PSTAT](https://www.freebsd.org/cgi/man.cgi?query=swapinfo&sektion=8)。

## 使用 "ps" 显示进程状态

## 使用 "ps" 显示进程状态

如果你在不带任何选项的情况下运行 `ps` 命令，它将只显示具有控制终端的进程：

```
### ps
PID TT  STAT    TIME COMMAND
854 v0  Is+  0:00.00 /usr/libexec/getty Pc ttyv0
710 v1  Is+  0:00.00 /usr/libexec/getty Pc ttyv1
711 v2  Is+  0:00.00 /usr/libexec/getty Pc ttyv2
712 v3  Is+  0:00.00 /usr/libexec/getty Pc ttyv3
713 v4  Is+  0:00.00 /usr/libexec/getty Pc ttyv4
714 v5  Is+  0:00.00 /usr/libexec/getty Pc ttyv5
715 v6  Is+  0:00.00 /usr/libexec/getty Pc ttyv6
716 v7  Is+  0:00.00 /usr/libexec/getty Pc ttyv7
847  0  Ss   0:00.04 -csh (csh)
883  0  R+   0:00.00 ps
```

如果你也想查看没有控制终端的进程，请添加 `-x` 选项：

```
### ps -ax
PID TT  STAT     TIME COMMAND
  0  -  DLs   0:00.10 [kernel]
  1  -  ILs   0:00.05 /sbin/init --
  2  -  DL    0:00.05 [cam]
  3  -  DL    0:00.00 [mpt_recovery0]
  4  -  DL    0:00.00 [sctp_iterator]
  5  -  DL    0:00.04 [pagedaemon]
  6  -  DL    0:00.00 [vmdaemon]
  7  -  DL    0:00.00 [pagezero]
  8  -  DL    0:00.08 [bufdaemon]
  9  -  DL    0:00.01 [vnlru]
 10  -  DL    0:00.00 [audit]
 11  -  RL   50:35.75 [idle]
 12  -  WL    0:08.20 [intr]
 13  -  DL    0:00.02 [geom]
 14  -  DL    0:00.91 [rand_harvestq]
 15  -  DL    0:00.44 [usb]
 16  -  DL    0:00.20 [syncer]
302  -  Is    0:00.01 dhclient: em0 [priv] (dhclient)
364  -  Is    0:00.00 dhclient: em0 (dhclient)
379  -  Is    0:00.00 /sbin/devd
524  -  Ss    0:00.02 /usr/sbin/syslogd -s
652  -  Is    0:00.00 /usr/sbin/sshd
655  -  Ss    0:00.10 sendmail: accepting connections (sendmail)
658  -  Is    0:00.00 sendmail: Queue runner@00:30:00 for /var/spool/clientmqueue (sendmail)
662  -  Ss    0:00.01 /usr/sbin/cron -s
844  -  Ss    0:00.06 sshd: root@pts/0 (sshd)
854 v0  Is+   0:00.00 /usr/libexec/getty Pc ttyv0
710 v1  Is+   0:00.00 /usr/libexec/getty Pc ttyv1
711 v2  Is+   0:00.00 /usr/libexec/getty Pc ttyv2
712 v3  Is+   0:00.00 /usr/libexec/getty Pc ttyv3
713 v4  Is+   0:00.00 /usr/libexec/getty Pc ttyv4
714 v5  Is+   0:00.00 /usr/libexec/getty Pc ttyv5
715 v6  Is+   0:00.00 /usr/libexec/getty Pc ttyv6
716 v7  Is+   0:00.00 /usr/libexec/getty Pc ttyv7
847  0  Ss    0:00.04 -csh (csh)
897  0  R+    0:00.00 ps -ax
```

时间，还有更多 `TT` 列为 `-` 的结果。最常用的 `ps` 命令是 `ps aww`，它会显示所有进程的详细信息，这类似于 `GNU/Linux` 上的 `ps -ef`：

```
 ps aww
USER  PID %CPU %MEM   VSZ  RSS TT STARTED     TIME COMMAND
root   11 99.2  0.0   116   -  RL    50:48 54:14.29 [idle]
root    0  0.0  0.0   160   -  DLs   50:48  0:00.10 [kernel]
root    1  0.0  0.0  9492  772  -  ILs   50:48  0:00.05 /sbin/init
root    2  0.0  0.0    32   -  DL    50:48  0:00.05 [cam]
root    3  0.0  0.0    48   -  DL    50:48  0:00.00 [mpt_recovery0]
root    4  0.0  0.0    16   -  DL    50:48  0:00.00 [sctp_iterator]
root    5  0.0  0.0    32   -  DL    50:48  0:00.00 [pagedaemon]
root    6  0.0  0.0    0   -  DL    50:48  0:00.00 [vmdaemon]
root    7  0.0  0.0    0   -  DL    50:48  0:00.00 [pagezero]
root    8  0.0  0.0    32   -  DL    50:48  0:00.08 [bufdaemon]
root    9  0.0  0.0    16   -  DL    50:48  0:00.01 [vnlru]
 10  -  0.0  0.0    0   -  DL    50:48  0:00.00 [audit]
 11  -  0.0  0.0    0   -  RL    50:48  50:35.75 [idle]
 12  -  0.0  0.0    0   -  WL    50:48  0:08.20 [intr]
 13  -  0.0  0.0    32   -  DL    50:48  0:00.02 [geom]
 14  -  0.0  0.0    0   -  DL    50:48  0:00.91 [rand_harvestq]
 15  -  0.0  0.0    16   -  DL    50:48  0:00.44 [usb]
 16  -  0.0  0.0    16   -  DL    50:48  0:00.20 [syncer]
root   302  -  0.0  0.1  2148  -  Is    50:48  0:00.01 dhclient: em0 [priv] (dhclient)
root   364  -  0.0  0.1  2236  -  Is    50:48  0:00.00 dhclient: em0 (dhclient)
root   379  -  0.0  0.2  4932  -  Ss    50:48  0:00.00 /sbin/devd
root   524  -  0.0  0.1  2092  -  Ss    50:48  0:00.02 /usr/sbin/syslogd -s
root   652  -  0.0  0.3  6564  -  Is    50:48  0:00.00 /usr/sbin/sshd
root   655  -  0.0  0.3  5380  -  Ss    50:48  0:00.10 sendmail: accepting connections (sendmail)
smmsp  658  -  0.0  0.2  5044  -  Is    50:48  0:00.00 sendmail: Queue runner@00:30:00 for /var/spool/clientmqueue (sendmail)
root   662  -  0.0  0.1  2212  -  Ss    50:48  0:00.01 /usr/sbin/cron -s
root   844  -  0.0  0.0  0   -  Ss    50:48  0:00.06 sshd: root@pts/0 (sshd)
```



```
### freecolor
Physical  : [#################################..] 94%   (1907820/2018396)
Swap      : [###################################] 100%  (1048540/1048540)
```

以传统的 `free` 格式显示用法：

```bash
### freecolor -m -o
             total       used       free     shared    buffers     cached
Mem:          1971        107       1863          0          0          0
Swap:         1023          0       1023
```

参考：

[FreeBSD 查找 RAM 内存大小，包括空闲和已用内存大小](http://www.cyberciti.biz/faq/freebsd-command-to-get-ram-information/).

## 使用 Subversion 的注意事项

## 使用 Subversion 的注意事项

如果您想使用 `Subversion`（例如更新 ports 树），您应该注意以下问题：

(1) 如果您的服务器运行在代理之后，您应该修改您的 `Subversion` 配置文件：

```bash
### cat ~/.subversion/servers
[global]
http-proxy-host = web-proxy.xxxx.com
http-proxy-port = 8080
http-compression = no
```

否则，您可能会遇到以下错误：

```bash
### svn checkout https://svn.FreeBSD.org/ports/head /usr/ports
Error validating server certificate for 'https://svn.freebsd.org:443':
 - 证书不是由信任的机构颁发的。请使用
   指纹手动验证证书！
 - 证书主机名不匹配。
证书信息：
 - Hostname: FG3K6C3A15800021
 - Valid: from Mar 21 09:15:26 2015 GMT until Mar 21 09:15:26 2025 GMT
 - Issuer: FG3K6C3A15800021, Fortinet Ltd.
 - Fingerprint: 1D:F4:21:20:2F:06:41:45:3F:7A:18:FB:79:F3:BB:30:36:32:22:A3
(R)eject，临时接受 (t) 还是永久接受 (p)? p
svn: E170013: Unable to connect to a repository at URL 'https://svn.freebsd.org/ports/head'
svn: E000054: Error running context: Connection reset by peer
```

或：

```bash
### svn checkout https://svn.FreeBSD.org/ports/head /usr/ports
......
svn: E175002: REPORT request on '/ports/!svn/me' failed
```

(2) 如果您在执行 `svn` 命令时遇到类似下面的错误：

```bash
svn: E200030: SQLite compiled for 3.11.1, but running with 3.9.2
```

您应该更新您的 `SQLite`：

```bash
### pkg upgrade sqlite3
```

参考文献：

[在受控网络中使用 FreeBSD – 必须的 HTTP 代理且无 FTP](http://www.rhyous.com/2012/04/13/using-freebsd-inside-a-controlled-network-a-required-http-proxy-and-no-ftp/)；

[如何为 svn 配置 HTTP 代理](http://stackoverflow.com/questions/1491180/how-to-configure-a-http-proxy-for-svn).

## 输出 PCI 设备信息

## 输出 PCI 设备信息

`FreeBSD` 提供了 `pciconf` 命令，可以列出 `PCI` 设备信息：

```bash
### pciconf -lv
hostb0@pci0:0:0:0:  class=0x060000 card=0x197615ad chip=0x71908086 rev=0x01 hdr=0x00
vendor = 'Intel Corporation'
device = '440BX/ZX/DX - 82443BX/ZX/DX Host bridge'
class  = bridge
subclass   = HOST-PCI
pcib1@pci0:0:1:0:   class=0x060400 card=0x00000000 chip=0x71918086 rev=0x01 hdr=0x01
vendor = 'Intel Corporation'
device = '440BX/ZX/DX - 82443BX/ZX/DX AGP bridge'
class  = bridge
subclass   = PCI-PCI
isab0@pci0:0:7:0:   class=0x060100 card=0x197615ad chip=0x71108086 rev=0x08 hdr=0x00
vendor = 'Intel Corporation'
device = '82371AB/EB/MB PIIX4 ISA'
class  = bridge
subclass   = PCI-ISA
......
```

如果您习惯了 `GNU/Linux` 自带的 `lspci`，您可以自行安装：

```bash
### pkg install pciutils
```

