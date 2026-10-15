

## 使用 du 确定磁盘使用情况

另一个你可以获取的信息是 Unix 系统中磁盘空间的使用情况。你可以使用 du 来做到这一点，如代码清单 7.5 所示：

### 使用 du 确定磁盘使用情况：
- du

在 shell 提示符下，输入 du。如代码清单 7.5 所示，你将获得有关当前目录以及所有子目录的磁盘使用信息。数字通常以 1 Kbyte 块为单位进行测量（如 df 所述）。你实际上可以通过使用 du -h 来读取输出。

### 提示
- 如果你在一个执行磁盘空间配额的系统上（大多数 ISP 都是如此），你可以找出你的配额是多少以及你离达到配额有多近。只需在 shell 提示符下输入 quota -v 即可。
- 你可以使用 du 加上路径名来检查单个目录或子目录中的磁盘使用情况（参见代码清单 7.6）。du 会在打印结果时按子目录汇总使用情况。
- 使用 du -s，可选择指定目录，只打印所用空间量的摘要。

```
[ejr@hobbes ejr]$ du
2 ./Mail
1 ./nsmail
1 ./netscape/cache/0F
3 ./netscape/cache/1A
22 ./netscape/cache
1 ./netscape/archive
172 ./netscape
1 ./Projects
28 ./wprc
3 ./axhome
5 ./groups
1 ./manipulate/empty
154 ./manipulate
1 ./mail
1 ./unixvqs/ch6
2 ./unixvqs
6 ./dupgroups
255 ./compression/Folder
670 ./compression/temp/BackupFolder
1921 ./compression/temp
670 ./compression/BackupFolder
4657 ./compression
5 ./clean
1 ./elm
15 ./editors
5619 .
[ejr@hobbes ejr]$
```

代码清单 7.5 du 命令会详尽地报告当前目录及其子目录中的磁盘使用情况。

```
[ejr@hobbes ejr]$ du /home/ejr/compression
255 /home/ejr/compression/Folder
670 /home/ejr/compression/temp/BackupFolder
1921 /home/ejr/compression/temp
670 /home/ejr/compression/BackupFolder
4657 /home/ejr/compression
[ejr@hobbes ejr]$
```

代码清单 7.6 使用 du 并指定目录名可以得到更有针对性的结果。

## 使用 file 查找文件类型

如果你来自 Windows、Macintosh 或 DOS 背景，你可能习惯于访问文件并能够看到它们是什么类型的文件——HTML 文件、GIF、文档或任何其他类型。在 Unix 中，通过列出文件或显示目录内容通常无法判断文件类型。这时 file 就派上用场了，如代码清单 7.7 所示。

### 使用 file 识别文件类型：
- file /usr/bin/pico
在 shell 提示符下，输入 file，后跟路径（如果必要）和文件名。你会看到与代码清单 7.7 中类似的输出。

### 提示
- 并非所有文件都具有使 file 正常工作的“魔术”信息，但大多数都有。在没有的情况下，你会得到一个最佳猜测的响应，就像代码清单 7.7 中的第二个响应一样。不幸的是，你无法通过查看来判断它是确定信息还是猜测，但如果它很简略（如第二个响应），请谨慎对待。

```
[ejr@hobbes ejr]$ file /usr/bin/pico
/usr/bin/pico: ELF 32-bit LSB executable,
  Intel 80386, version 1, dynamically ld
[ejr@hobbes ejr]$ file temp.htm
temp.htm: ASCII text
[ejr@hobbes ejr]$
```

代码清单 7.7 file 命令提供了有关特定文件中包含何种数据的有用信息。

## 使用 finger 查找用户信息

使用 finger 命令，你可以查出当前谁登录到 Unix 系统，以及他们在做什么、登录了多久，以及其他一些窥探性的、可能与你无关的信息（代码清单 7.8）。

### 使用 finger 查找谁已登录：
1. `finger`
   在 shell 提示符下，输入 `finger` 以查看还有谁登录到系统并获取有关他们的一些信息（代码清单 7.8）。
2. `finger @stc.org`
   输入 `finger @`，后跟主机名（在本例中为 stc.org）以查找另一个主机上谁已登录。
   根据其他主机计算机的安全设置，查询不同主机并不总是有效。如果主机不允许，你会收到类似代码清单 7.8 中的消息。

```
[ejr@hobbes ejr]$ finger
Login       Name       Tty   Idle   Login Time   Office   Office Phone
asr                              *4     1          Jul 24 13:32
deb                              5      1          Jul 24 13:32
ejr         Eric J. Ray 1       3:20       Jul 22 07:42
ejr         Eric J. Ray p1      1:12       Jul 24 12:14 (calvin)
ejr         Eric J. Ray p0                 Jul 24 13:02 (calvin)
root                             *2     1d         Jul 25 15:13
[ejr@hobbes ejr]$ finger @stc.org
[stc.org]
No one logged on
[ejr@hobbes ejr]$ finger @osunwx.ucc.okstate.edu
[osunwx.ucc.okstate.edu]
finger: connect: Connection refused
[ejr@hobbes ejr]$
```

**代码清单 7.8** finger 命令通常会提供有关谁登录到不同系统的有趣信息。

