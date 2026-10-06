

```
root@kemal:/usr/share/doc# ls
trace
acceck
accountservice
ace-voip
ac
adduser
adwaita-icon-theme
afflib-tools
agfln
aircraft-ng
alsa-tools
amap
amd64-microcode libpng12-dev
libpod-latex-perl
libpod-readme-perl
polkit-agent-1-0
libpolkit-backend-1-0
libpolkit-geoip-1-0
libpopler-46
libpopler-glib
libpopler-qt4-4
libport0
libportaudio2
libpostproc52
libpotrace0
```

Man pages（帮助页）是 Linux 系统中的基础帮助文件。一个 man 页的结构通常如下：

- NAME：命令的名字和定义
- SYNOPSIS：如何使用该命令
- DESCRIPTION：命令功能的描述
- EXAMPLES：命令的用法示例。
- SEE ALSO：相关标题。

手册页位于下方 /usr/share/man。

```
root@kemal:/usr/share/man# ls id man1 man5 nl pt_BR sl vi
cs es fr.,UTF-8 gl it man2 man6 pl ro sr zh
da fi qi ja man3 man7 pl.UTF-8 ru sv_CN
de br hr de.UTF-8 fr.TR.ISO8859-1 hu ko man4 man8 pl sk tr zh_TW
root@kemal:/usr/share/man# _
```

手册页的配置如下：

- man1：通用用户程序。
- man2：系统程序。
- man3：库函数。（关于 C 语言编程）
- man4：私有文件。
- man5：文件格式。
- man6：游戏和屏幕保护程序。
- man7：不属于其他类别的各种命令。
- man8：系统管理与维护。

要查看 ls 命令的 man 帮助页（解释我们在上面提供的示例中的 help 命令），我们可以使用 **man ls command**。

![](img/aa6ce54dbb8ffe5b9d7befb8c6764064_28_0.png)

在查阅手册页中的帮助主题后，应按 **Q** 键退出。

# 30 | Linux 命令精大师

## Whatis

另一个名为 **whatis** 的命令，它可以间接帮助我们。我们可以使用这个命令来查找手册中某个应用程序或命令的帮助主题所在的位置。

```
root@kemal:~ whatis echo
echo (1)           - 显示一行文本
```

如果你想使用通配符进行查询（我们稍后会讨论到），你必须使用 **-w** 参数。例如 **whatis -w cal**。

```
root@kemal:~ whatis cal+
cal+: nothing appropriate.
root@kemal:~ whatis cal+
cal (1)           - 显示日历和复活节日期
calendar (1)      - 提醒服务
calloc (3)       - 分配和释放动态内存
calloc (3avr)     - (未知主题)
callprpc (3)     - 远程过程调用的库程序
```

## Apropos

**apropos** 命令用于获取帮助，它实际上会在后台运行 **man -k** 命令。

```
root@kemal:~ man -k printf
asprintf (3)      - 打印到分配的字符串
dnprintf (3)       - 打印到文件描述符
fprintf (3)       - 格式化输出转换
printf (3avr)     - (未知主题)
printf.P (3avr)   - (未知主题)
fprintf (3)      - 格式化字符输出转换
printf (1)        - 格式化打印数据
printf (3)        - 格式化输出转换
printf (3avr)     - (未知主题)
printf.P (3)       - (未知主题)
sprintf (3)      - 格式化输出转换
sprintf (3avr)     - (未知主题)
sprintf.P (3avr)   - (未知主题)
```

查看输出命令可以看到包含 **printf** 词的应用程序。**apropos** 命令的输出与 **man -k** 命令的输出相同。

```
root@kemal:~# apropos printf
asprint - to allocated string
dprintf (3) - print to a file descriptor
printf (3) - formatted output conversion
printf (3avr) - (unknown subject)
printf P (3avr) - (unknown subject)
fwprintf (3) - formatted wide-character output conversion
printf (1) - format and print data
printf (3) - formatted output conversion
printf (3avr) - (unknown subject)
```

最后，如果无法在 man 页中找到帮助，可以在更新 man 目录内存后尝试。可以使用 mandb 命令进行更新。

