

## 目录（续）

- 在指定时间执行命令 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 95
- 与另一位用户共享您的屏幕会话 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 96
- 执行别名的非别名版本命令 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 98
- 将命令输出保存为图像 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 98
- 关于作者 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 100
- 作者的其它书籍 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 101
- 作者的其它课程 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 102
- 索引 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 103
- 附录 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 114
- 商标 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 114

## 您的免费礼物

感谢您阅读《Command Line Kung Fu》（命令行功夫），我想送您一份《Linux 应用程序对 Windows 的替代方案》的副本。书中介绍了目前 Linux 上 50 多种最流行的应用程序。这些应用程序允许您浏览网页、观看电影、收听音乐、连接您喜爱的社交网络、制作演示文稿等等。这份礼物是本的最佳补充，将帮助您在 Linux 的学习之路上更进一步。访问 [http://www.linuxtrainingacademy.com/linux-apps](http://www.linuxtrainingacademy.com/linux-apps) 下载您的免费礼物。

## 引言

自 20 世纪 90 年代以来，我我一直在 Unix 和 Linux 系统的命令行上工作。不用说，除了一个美元符号（`$`）和一个闪烁的光标对着我之外，我对此感到如鱼得水。多年来，我学会了几个命令行“技巧”，它们为我节省了时间和烦恼。

其中一些技巧源于必要性——我手头的工作太多，而时间太少。另一些则借鉴了计算机编程和应用程序开发中的流行模式。剩下的则是由我的命令行偶像和导师直接或间接分享给我的。通过观察、模仿并向经验丰富的 Unix 和 Linux 专业人士寻求建议，您能学到惊人的东西。

尽管书名是《Command Line Kung Fu》（命令行功夫），但您不需要成为 Linux 忍者就能使用本书介绍的策略。这些技巧可以直接使用。您可以立即开始应用它们，而无需完全理解所有细节和细微差别。然而，如果您想要或需要更多信息，每个技巧后面都附有解释和实际现实世界示例。

另外，如果您想看看这些命令的实际操作，请访问 [http://www.linuxtrainingacademy.com/fu](http://www.linuxtrainingacademy.com/fu)。在那里，您会找到一系列视频，演示本书中涵盖的一些命令。

最后，如果您想要 Linux 命令行和操作系统概览，请阅读我的另一本书《Linux 入门》。它将为您提供坚实的基础，以便您构建您的 Linux 技能。

让我们开始吧。

## Shell 历史记录

### 以 Root 身份运行最后一个命令

```bash
$ sudo !!
$ su -c "!!"
```

如果您忘记以 root 权限运行某个命令，可以使用 `sudo !!` 或 `su -c "!!"` 简单地重复该命令。

```bash
$ adduser sam
-bash: /usr/sbin/adduser: Permission denied
$ sudo !!
sudo: adduser sam
$ id sam
uid=1007(sam) gid=1007(sam) groups=1007(sam)
$ userdel -r sam
-bash: /usr/sbin/userdel: Permission denied
$ sudo !!
sudo userdel -r sam
$ id sam
id: sam: No such user
$ useradd jim
-bash: /usr/sbin/useradd: Permission denied
$ su -c "!!!"
su -c "useradd jim"
Password:
$ id jim
uid=1007(jim) gid=1007(jim) groups=1007(jim)
```

这种感叹号语法被称为事件标识符（event designator）。事件标识符引用 shell 历史中的一个命令。Bang-Bang (`!!`) 重复最近的命令，但我对事件标识符最喜欢的用法之一是运行以特定字符串开始的最近命令。下面是一个例子。

```bash
$ whoami
jason
$ uptime
12:33:15 up 35 min, 1 user, load average: 0.00, 0.00, 0.00
$ df -hT /boot
Filesystem Type Size Used Avail Use% Mounted on
/dev/vda1 ext4 485M 55M 406M 12% /boot
$ !u
uptime
12:33:29 up 35 min, 1 user, load average: 0.00, 0.00, 0.00
$ sudo !w
sudo whoami
root
```

### 重复以给定字符串开头的最后一个命令

```bash
$ !<string>
```

这是另一个事件标识符的例子。要调用以 `<string>` 开始的最近命令，请运行 `!<string>`。您可以简单地指定第一个字母，或者指定字符串中足以使其唯一的任何部分。此示例演示了该概念。

```bash
$ who
jason    pts/1    2014-04-06 21:04 (192.168.1.117)
$ w
jason    pts/1    192.168.1.117 21:04 0.00s
0.33s 0.00s w
$ !w
w
jason    pts/1    192.168.1.117 21:04 0.00s
0.33s 0.00s w
$ !wh
who
jason    pts/1    2014-04-06 21:04 (192.168.1.117)
```

这是一个实用示例，其中您检查某个进程是否正在运行，将其终止，并确认它确实已停止。

```bash
$ ps -fu apache
UID  PID  PPID C STIME TTY TIME CMD
apache 1877 1879 0 21:32 ? 00:00:00
/usr/sbin/httpd
apache 1879 1 0 21:32 ? 00:00:00
/usr/sbin/httpd
$ sudo service httpd stop
Stopping httpd: [ OK ]
$ !fp
ps -fu apache
UID PID PPID C STIME TTY TIME CMD
$
```

### 重用前一条命令中的第二个单词（第一个参数）

```bash
$ !^
```

如果您需要获取前一条命令中的第二个单词，可以使用 "!^" 单词标识符。任何使用 "!^" 的地方都将被前一条命令中的第二个单词替换。您也可以将其视为前一条命令的第一个参数。

```bash
$ host www.google.com 8.8.8.8
Using domain server:
Name: 8.8.8.8
Address: 8.8.8.8#53
Aliases:
www.google.com has address 173.194.46.83
www.google.com has address 173.194.46.81
www.google.com has address 173.194.46.84
www.google.com has address 173.194.46.82
www.google.com has address 173.194.46.80

www.google.com has IPv6 address
2607:f8b0:4009:805::1013

$ ping -cl !^
ping -cl www.google.com
PING www.google.com (173.194.46.80) 56(84) bytes of data.
64 bytes from ord08s11-in-f16.l.google.net
(173.194.46.80): icmp_seq=1 ttl=51 time=17.0 ms
--- www.google.com ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 49ms

rtt min/avg/max/mdev = 17.071/17.071/17.071/0.000 ms
$
```

### 重用前一条命令中的最后一个单词（最后一个参数）

```bash
$ !$
```

我经常发现需要在前一条命令行上的最后一项上执行另一个操作。要在当前命令中访问该项，请使用 '!$'。

```bash
$ unzip tpstreport.zip
Archive: tpstreport.zip
inflating: cover-sheet.doc
$ rm !$
rm tpstreport.zip
$ mv cover-sheet.doc reports/
$ du -sh !$
du -sh reports/*
4.7G  reports/
$
```

### 重用前一条命令中的第 N 个单词

```bash
$ !!!:N
$ <event_designator>:<number>
```

要访问前一条命令中的单词，请使用 `!!:N`，其中 N 是您想要获取的单词编号。第一个单词是 0，第二个单词是 1，依此类推。您可以将 0 视为命令本身，1 视为命令的第一个参数，2 视为第二个参数，等等。

您可以将任何事件标识符与单词标识符结合使用。在下面的示例中，`!!` 是最近的命令行：`avconv -i screencast.mp4 podcast.mp3`。`!a` 事件标识符扩展为相同的命令，因为它是以字母 “a” 开头的最近命令。

```bash
$ avconv -i screencast.mp4 podcast.mp3
$ mv !!:2 converted/
mv screencast.mp4 converted/
$ mv !a:3 podcasts/
mv podcast.mp3 podcasts/
$
```

### 重复前一条命令并替换字符串

```bash
$ ^<string1>^<string2>^
```

这个小技巧非常适合快速纠正打字错误。如果您省略 `^<string2>^`，则 `<string1>` 将从前一条命令中移除。By

