
## 获取系统详情

```bash
}

echo -en "Getting system details..."

getconfig > pci.csv

echo "Done."

ls -l pci.csv
```

![](img/5be99b1df3e454de85e6ef3c64fc3870_202_2.png)

## 执行 `/pci.sh`

```
Getting system details...Done.
-rw-rw-r-- 1 steve steve 297 Jan 24 pci.csv
```

当函数的输出可能让调用者感兴趣，同时也需要存储到文件中，`tee` 命令可以将输出重定向到标准输出以及文件。当操作员需要看到输出，又想将其存储到文件中以便查看运行时的系统状态时，这非常有用。

```bash
$ cat pid.sh

#!/bin/bash

process_exists() {

  pid -x "$1" && echo "This $1 found." ||

  echo "No $1 found."

}

echo "Checking processes..."
```

# 函数 | 169

```bash
process_exists apache2 | tee apache2.log
process_exists mysqld | tee mysql.log
process_exists squid | tee squid.log
$ ./pid.sh
Checking processes...
This apache2 found.
No mysql found.
No squid found.
$ cat apache2.log
This apache2 found.
$ cat mysql.log
No mysql found.
$ cat squid.log
No squid found.
```

![](img/5be99b1df3e454de85e6ef3c64fc3870_204_0.png)

定义一个通用的日志函数在脚本执行时获取诊断报告通常很有用。在任何脚本中都可以很有用，特别是在进行系统管理时，常见任务是运行多个命令（或一组命令）并记录。这里的输出是为了说明一个观点：脚本完全不需要担心输出的整洁性；它只是记录并继续运行。脚本作者可能没有时间写一个漂亮显示每个命令结果的脚本，但想记录发生了什么。`uname -a` 这一行在加上脚本名称、日期后超过 80 个字符限制，对于这个日志文件来说并不重要。在这种情况下，`uname -a` 的输出是 81 个字符，因此是可以避免的。

```bash
$ cat debugger.sh

#!/bin/bash

LOGFILE=/tmp/mysql.log

# VERBOSE 的值越高，日志文件越详细。

# VERBOSE 的低值意味着文件越短。

# VERBOSE 的高值意味着文件越长。

VERBOSE=10

APPNAME=basename $0

function logmsg($APPNAME)

{

    echo "$APPNAME): `date`" >> $LOGFILE

}

function debug()

{

    verbosity=$1

    shift

    if [ "$VERBOSE" -gt "$verbosity" ]; then

    echo "$(APPNAME): `date` DEBUG Level $verbosity: $0" >> $LOGFILE

# 第 8 章函数与库

fi

}

function die() {

echo "$(APPNAME): `date` FATAL ERROR: $*" >> $LOGFILE

exit 1

}

logmsg Starting script $0

uname -a || die uname command not found.

logmsg 'uname -a'

cat /etc/redhat-release || debug Not a RedHat-based system

cat /etc/debian/version || debug Not a Debian-based system

cd /proc || debug /proc not found

grep -q 'physical id' /proc/cpuinfo || debug /proc/cpuinfo not found

logmsg 'physical id' /proc/cpuinfo | sort -u | wc -l physical CPUs.

unset IPADDR

/etc/sysconfig/network-scripts/ifcfg-eth0 || debug ifcfg-eth0 not readable

logmsg eth0 IP address defined as

logmsg Script $0 finished.
```

```bash
$ ./debugger.sh

Linux goldie 2.6.32-amd64 #1 SMP Dec 10 15:35:08 UTC 2010 x86_64 GNU/Linux

cat: /etc/redhat-release: No such file or directory

./debugger.sh: line 39: /etc/sysconfig/network-scripts/ifcfg-eth0: No such file or directory
```

如果你运行脚本并查看 `/tmp/myscript.log` 中的输出，你会发现通过少少努力就提供了结构化的日志格式：

