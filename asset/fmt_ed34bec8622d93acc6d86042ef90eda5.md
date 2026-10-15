
正则表达式定义了一组一个或多个字符字符串。正则表达式被认为匹配它所定义的任何字符串。以下字符在正则表达式中是特殊字符：

| 特殊字符 | 功能 |
| --- | --- |
| `.` | 匹配任意单个字符 |
| `*` | 匹配前一个字符匹配的零次或多次 |
| `^` | 强制从行首开始匹配 |
| `\` | 用于给特殊字符加引号 |
| `\<` | 强制从单词开始匹配 |
| `\>` | 强制从单词结束处匹配 |

以下字符串是正则表达式的特殊形式，用于匹配字符类和括号正则表达式：

| 正则表达式 | 功能 |
| --- | --- |
| `[xyz]` | 定义一个匹配 x, y 或 z 的字符类 |
| `[^xyz]` | 定义一个匹配除 x, y 或 z 之外任意字符的字符类 |
| `[x-z]` | 定义一个匹配从 x 到 z（包含边界）任意字符的字符类 |
| `(xyz)` | 匹配 xyz（一个括号正则表达式） |

除了上述特殊字符和字符串（排除带引号的括号），以下字符在扩展正则表达式中是特殊的：

| 特殊字符 / 正则表达式 | 功能 |
| --- | --- |
| `+` | 匹配前一个字符的一次或多次出现 |
| `?` | 匹配前一个字符的零次或一次出现 |
| `(xyz)+` | 前一个字符的一次或多次出现 |

### 扩展正则表达式 912

| 特殊字符 / 正则表达式 | 功能 |
|---|---|---|
| `(xyz)?` | 前一个字符的零次或一次出现 |
| `(xyz)*` | 前一个字符的一次或多次出现 |
| `xyz|abc` | xyz 或 abc |

参见第 220 页关于 `sed` 中正则表达式的描述。以下字符在替换字符串中是特殊的：

| 字符 | 功能 |
|---|---|
| `&` | 代表正则表达式（搜索字符串）所匹配的内容 |
| `\n` | 带引号数字 n，代表括号正则表达式 |

## 964 帮助！

为 Linux 用户和潜在用户提供了大量的帮助。有些帮助在书内，有些在书外。书外还有更多帮助，只需要花一点精力寻找。互联网比大多数人想象的要大得多。所有的源代码和大部分 Linux 文档在网上都有。网上有大量的 Linux 用户和管理员帮助，你只需要找到并下载它们。这就是附录的第一部分内容：查找和下载 Linux 信息、文档、源代码。

附录的最后部分了与你的系统相关的问题：如何使用打印机、按键含义以及 shell 和版本信息。

### 1. 我可以在系统的哪里找到 Linux 文档？

Linux 发行版通常不带纸质参考手册。它们确实提供了存储在线的参考页。你可以使用 `man` 或 `xman` 工具读取这些被称为 man 页的文档（执行命令 `man man`，详见第 27 页）。你可以在阅读本书时或确定可用 Linux 功能时通过 man 页获取特定信息。你可以使用 `apropos` 工具搜索主题（执行命令 `apropos apropos` 或 `man apropos`，详见第 50 页）。

## 916 附录 B：帮助！

最后，文件中有一个存储了各种文档的存储区域。该区域被称为 `/usr/doc` 目录，它通常包含比通过 `man` 或 `info` 工具获取的更详细的信息。命令 `cd /usr/doc` 更改你的工作目录，而 `ls` 则显示该目录下的目录列表：

```
$ cd /usr/doc
ls
findultis-4.1-3 m4-1.4-2 sed-2.05-1
FAQ fwhois-1.00-2 make-3.74-3 sendmail-8.7.1-2
HOWTO gawk-2.15-6 modules-2.0.0-1 tsh-utils-11-2
HTML mt-2.9.1-2 tsch-0.94-2 textutils-12.1.3
LST grep-2.0.0 ncurses-19.6-2
SysVint-2.56-6 gzip-2.1.4-2 nfs-server-2.beta-4a1 time-1.6
SysVint-2.56-2 ICS-1.2-2 nslookup.help t tksysv-0.9-1
Xfree86-3.11-1 iputils-2.2-5 patch vim-3.1.3
bash-2.3.2 ishell-3.11-18 pccmsa-z-2.7-6 wu-ftpd-2.4.3
calderacloc-0.1-2 less libc-5.0-9 portmap-4.0-1 xv-3.10a-1
cpio-2.3-2 lio-1.1-16 ppp-2.2.1-3 yp-clients-2.0.1
dnffutils-2.7-2 ppp-2.0.1 zoneinfo-95e-2
ed-0.8-2 rpm-2.2.4-1
fileutils-3.12.2-5
```

如果你想获取关于 xv 的更多信息，在 `xv-3.10a-1` 目录中看到的是 `ls` 后面跟着一个以 xv 开头的模糊引用，例如“Filename Generation/Pathname Expansion”（第 106 页）。你也可以获取命令 `ls xv-3.10a-1`。在这种情况下，最有趣的内容可能是 `xvdocs.ps`。ps 文件扩展名告诉你它是一个 postscript 文件。然后你可以将 postscript 文件发送到打印机（如下所示），或使用 `ghostscript` 查看它（执行命令 `ghostscript xv*.ps`）。

```
$ ls xv* CHANGELOG
BUGS IDEAS README xvdocs.ps
$ ls pr*/ xvdocs.ps
```

```
$ cd HOWTO
ls
BootPrompt-HOWTO.gz ... README
Bootdisk-HOWTO.gz German-HOWTO.gz SCSI-HOWTO.gz
Busmouse-HOWTO.gz HAM-HOWTO.gz Mail-HOWTO.gz SCSI-Programming-HOWTO.gz
CDROM-HOWTO.gz INDEX MCR-HOWTO.gz --HOWTO.gz
COPV-HOWTO.gz HP-HOWTO.gz NET-HOWTO.gz Sound-HOWTO.gz
Commercial-HOWTO.gz Hebrew-HOWTO.gz NIS-HOWTO.gz Term-HOWTO.gz
Cyrillic-HOWTO.gz INDEX News-HOWTO.gz Tips-HOWTO.gz
DOSEU-HOWTO.gz PCI-HOWTO.gz UPS-HOWTO.gz
Data-HOWTO.gz INFO-short-HOWTO.gz USDOS-HOWTO.gz
Distribution-HOWTO.gz INFO-SHEET-HOWTO UCP-HOWTO.gz
ELF-HOWTO.gz Installation Portuguese-HOWTO.gz Xfree86-HOWTO.gz
Ethernet-HOWTO.gz JE-HOWTO.gz Printing-HOWTO.gz mini
Firewall-HOWTO.gz Kernel-HOWTO.gz Printing-Usage-HOWTO.gz other-formats
```

当你看到 `Bootdisk.HOWTO.gz` 文件名时，.gz 文件扩展名告诉你该文件是用 `gzip` 压缩的，你必须使用 `gzip` 或 `zcat` 进行解压（第 48 页）。执行以下命令打印它：

```
$ zcat Bootdisk.HOWTO.gz | lpr
```

### 有哪些实用的 Linux 互联网网站？

你可以使用 `less`（第 36 页）在屏幕上查看文件，如下：

```
$ zcat Bootdisk* | less
```

Linux 启动盘 HOWTO

Graham Chapman, grahamc@zeta.org.au

v1.02, 1995年6月25日

本文描述了如何创建 Linux 启动盘、启动/根和工具维护磁盘。这些磁盘可以用作救援磁盘或测试新内核。

- 1. 引言
- 1.1 为什么要制作启动盘？

Linux 启动盘在许多情况下都很有用，例如：

- 测试新内核。
- 从磁盘或系统故障中恢复。此类故障可能是从丢失引导区到磁盘头损坏的任何问题。

制作启动盘有几种方法：

### 有哪些实用的 Linux 互联网网站？

通常这些特定网站非常忙，以至于你无法登录。当这种情况发生时，通常会有一些镜像站点。在这种情况下，你通常可以通过 [Linux 主页](http://www.linux.org) 访问相关信息。

## 920 附录 B：帮助！

220 freya FTP 服务器 (版本 wu2-4(51) 1995年9月6日 00:54:08 EDT)

已就绪。

用户名 (ftp.yggrasil.com:mark): ftp

331 访客登录成功，请以您的电子邮件地址作为密码。

密码:

230 访客登录成功，适用访问限制。

远程系统类型为 UNIX。

正在使用二进制模式传输文件。

```bash
ftp cd mirrors/sunette
```

250- 请阅读 READAME 文件

250- 最后修改于 1996年6月5日 07:40:00 - 77天 天前

250- 命令成功。

ftp

```
dir
```

200 PORT 命令成功。

150 正在为 /bin/ls 打开 ASCII 模式数据连接。

```
drwxr-xr-x 18 mirror      1024 Aug 11 19:38
drwxr-xr-x 17 mirror      1024 Dec 6 1995
-r--r--r-- 1 mirror      189638 Jan 14 01:50-00-Linux.gz
drwxr-xr-x 12 mirror      1024 Aug 5 15:55 ALPHA
drwxr-xr-x 12 mirror      3072 Mar 19 01:59 CCC
-r--r--r-- 1 mirror      1751 Apr 24 17:36 INDEX
d-r--r--r-- 1 mirror      29313 Apr 23 14:26 INDEX.html
d-r--r--r-- 1 mirror      2904 Apr 24 17:36 INDEX.short
drwxr-xr-x 1 mirror      110806 Jul 15 00:02 INDEX.world.gz
drwxr-xr-x 2 mirror      20483 Jun 25 21:10 MIRRORS
drwxr-xr-x 1 mirror      11261 Jun 26 21:10 MIRRORS.
drwxr-xr-x 1 mirror      64174 Jul 11 15:40 NEW
d-r--r--r-- 1 mirror      31538 Aug 20 14:45 New.Apr20
d-r--r--r-- 1 mirror      70923 Aug 20 14:45 New.Apr20.
d-r--r--r-- 1 mirror      145441 Jul 11 15:40 NEW
d-r--r--r-- 1 mirror      737 Jun 5 14:41 READAME
dr-xr-xr-x 18 mirror      1024 Aug 5 15:55 apps
drwxr-xr-x 17 mirror      1024 Aug 5 15:55 devel
drwxr-xr-x 16 mirror      1024 Aug 5 15:55 distributions
drwxr-xr-x 10 mirror      1024 Aug 5 15:55 docs
d-r--r--r-- 1 mirror      409 Oct 14 19:53 how.to.submit
drwxr-xr-x 10 mirror      501 Nov 14 09:59 info/for.cdrom.vendors
drwxr-xr-x 10 mirror      1024 Aug 5 16:03 kernel
drwxr-xr-x 8 mirror      1024 Aug 5 15:55 utils
d-r--r--r-- 1 mirror      906 Jun 5 14:39 welcome.html
```

226 传输完成。

ftp

257 "mirrors/1-2-sunite.com/pub/Linux" 是当前目录。

cd apps/editors

250- 请阅读 READAME 文件

250- 最后修改于 1992年10月20日 17:00:00 - 1400天前

250 CWD 命令成功。

ftp dir

200 PORT 命令成功。

150 正在为 /bin/ls 打开 ASCII 模式连接。

```
-r--r--r-- 1 mirror      275836 Mar 7 1995 joe-2.8-src+bin.tar.gz
-r--r--r-- 1 mirror      443 Mar 6 1995 joe-2.8-lsm
```

226 传输完成。

ftp

200 类型已设置为 I。

## 我该如何获取、编译并安装软件？

```bash
ftp get joe-2.8-src+bin.tar.gz
200 PORT 命令成功。
150 正在为 joe-2.8-src+bin.tar.gz 打开 BINARY 模式数据连接。
(275836 bytes)
226 传输完成。
在 133 秒内接收了 275836 字节 (2 Kbytes/sec)
quit
221 再见。
$ ls -l joe*
-rw-r--r-- 1 mark      275836 Aug 21 17:00 joe-2.8-src+bin.tar.gz
$ tar -zvf joe*
joe-2.8/
joe-2.8/.macsrc
joe-2.8/.joerc
joe-2.8/.picorc
joe-2.8/.starrc
joe-2.8/.rjoerc
joe-2.8/INFO
joe-2.8/LIST
joe-2.8/joe
joe-2.8/jacs
joe-2.8/starrc
joe-2.8/rjoec
joe-2.8/jpico
joe-2.8/README.linux
joe-2.8/termix
joe-2.8/joe-1sm
$ ls -l joe
-rwxrxr-x 5 mark 177156 3 1995 joe
$ mv joe /usr/local/bin
mv cannot move 'joe' to '/usr/local/bin': Permission denied
$ su
Password:
$ mv joe /usr/local/bin
$ chmod 755 /usr/local/bin/joe
$ exit
```

### 5. 我如何获取、编译并安装软件？

无论你对 Linux 系统有多满意，迟早都会想要安装或升级软件包。安装软件包的步骤由软件包的创建者决定，且彼此差异很大。请参考第 918 页关于下载和安装 joe 的说明，这是一个相对简单的过程。虽然没有统一的安装标准，但有一些常用的技术。第 922 到 926 页的讨论将引导你安装特定的软件包——Z Shell。

### 6. 我如何从互联网下载软件？

要安装新的软件包或新版本的软件，你需要软件副本。获取 Linux 软件（尤其是免费软件）的一种常用方法是从互联网获取软件包。使用 `ftp` 工具（第 169 和 743 页）连接到拥有软件包的远程站点并下载、拷贝。

了解软件包的一种方法是通过新闻组的消息。如果你足够幸运，你的阅读器将能够代表你从消息下载软件。如果是这种情况，新闻阅读器将找到软件包并运行 ftp。

在示例中，Jenny 下载并安装了新发布的 Z Shell 3.0.0。她的第一步是连接到发布 zsh 的站点并使用 ftp 下载。大多数软件发行 tar 存档（第 48 和 872 页）已使用 `gzip` 压缩（第 45 和 755 页），以节省空间和传输时间。此类文件通常具有 `.tar.gz` 或 `.tgz` 扩展名。

有些发行者提供源代码和预编译的二进制版本。由于编译软件包通常是一个复杂且耗时的过程，对于你的 Linux 系统来说，安装二进制版本更容易。大多数常用软件包仅提供二进制版本。

Jenny 选择了 uarchive.cs.uuc 站点。她使用 `cd` 进入工作目录 `/usr/local/src/incoming`——下载软件的目录——并使用 `ftp` 命令连接远程。一旦作为匿名用户 (`ftp`) 连接，她将电子邮件地址作为密码，进入存放 zsh 发行版的目录并列出该目录。

```bash
$ cd /usr/local/src/incoming

$ ftp uarchive.cs.uuc.edu

Connected to uarchive.cs.uuc.edu.

220 uarchive.cs.uuc.edu: FTP 服务器 (版本 v2.4(5) 1995年6月13日 17:42:00 UTC) 已就绪。

用户名 (uarchive.cs.uuc.edu): ftp:

密码 uarchive.cs.uuc.edu:ftp:

331 访客登录成功，输入地址作为密码。

230 访客登录成功，适用访问限制。

远程系统为 UNIX。

正在使用二进制模式传输文件。

$ cd pub/packages/shells/zsh

250 命令成功。

$ dir

200 PORT 命令成功。

150 为 /bin/ls 打开 ASCII 数据连接。

total 8384

-rw-xr--r-- 1 ftpadmin ftpadmin 59652 Aug 15 22:23 FEQ

-rw-xr--r-- 1 ftpadmin ftpadmin 1466 Aug 15 22:54 MDOSSUM

-rw-xr--r-- 1 ftpadmin ftpadmin 3139 Aug 23 02:54 META
```
