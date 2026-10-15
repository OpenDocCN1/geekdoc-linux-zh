
```bash
# find -perm looks at the permissions of the file: 4000 and above
# are setuid/setgid.

find / -type f -perm +4000 -print0 | while read -d '' -r match
do
  if [ -x "$match" ] ; then
    # Let's split file owner and permissions from the ls -ld output.
    owner="$(ls -ld $match | awk '{print $3}')"
    perms="$(ls -ld $match | cut -c5-10 | grep 'w')"
    if [ ! -z $perms ] ; then
      echo "*** $match (writable and setuid $owner)"
    elif [ ! -z $(find $match -mtime -$mtime -print) ] ; then
      echo "*** $match (modified within $mtime days and setuid $owner)"
    elif [ $verbose -eq 1 ] ; then
      # By default, only dangerous scripts are listed. If verbose, show all.
      lastmod="$(ls -ld $match | awk '{print $6, $7, $8}')"
      echo "  $match (setuid $owner, last modified $lastmod)"
    fi
  fi
done

exit 0
```

清单 6-1：findsuid 脚本

### 工作原理

该脚本检查系统上的所有 setuid 命令，看它们是否对组或其他用户可写，以及是否在最近 $mtime 天内被修改过。为此，我们使用 find 命令，并通过参数指定要搜索的文件权限类型。如果用户要求详细输出，那么无论读写权限和修改日期如何，所有具有 setuid 权限的脚本都会被列出。

### 运行脚本

这个脚本有一个可选参数：`-v` 会产生详细输出，列出脚本遇到的每个 setuid 程序。这个脚本应以 root 身份运行，但也可以由任何用户运行，因为每个人通常对关键目录都有基本访问权限。

### 运行结果

我们在系统的某个地方放置了一个有漏洞的脚本。看看 findsuid 能否在清单 6-2 中找到它。

```text
$ findsuid
*** /var/tmp/.sneaky/editme (writable and setuid root)
```

清单 6-2：运行 findsuid shell 脚本并发现一个后门 shell 脚本

就是它（清单 6-3）！

```text
$ ls -l /var/tmp/.sneaky/editme
-rwsrwxrwx 1 root wheel 25988 Jul 13 11:50 /var/tmp/.sneaky/editme
```

清单 6-3：后门文件的 ls 输出，权限中的 `s` 表示该文件是 setuid

这是一个巨大的漏洞，正等着被人利用。幸好我们发现了！

## #46 设置系统日期

简洁是 Linux 及其 Unix 前身的核心精神，也深刻影响了 Linux 的演进。但在某些方面，这种简洁性会让系统管理员抓狂。最常见的烦恼之一就是重置系统日期时要求的格式，date 命令如下所示：

```text
usage: date [[[CC]YY]MM]DD[hh:mm[.ss]]
```

要弄明白所有这些方括号实在令人困惑，更不用说还要判断哪些内容需要指定、哪些不需要了。我们来解释一下：你可以只输入分钟；或者输入分钟和秒；或者输入小时、分钟和秒；或者在前面基础上再加上月份；还可以再加上年份甚至世纪。没错，就是这么疯狂！与其费劲去推算，不如使用一个像清单 6-4 那样的 shell 脚本，它会逐个字段提示输入，然后构造出紧凑的日期字符串。这绝对能让你保持清醒。

### 代码

```bash
#!/bin/bash
# setdate - Friendly frontend to the date command
# Date wants: [[[CC]YY]MM]DD[hh:mm[.ss]]

# To make things user-friendly, this function prompts for a specific date
#   value, displaying the default in [] based on the current date and time.

. library.sh  # Source our library of bash functions to get echon().
```

这是使用 date 命令时一个很微妙的问题。使用这个脚本时，如果你在提示过程中指定了精确时间，但之后不得不输入 sudo 密码，你最终可能会把系统时间设为几秒之前。这可能不是大问题，但这也是联网系统应该使用网络时间协议（NTP）工具、让系统与官方授时服务器同步的原因之一。你可以先阅读 Linux 或 Unix 系统中的 `timed(8)` 手册，开始了解网络时间同步。

### 运行脚本

注意，该脚本使用 sudo 命令来实际执行日期重置，如清单 6-5 所示。通过向 sudo 输入错误的密码，你可以试验这个脚本，而不必担心产生任何奇怪的结果。

### 运行结果

```text
$ setdate
year [2017] :
month [05] :
day [07] :
hour [16] : 14
minute [53] : 50

Setting date to 201705071450. You might need to enter your sudo password:

password $
```

## #47 按名称终止进程

Linux 和一些 Unix 系统有一个很有用的命令叫 killall，它允许你终止所有与指定模式匹配的运行中的应用程序。当你想要用 `kill -9` 强杀那些顽固的守护进程，或者只想向 xinetd 发送 SIGHUP 信号、促使其重新读取配置文件时，它会非常有用。没有 killall 的系统可以在 shell 脚本中模拟它：用 ps 识别匹配的进程，再用 kill 发送指定信号。

这个脚本最棘手的部分在于，ps 的输出格式在不同操作系统之间差异很大。例如，FreeBSD、Red Hat Linux 和 OS X 在默认 ps 输出中显示运行进程的方式就截然不同。

先来看 FreeBSD 的输出：

```text
BSD $ ps
PID TT STAT TIME COMMAND
792 0 Ss 0:00.02 -sh (sh)
4468 0 R+ 0:00.01 ps
```
