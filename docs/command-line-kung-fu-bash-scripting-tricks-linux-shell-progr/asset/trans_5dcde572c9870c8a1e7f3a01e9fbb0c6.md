

# 按 CPU 使用率排序列出进程

```
$ ps aux | sort -nk 3
```

使用此命令可以查找正在消耗最多 CPU 的进程。CPU 使用率最低的进程会从屏幕顶部滚出，而 CPU 使用率最高的进程将显示在你的 shell 提示符上方。

在本例中，mysqld 正在消耗该主机 94% 的 CPU。

```
$ ps aux | head -1
USER   PID %CPU %MEM      VSZ   RSS TTY STAT
START TIME COMMAND

$ ps aux | sort -nk 4 | tail -5
root    2469  0.0   0.3  11856   3228 ?   Ss   17:16
0:00  /usr/sbin/fcoemon

root      452  0.0   0.3  20844   4084 ?   Ssl  00:00
0:00  master

root     5571  2.1   0.3  11364   3380 ?   Ss   17:52
0:00  /usr/sbin/httpd

mysql 4447  94.0 12.8 2134672 1031064 ?        Sl    10:52
0:27:39 /usr/libexec/mysqld
$
```

## 快速判断系统是 32 位还是 64 位

```
$ getconf LONG_BIT
```

如果你需要知道当前系统是 32 位还是 64 位，可以使用 getconf 命令。

```
$ getconf LONG_BIT
32
$ ssh remote-host getconf LONG_BIT
64
```

## 生成随机密码

```
$ openssl rand -base64 48 | cut -c1-PASSWORD_LENGTH
$ gpw () { openssl rand -base64 48 | cut -c1-${1}; }
```

你可以使用 openssl 命令来生成随机密码。如果你经常这样做，可以创建一个函数。只需传入你希望密码的长度即可。

```
$ echo 'gpw () {openssl rand -base64 48|cut -c1-$1};' >> ~/.bash_profile
$ . ~/.bash_profile
$ gpw
t3eyxXxBBx3Vdr7G8V3FMvvZpXLoV+AQwgQnw9pLm/UaRNHoPBjKaQsr26i3k
$ gpw 6
uu12M8
```

# 文件和目录

## 快速备份文件

```
$ cp file{,.bak}
```

你可以使用花括号扩展来快速创建文件的备份副本。花括号扩展允许你从单个参数创建多个命令行参数。该单参数会与花括号内给出的所有字符串组合，并创建与花括号字符串数量相同的新参数。花括号内的值可以是逗号分隔的字符串，也可以是序列表达式。序列表达式的示例包括 {1..5} 和 {a..z}。

```
$ sudo cp /etc/passwd{,.bak}
$ ls /etc/passwd*
/etc/passwd /etc/passwd.bak
$ mkdir -p ~/my-app/{bin,lib,log}
$ ls ~/my-app/
bin     lib     log
$ echo 10.0.0.{0..7}
10.0.0.0    10.0.0.1    10.0.0.2    10.0.0.3    10.0.0.4    10.0.0.5    10.0.0.6    10.0.0.7
```

## 快速更改文件扩展名

```
$ mv file{.old,.new}
```

要使用新扩展重命名文件，请采用花括号扩展。此示例将 “.txt” 文件更改为 “.doc” 文件。

```
$ ls report*
report.txt
$ mv report.{txt,doc}
$ ls report*
report.doc
$
```

这里还有另一个示例。

```
$ ls httpd*
httpd.cfg
$ mv httpd.{cfg,conf}
$ ls httpd*
httpd.conf
$
```

此命令会为文件添加一个扩展名。

```
$ ls jazz*
jazz
$ mv jazz{.,.mp3}
$ ls jazz*
jazz.mp3
$
```

## 轻松按日期创建文件备份

```
$ alias d='date +%F'
```

通过在文件或目录名称中使用 YYYY-MM-DD 的日期格式，你可以让 ls 的输出更便于人类阅读。使用这种格式时，你可以快速看出文件的日期顺序。

```
$ ls -l file*
file.2013-04-08
file.2013-12-21
file.2014-04-08
$ ls -l other-file.*
other-file.04-08-2013
other-file.04-08-2014
other-file.12-21-2013
```

在修改文件之前，我喜欢先制作一个备份副本。我还希望知道我是何时做的备份。通过创建一个名为 "d" 的别名，它代表 YYYY-MM-DD 格式的名称，我可以快速创建这类备份。

```
$ echo "alias d='date +%F'" >> ~/.bash_profile
$ . ~/.bash_profile
$ d
2014-04-09
$ sudo cp httpd.conf httpd.conf.$(d)
$ sudo cp httpd.conf !#.$(d)
$ sudo cp httpd.conf{,.${d}}
$ ls -l httpd.conf*
httpd.conf
httpd.conf.2014-04-08
```

## 覆盖文件内容

```
$ command > file
```