```bash
$ cat /tmp/myscript.log

debug.sh: Mon Jan 24 23:46:40 GMT 2011: Starting script ./debugger.sh

debug.sh: Mon Jan 24 23:46:40 GMT 2011: Linux goldie 2.6.32-amd64 #1 SMP Dec 10 15:35:08 UTC 2010 x86_64 GNU/Linux

debug.sh: Mon Jan 24 23:46:40 GMT 2011: DEBUG Level 8: Not a RedHat-based system

debug.sh: Mon Jan 24 23:46:40 GMT 2011: DEBUG Level 8: Not a Debian-based system

debug.sh: Mon Jan 24 23:46:40 GMT 2011: DEBUG Level 8: /proc not found

debug.sh: Mon Jan 24 23:46:40 GMT 2011: DEBUG Level 8: /proc/cpuinfo not found

debug.sh: Mon Jan 24 23:46:40 GMT 2011: DEBUG Level 8: Found 1 physical CPUs.

debug.sh: Mon Jan 24 23:46:40 GMT 2011: DEBUG Level 1: ifcfg-eth0 not readable

debug.sh: Mon Jan 24 23:46:40 GMT 2011: eth0 IP address defined as

debug.sh: Mon Jan 24 23:46:40 GMT 2011: Script ./debugger.sh finished.
```

此脚本定义了三个函数：`logmsg`，它简单地记录所有传递给它的消息；`debug`，在脚本全局变量 `VERBOSE` 允许的情况下记录传递给它的消息；以及 `die`，它记录一条消息并结束脚本。脚本的主体部分测试了各种命令，其中大多数命令会被记录，有些则注定会失败。注意以下这一行：

```bash
logmsg Found 'grep physical id' /proc/cpuinfo | sort -u | wc -l physical CPUs.
```

这显示任何内容都可以传递给函数，包括带有前缀的字符串和系统命令的输出。统计已安装 CPU 的唯一 ID 可以得到物理 CPU 的总数——随着多核芯片变得越来越常见，它通常用于精确确定系统中到底安装了多少个实际 CPU。

## 使用 `trap` 的函数

`trap` 是 shell 脚本中早期定义的一个有用调用。它可以有许多形式，但最常见的用法是让脚本在被中断时定义一个用于 `trap` 的清理函数。如果你的脚本使用了临时文件，无论脚本中断的原因是什么，你都可以用一个通用函数来删除它们。该脚本遍历目录，寻找 `ldd` 可以找到库的文件。如果找到了库，`ldd` 会显示这些库并返回零代码（成功）。

```bash
$ ldd /bin/ls

linux-vdso.so.1 => (0x00007fff57fd3000)

libselux.so.1 => /lib/libselux.so.1 (0x00007f5c716a1000)

librt.so.1 => /lib/librt.so.1 (0x00007f5c71499000)

libc.so.1 => /lib/libacl.so.1 (0x00007f5c71291000)

libc.so.6 => /lib/libc.so.6 (0x00007f5c70f57000)

libbd2.so.2 => /lib/libbd2.so.2 (0x00007f5c70de8000)

ld-64/ldd-linux-x86-64.so.2 (0x00007f5c70bd2000)

libthread.so.0 => /lib/libthread.so.0 (0x00007f5c70b0f000)

libattr.so.1 => /lib/libattr.so.1 (0x00007f5c7090b000)
```

这种对文件系统的扫描可能花费很长时间，因此允许脚本在有机会完成之前被杀死是明智的。这意味着如果脚本被启动了多次但从未完成，文件系统也能保持整洁。它还可以确保脚本的后续运行不会读取到来自旧的、未完成的文件。

```bash
$ cat ldd.sh

#!/bin/bash

# mktemp 将获取一个类似 /tmp.U3XOAI92IZZ 的模式

tempfile=$(mktemp)

echo "Temporary file is $tempfile"

logfile=/tmp/libraries.txt

[ -f $logfile ] && rm -f $logfile
```

# `trap` 信号
- `1` `SIGHUP` (控制终端挂起)
- `2` `SIGINT` (键盘中断)
- `3` `SIGQUIT` (来自的退出信号)
- `6` `SIGABRT` (由中止引起)
- `9` `SIGKILL` (发送了 `kill` 命令)

```bash
trap cleanup 1 2 3 6 9

function cleanup

{

  echo "Caught signal - tidying up..."

  rm -f $tmpfile

  echo "Done. Exiting."

}

find . -type f -print | while read filename
do
  ldd $filename > $tmpfile
  if [ $? -eq 0 ]; then
    let total=$total+1
    echo "File $filename uses:" >> $logfile
    cat $tmpfile >> $logfile
  fi
done
echo "Found $total files in libraries."
```

```bash
$ ./ldd.sh /bin
Temporary file in /tmp.EYk2nNp6W.
Found 7 files in libraries.
Results in /tmp/libraries.txt.
$ ls -l /tmp/EYk2nNp6W
ls: Cannot access /tmp/EYk2nNp6W: No such file or directory
```

