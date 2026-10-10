
你武器库中的主要武器是 `find` 命令。该命令可以快速遍历指定目录（以及其他文件系统），并根据你的规范显示找到的文件。例如，你可以使用 `find` 命令在系统中搜索备份文件（通常以 `.bak` 扩展名标识），如下所示：

```
# find / -name *.bak
/home/dball1/Office51/config/rootag.bak
/home/dball1.kde/share/apps/kfm/cookies.bak
/usr/X11R6/lib/X11/xfig/html/images/add-arrow-button.gif.bak
/usr/X11R6/lib/X11/xfig/html/images/open-compound-button.gif.bak
/usr/X11R6/lib/X11/xfig/html/images/screen-image.fig.bak
/usr/X11R6/lib/X11/xfig/html/images/update-control.gif.bak
/var/lib/nfs/sm.bak
/etc/printcap.bak
/root/.kde/share/apps/kfm/cookies.bak
```

然后，你可以通过将 `find` 命令的输出通过管道传递给 `xargs` 命令，并使用 `rm` 命令删除文件来快速删除这些文件：

```
# find / -name *.bak | xargs rm -f
```

其他适合删除的候选文件包括 `*.bak` 文件、扩展名为 `.o` 的文件（来自编译操作的目标文件）以及名为 "core" 的文件。如果你不想删除这些文件，可以构建一个候选列表：

```
# find / -name *.o >> files_to_delete.txt
```

## 最小化系统日志

Linux 系统中另一个会随着时间增长的区域是你的系统日志。日志记录了近乎所有由不同软件执行的操作和输出，例如内核、邮件、数据库、打印以及其他守护进程和服务。这些日志可能会变得相当大，占用许多兆字节宝贵的磁盘空间。

每个月，包含在 `/var/log` 目录中的这些日志通常会被“滚动”并重命名，以便创建新的日志。旧的日志文件会在其文件名后附加数字，如 1、2、3 等。在使用笔记本电脑上的 Linux 一段时间后，你可以使用 `find` 和 `ls` 命令快速了解这些日志的大小：

```
# find /var/log -name *.4 | xargs ls -l
-rw------- 1 root root 645185 Feb 6 04:02 /var/log/cron.4
-rw-r---m 1 root root 0 Jan 30 04:02 /var/log/httpd/access_log.4
-rw-r---m 1 root root 979 Jan 31 13:31 /var/log/httpd/error_log.4
-rw-r--r-- 1 root root 1472087 Feb 6 04:02 /var/log/maillog.4
-rw-r--r-- 1 root root 171891 Feb 6 04:02 /var/log/messages.4
-rw-r-x--x-- 1 root root 0 Oct 12 08:41 /var/log/netconf.log.4
-rw-r-x--x-- 1 root root 23795 Jan 24 09:55 /var/log/samba/log.nmb.4
-rw-r--r-- 1 root root 2300 Feb 4 21:48 /var/log/secure.4
-rw-r--r-- 1 root root 0 Jan 30 04:02 /var/log/spooler.4
-rw-r--r-- 1 uucp uucp 0 Jan 30 04:02 /var/log/uucp/Debug.4
-rw-r-x--x-- 1 uucp uucp 0 Jan 30 04:02 /var/log/uucp/log.4
-rw-f-x--x-- 1 uucp uucp 0 Jan 30 04:02 /var/log/uucp/Stats.4
-rw-r--r-- 1 root root 130101 Jan 31 14:20 /var/log/xferlog.4
```

如图所示，有些日志在一个月内可能会变得相当大！如果你不需要这些文件，可以安全地删除它们以释放磁盘空间。

## 结合自动化整合

Linux 不仅提供了查找和删除文件所需的工具，还提供了自动化此过程所需的软件。

通过使用 `cron` 守护进程和系统的 `crontab` 表，你可以设置 Linux 自动搜索并删除不需要的文件。以 root 身份登录，然后使用你最喜欢的编辑器打开 `/etc/crontab` 文件。你可能会看到类似这样的内容：

```
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

# run-parts
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```