```
root@kemal:~# mandb
Purging old database entries in /usr/man...
Processing manual pages under /usr/man...
Purging old database entries in /usr/share/man...
Processing manual pages under /usr/share/man...
Purging old database entries in /usr/share/man/zh...
Processing manual pages under /usr/share/man/zh...
Purging old database entries in /usr/share/man/sr...
```

# 第 3 章：获取信息的命令

有几个命令可以获取我们系统中存储的关于进程、用户等相关信息。

### Lsb Release

要查找我们所使用的 Linux 发行版名称，我们使用 lsb_release -a。

```
root@kemal:-# lsb_release -a
No LSB modules available.
Distributor ID: Kali
Description: Kali/Linux 2.0
Release: 2.0
Codename: Kali
```

类似的命令是 cat /etc/release。通过它，我们可以获取更多关于系统的系统的信息。

```
root@kemal:-# cat /etc/release
DISTRIB_ID=Kali
DISTRIB_RELEASE=2.0
DISTRIB_DENAME=Kali
PRETTY_NAME="Kali/Linux 2.0"
NAME="Kali"
VERSION="2.0"
ID_LIKE=debian
HOME_URL="http://kali.org/"
SUPPORT_URL="http://forums.kali.org/"
BUG_REPORT_URL="http://bugs.kali.org/"
```

# 34 | Linux 命令精大师

### Issue

要查看我们正在使用的 Linux 名称，也可以使用 cat /etc/issue 命令。

```
root@kemal:~# cat /etc/issue
Kali/Linux 2.0
```

### uname

要查找我们系统的内核版本，也可以使用 uname -a 命令。

```
root@kemal:~# uname -a
Linux kemal 4.0.0-kali1-686 #1 SMP Debian 4.0.4-1+kali (2015-06-03) i686
```

事实上，通过 -a 参数，我们不仅学习了内核版本，还学习了内核名称以及所有信息，例如架构。单独查询可以按如下所示：

```
root@kemal:~# uname
Linux
root@kemal:~# uname -n
kemal
root@kemal:~# uname -m
i686
root@kemal:~# uname -r
4.0.0-kali1-686
```

### Cal

我们可以使用 cal 命令在控制台上显示系统当前所在月份的月度日历。

```
root@kemal:~# cal
Agustos 2015
Pe Sa Pr Cu
             1
2 3 4 5 6 7 8
9 10 11 12 13 14 15
16 17 18 19 20 21 22
23 24 25 26 27 28 29
30 31
```

例如，如果你想看 1977 年的第一月，你应该使用 cal 1977。

```
root@kemal:~# cal 1977
Ocak 1977
Pe Sa Pr Cu
             1
2 3 4 5 6 7 8
9 10 11 12 13 14 15
16 17 18 19 20 21 22
23 24 25 26 27 28 29
30 31
```

对于特定的年份，我们可以使用类似的命令。

### Date

Date 命令用于查找系统的当前时间和日期信息。

```
root@kemal:~# date
Sat Aug 22 21:00:34 EEST 2015
```

### Hostname

要查看我们使用的计算机系统的主机名，可以使用 hostname 命令。

```
root@kemal:~# hostname
kemal
```

### Who-Whoami

要查找系统中哪些用户活跃、谁登录了、查找身份信息，我们可以使用 w, who, whoami 命令。

```
root@kemal:-# w
01:55:59 up 8:17, 2 users, load average: 0.78, 1.06,
USER     TTY             FROM LOGIN@ IDLE JCPU
root     :0               17:39 ?xdm? 55:50
root     pts/0           :0               17:48 0.00s 0.58
```

这些命令有其用途。简之：

- w：查找当前时刻运行应用程序/命令的用户。
- who：识别系统中正在工作的配置文件。
- whoami：识别正在操作的用户身份。

```
root@kemal:-# who              2015-08-22 17:39 (:0)
root     :0
root     pts/0         2015-08-22 17:48 (:0)
root@kemal:-# whoami
root
root@kemal:-# am i
root     pts/0         2015-08-22 17:48 (:0)
```

当我们使用 who 命令并配合 -b 时，可以看到系统上一次运行的时间，使用 -r 显示当前的运行级别（runlevel）。