你可以使用大于号将某个命令的输出重定向到文件。单个大于号 (> ) 将标准输出重定向到文件，并覆盖（截断）文件的任何现有内容。如果文件不存在，它会创建一个。

```
$ grep bash /etc/passwd > users-that-use-bash
$ cat users-that-use-bash
root:x:0:0:root:/root:/bin/bash
jason:x:501:501:Jason:/home/jason:/bin/bash
oracle:x:1006:1006::/home/oracle:/bin/bash
bob:x:1000:1000:Bob Smith:/home/bob:/bin/bash
$
```

## 清空正在写入的文件

```
$ > file
$ cat /dev/null > file
```

要快速清零一个文件，你可以将空内容重定向到该文件。为什么不直接删除文件并重新创建它呢？如果你在删除文件时某个进程正持有该文件的打开句柄，该进程会继续持有文件句柄并继续写入该文件。只有当进程关闭文件句柄时，该文件占用的磁盘空间才会被释放。如果一个应用填满了 /var，而你删除了打开的日志文件，/var 仍然会是满的。如果你将空内容重定向到该文件，文件会被截断，应用可以继续向该文件写入数据。

```
$ sudo -s
# > /var/log/maillog
# ls -l maillog
-rw------- 1 root root 0 Apr 9 18:55 maillog
```

## 将字符串追加到文件

```
$ command >> file
```

双大于号 (>>) 将标准输出重定向到文件，并追加到任何现有内容之后。如果文件不存在，它会创建一个。

```
$ echo build new server >> todo.txt
$ cat todo.txt
build new server
$ echo add server to the load balancer >> todo.txt
$ cat todo.txt
build new server
add server to the load balancer
$
```

## 实时跟踪正在增长的文件

```
$ tail -f file
```

对于正在持续更新的文件（如日志文件），使用 tail -f 可以实时查看文件的更新。

```
$ tail -f /var/log/syslog
Apr 10 21:45:01 linwww1 CRON[31769]: (root) CMD (command -v debian-sal > /dev/null && debian-sal l l)
Apr 10 21:46:28 linwww1 whoopsie[1421]: online
Apr 10 21:47:37 whoopsie[1421]: last message repeated 2 times
Apr 10 21:55:01 linwww1 CRON[32548]: (root) CMD (command -v debian-sal > /dev/null && debian-sal l l)
Apr 10 22:05:01 linwww1 CRON[931]: (root) CMD (command -v debian-sal > /dev/null && debian-sal l l)
Apr 10 22:15:01 linwww1 CRON[2459]: (root) CMD (command -v debian-sal > /dev/null && debian-sal l l)
Apr 10 22:17:01 linwww1 CRON[2609]: (root) CMD ( cd / && run-parts --report /etc/cron.hourly)
Apr 10 22:25:01 linwww1 CRON[3197]: (root) CMD (command -v debian-sal > /dev/null && debian-sal l l)
Apr 10 22:35:01 linwww1 CRON[4036]: (root) CMD (command -v debian-sal > /dev/null && debian-sal l l)
Apr 10 22:35:33 linwww1 whoopsie[1421]: online
```

## 同时监视多个日志文件

```
$ multitail file1 fileN
$ multitail file1 -I fileN
```

multitail 命令允许你同时浏览多个文件。multitail 不仅允许你监视多个文件，还支持颜色高亮、过滤、合并等功能。以下是 multitail 中一些最有用命令的简要说明。

- F1 - 帮助
- a - 添加另一个文件进行跟踪
- d - 从视图中删除一个文件
- / - 开始搜索 (Find)
- ctrl-g - 退出命令、菜单或操作。类似于 emacs 的 ctrl-g 键位绑定。
- q - 退出

```
$ sudo multitail /var/log/syslog /var/log/kern.log
Apr 19 12:43:29 linuxsvr NetworkManager[758]: <info> (eth0): IP4 addrconf timed out or failed.
Apr 19 12:43:29 linuxsvr NetworkManager[758]: <info> Activation (eth0) Stage 4 of 5 (IPv4 Configure Timeout) scheduled...
Apr 19 12:43:29 linuxsvr NetworkManager[758]: <info> Activation (eth0) Stage 4 of 5 (IPv6 Configure Timeout) started...
Apr 19 12:43:29 linuxsvr NetworkManager[758]: <info> Activation (eth0) Stage 4 of 5 (IPv6 Configure Timeout) complete.
00] /var/log/syslog *Press <CTRL>+<h> for help*
132KB - 2014/09/19 12:46:45
Apr 19 12:43:08 linuxsvr kernel: [ 10.012891] Console: switching to colour frame buffer device 240x67
Apr 19 12:43:08 linuxsvr kernel: [ 10.012926] fb0: VESA VGA frame buffer device
Apr 19 12:43:11 linuxsvr kernel: [ 12.288420] hda-intel: Invalid position buffer, using LPB read
```