`/etc/crontab` 文件包含给 `cron` 守护进程的指令，该守护进程在启动 Linux 时开始运行。此软件在后台运行，每分钟查看该文件以查找要运行的任务。

在这个例子中，`cron` 守护进程每小时整点查看 `/etc/cron.hourly` 目录。每天凌晨 4:02，它会查看 `/etc/cron.daily` 中的任务。每个周日凌晨 4:22，它会运行 `/etc/cron.weekly` 目录中的任务。每月 1 号凌晨 4:42，守护进程运行列在 `/etc/cron.monthly` 中的任务。

如果你对时间和安排满意，创建你的命令，例如将 `find` 命令的输出与 `xargs` 和 `rm` 命令结合，并将其放入文本文件中。接下来，为该文件命名并使其可执行。例如：

```
chmod +x cleanup
```

然后将文件移动到每日、每周或每月目录。例如，要清理系统日志，你可以使用以下内容：

```
/usr/bin/find /var/log -name *\*.1 | /usr/bin/xargs /bin/rm -f
```

若要使其在每月 15 日下午 2:30 运行，你可以使用如下的 `/etc/crontab` 条目：

```
30 14 15 * * root /usr/bin/find /var/log -name *\*.1 | /usr/bin/xargs /bin/rm -f
```

## 压缩和压缩文件系统

计算机数据的压缩不仅是一种科学追求，也是一种艺术形式。甚至在计算机发明之前，人们就一直在努力寻找更好的方式来压缩数据。象形文字和楔形文字字母表可以被视为早期和原始的压缩信息形式。电报时代从战场报道的记者使用压缩语言，以便尽可能多地容纳信息，并将最重要的信息放在开头，以防传输中断。

今天，当我们通过调制解调器上网、收听流式音频或视频，或使用 Web 浏览器上传或下载文件（浏览器可以设置为实时解压文件）时，压缩被无形地使用。Linux 内核自 1997 年以来就具有使用内置压缩的能力，但由于时间和硬盘活动增加的额外开销，这种形式的文件系统活动并未在流行发行版中流行起来。

### 想要尝试压缩的挤压？

勇敢的笔记本用户如果希望或需要利用压缩功能，可以从以下地址下载 `e2compr` 内核补丁：

```
http://www.netinspace.net/-reiter/e2compr/
```

你需要应用内核补丁，然后使用包含的工具来压缩和解压你在 Linux 中使用的文件。

### Linux 中的压缩使用

你在笔记本上安装的 Linux 发行版包含许多用于压缩和解压文件的实用程序。本节向你介绍 Linux 的压缩工具。这些工具，像大多数其他命令行实用程序一样，可以与其他程序结合使用或包含在 shell 脚本中，以自动处理 Linux 会话中的文件压缩。

> **手册页压缩**
>
> 几乎所有的 Linux 发行版现在都使用压缩的手册页。这些页面可以在 `/usr/man` 目录下的文件中找到，可以通过 `/etc/man.config` 文件中指定的实用程序进行解压。如果没有使用压缩，这些文档页面将需要 100MB 或更多的驱动器空间。

表 8.2 列出了 Linux 中包含的一些压缩工具。你可能会（或不会）对一些老朋友感到惊讶。

### 提取存档

在下载新软件或打包为源代码的软件时，你很可能会遇到压缩文件。虽然 Red Hat、Mandrake、Caldera OpenLinux 和 SUSE Linux 的标准软件包管理软件是 Red Hat 软件包管理器，即 `rpm` 命令，但许多不同的 Linux 软件开发者分发已知为 *tarballs* 的压缩存档文件。这些文件很容易识别，扩展名如 `.tar.gz` 和 `.tgz`。

使用 `gunzip`、`gzip` 或 `tar` 命令解压这些文件非常简单。例如，如果你下载了一个具有 `.tar.gz` 扩展名的文件，你可以首先使用 `gunzip` 命令解压文件，如下所示：

```
$ gunzip xp2.tar.gz
```

你会得到一个名为 `xp2.tar` 的文件。然后你可以使用 `tar` 的 `-t`（列表）选项列出存档的内容：

```
$ tar tf xp2.tar
...
usr/
usr/X11R6/
usr/X11R6/bin/
```