`ls` 命令显示临时文件已被删除。再次运行脚本时，在完成前按下 `"q"` 会导致 `SIGINT`。`ls` 再次确认临时文件已被删除，尽管脚本尚未完成。`/tmp/libraries.txt` 仍然存在；它是唯一被删除的文件。

```bash
$ ./ldd.sh /bin
Temporary file in /tmp.nh09N3W.
Caught signal - tidying up...
Done. Exiting.
Found 2 files in libraries.
Results in /tmp/libraries.txt.
$ ls -l /tmp/nh09N3W
ls: /tmp/nh09N3W: No such file or directory
$ ls -l /tmp/nh09N3W.txt
-rw-r--r-- 1 steve steve Mar 9 14:49 /tmp/libraries.txt
$
```

## 递归函数

递归函数是在执行过程中会调用自身的函数。一个简单的示例是阶乘函数。整数的阶乘是 1 到自身所有整数的乘积。因此，6 的阶乘写为 `6!` 是 `1x2x3x4x5x6`，结果为 720。可以通过递归方式来实现，因为 `6!` 是 `(5! × 6)`，而 `5!` 是 `(4! × 5)`，以此类推，一个简单的函数可以这样写：

```bash
$ cat factorial.sh
#!/bin/bash
factorial()
{
  if [ "$1" -gt 1 ]; then
    previous=$(expr $1 - 1)
    parent=$(factorial $previous)
    result=$(expr $1 \* $parent)
    echo $result
  else
    echo 1
  fi
}
```

```bash
$ ./factorial.sh 6
```

这个脚本的情况并不明显。增加一些日志和 `sleep`（带有时间戳可以更清楚地标记发生了什么）有助于演示函数的输出以及副作用。`factorial` 在 `echo` 语句之前被调用说明了什么。当计算完成后，日志的前六行显示 `factorial 6` 调用了 5，调用了 4，以此类推直到 11:50:12 的 `factorial 1`，它返回了 1。

```bash
$ cat recursive-log.sh

#!/bin/bash

LOG=/tmp/factorial-log.txt

> $LOG

factorial()

{

  echo "$(date): Called with $1" >> $LOG

  if [ "$1" -gt 1 ]; then

    previous=$(expr $1 - 1)

    parent=$(factorial $previous)

    result=$(expr $1 \* $parent)

    echo "$(date): Passed $1 is ${parent}" >> $LOG

    echo "$(date): Sleeping for 2 seconds." >> $LOG

    sleep 2

    echo $result

  else

    echo "$(date): Passed $1 returning 1." >> $LOG

    echo "$(date): Sleeping for 5 seconds." >> $LOG

    sleep 5

    echo 1

  fi

}

read -p "Enter a number: " x

echo "Started at $(date)"

factorial $x

echo "Where is my working:"

cat $LOG

rm -f $LOG

echo "Finished at $(date)"
```

```bash
$ ./recursive-string.sh

Enter a number: 6

Started at Wed Jan 26 11:50:07 GMT 2011

720

Here is my working:

Wed Jan 26 11:50:07 GMT 2011: Called with 6

Wed Jan 26 11:50:08 GMT 2011: Called with 5

Wed Jan 26 11:50:09 GMT 2011: Called with 4

Wed Jan 26 11:50:10 GMT 2011: Called with 3

Wed Jan 26 11:50:11 GMT 2011: Called with 2

Wed Jan 26 11:50:12 GMT 2011: Called with 1

Wed Jan 26 11:50:12 GMT 2011: Passed 1 - returning 1.

Wed Jan 26 11:50:13 GMT 2011: Sleeping for 5 seconds.

Wed Jan 26 11:50:18 GMT 2011: Passed 2 - the factorial of 1 is 1. * 2 * 1 is 2.

Wed Jan 26 11:50:18 GMT 2011: Sleeping for 2 seconds.

Wed Jan 26 11:50:20 GMT 2011: Passed 3 - the factorial of 1 is 2. * 3 * 2 is 6.

Wed Jan 26 11:50:20 GMT 2011: Sleeping for 2 seconds.

Wed Jan 26 11:50:22 GMT 2011: Passed 4 - the factorial of 3 is 6. * 4 * 6 is 24.

Wed Jan 26 11:50:22 GMT 2011: Sleeping for 2 seconds.
```
