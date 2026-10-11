

# IDE 硬盘

你还可以添加其他四块 IDE 硬盘。它们对应 hde 到 hdh，每一块都可以拥有 1 到 16 号分区。

```
brw-r-----    1 root       disk        33,     0 Aug 18 1995 hde
brw-r-----    1 root       disk        33,    64 Aug 18 1995 hdf
brw-r-----    1 root       disk        34,     0 Aug 18 1995 hdg
brw-r-----    1 root       disk        34,    64 Aug 18 1995 hdh
```

# 网络设备文件

以下列表展示了 TCP/IP 网络设备的设备文件，以及核心 UNIX 网络（`/dev/inet` 和 `/dev/unix`）的设备文件。ICMP（即 `/dev/icmp`）是 TCP/IP 使用的消息网络（ping 命令使用 ICMP）。IP 设备（`/dev/ip`）是 TCP/IP 使用的寻址方式。传输层可以是 UDP 或 TCP（分别对应 `/dev/udp` 和 `/dev/tcp`）。

```
crw-------    1 root       root        18,     2 Feb 18 1994 icmp
drwxr-xr-x    2 root       root      1024 May  4 14:26 inet
crw-------    1 root       root        18,     1 Feb 18 1994 ip
crw-------    1 root       root        18,     3 Feb 18 1994 tcp
crw-------    1 root       root        18,     4 Feb 18 1994 udp
crw-------    1 root       root        17,     0 Feb 18 1994 unix
```

![](img/8ad518fddafc7f5e73715a2604b61d50_119_0.png)

有关网络的更多信息，请参阅第 11 章。

# INIT

此设备文件控制 init，即根进程。

```
brw-r-----    1 root       disk      1,   250 May 14 1996 initrd
```

![](img/8ad518fddafc7f5e73715a2604b61d50_119_1.png)

第 7 章解释了 init 进程。

# 内存访问

以下设备文件用于访问内存。设备 /dev/kmem（用于 xload 应用程序）是内核内存。其他设备文件对应 RAM（随机存取存储器）。

```
brw-r----- 1 root disk 1, 0 May 14 1996 ram0
brw-r----- 1 root disk 1, 1 May 14 1996 ram1
brw-r----- 1 root disk 1, 2 May 14 1996 ram2
brw-r----- 1 root disk 1, 3 May 14 1996 ram3
brw-r----- 1 root disk 1, 4 May 14 1996 ram4
brw-r----- 1 root disk 1, 5 May 14 1996 ram5
brw-r----- 1 root disk 1, 6 May 14 1996 ram6
brw-r----- 1 root disk 1, 7 May 14 1996 ram7
crw-r----- 1 root kmem 1, 1 Jul 17 1994 mem
crw-r----- 1 root kmem 1, 2 Jul 17 1994 kmem
```

# 回环接口

回环接口用于网络中，以确保网络连接正常工作。例如，可以使用回环地址来检查到某主机的 telnet 连接。Linux 中有八个回环接口。

```
brw-r--- 1 root root 7, 0 Jun 3 1996 loop0
brw-r--- 1 root root 7, 1 Jun 3 1996 loop1
brw-r--- 1 root root 7, 2 Jun 3 1996 loop2
brw-r--- 1 root root 7, 3 Jun 3 1996 loop3
brw-r--- 1 root root 7, 4 Jun 3 1996 loop4
brw-r--- 1 root root 7, 5 Jun 3 1996 loop5
brw-r--- 1 root root 7, 6 Jun 3 1996 loop6
brw-r--- 1 root root 7, 7 Jun 3 1996 loop7
brw-r--- 1 root root 7, 8 Jun 3 1996 loop8
```

# 打印机

有三个端口对应打印机：字符设备 lp0、lp1 和 lp2。为了让 Linux 连接打印机，它必须打开一个套接字。该套接字是 /dev/printer；实际的打印机设备是 /dev/lp0、/dev/lp1 和 /dev/lp2。

```
crw-rw---- 1 root daemon 6, 0 Apr 27 1995 lp0
crw-rw---- 1 root daemon 6, 1 Apr 27 1995 lp1
crw-rw---- 1 root daemon 6, 2 Apr 27 1995 lp2
srwxrwxrwx 1 root root 0 Jun 16 20:25 printer
```

# 鼠标

你的鼠标链接到在设置中选定的设备文件。该文件可以代表串行设备（如 ttyS0 到 ttyS3），或者代表兼容 PS/2 的鼠标，在这种情况下，鼠标通过符号链接指向 PS/2 设备（在下面的代码片段中，/dev/psaux 就是一个这样的设备）。

```
lrwxrwxrwx   1 root   root               5 May  4 14:49 mouse -> psaux
crw-rw-rw-   1 root   sys             10,   1 Jul 17  1994 psaux
```

# 伪终端

*pty 设备是伪终端，它们可以从实际终端设备扩展出来以创建新的终端。*

```
crw-rw-rw-   1 root   tty               2, 176 May 20  1996 ptya0
crw-rw-rw-   1 root   tty               2, 177 May 20  1996 ptya1
crw-rw-rw-   1 root   tty               2, 178 May 20  1996 ptya2
crw-rw-rw-   1 root   tty               2, 179 May 20  1996 ptya3
crw-rw-rw-   1 root   tty               2, 180 May 20  1996 ptya4
crw-rw-rw-   1 root   tty               2, 181 May 20  1996 ptya5
crw-rw-rw-   1 root   tty               2, 182 May 20  1996 ptya6
crw-rw-rw-   1 root   tty               2, 183 May 20  1996 ptya7
```

# SCSI 驱动器

*/dev/sd[a-h]* 文件是 SCSI 驱动器。对于系统管理员而言，这些驱动器与 IDE 硬盘（*/dev/hd[a-n]*）相似：可用八块驱动器，每块都有相同数量的可能分区（16 个）。尽管实际的 SCSI 和 IDE 硬件在功能上有着熟悉的差异，但操作系统实际上无需区分它们（除了将 */dev/sda4* 保留给 Iomega Zip 驱动器）。请考虑以下列表：

```
brw-r-----   1 root   disk               8,   0 Apr 29  1995 sda
brw-r-----   1 root   disk               8,   1 Apr 29  1995 sda1
brw-r-----   1 root   disk               8,   2 Apr 29  1995 sda2
brw-r-----   1 root   disk               8,   3 Apr 29  1995 sda3
brw-r-----   1 root   disk               8,   4 Apr 29  1995 sda4
brw-r-----   1 root   disk               8,  16 Apr 29  1995 sdb
brw-r-----   1 root   disk               8,  17 Apr 29  1995 sdb1
brw-r-----   1 root   disk               8,  18 Apr 29  1995 sdb2
brw-r-----   1 root   disk               8,  19 Apr 29  1995 sdb3
brw-r-----   1 root   disk               8,  20 Apr 29  1995 sdb4
brw-r-----   1 root   disk               8,  32 Apr 29  1995 sdc
brw-r-----   1 root   disk               8,  33 Apr 29  1995 sdc1
brw-r----  1 root  disk     8, 34 Apr 29 1995 sdc2
brw-r----  1 root  disk     8, 35 Apr 29 1995 sdc3
brw-r----  1 root  disk     8, 36 Apr 29 1995 sdc4
brw-r----  1 root  disk     8, 48 Apr 29 1995 sdd
brw-r----  1 root  disk     8, 49 Apr 29 1995 sdd1
brw-r----  1 root  disk     8, 50 Apr 29 1995 sdd2
brw-r----  1 root  disk     8, 51 Apr 29 1995 sdd3
brw-r----  1 root  disk     8, 52 Apr 29 1995 sdd4
brw-r----  1 root  disk     8, 64 Apr 29 1995 sde
brw-r----  1 root  disk     8, 65 Apr 29 1995 sde1
brw-r----  1 root  disk     8, 121 Apr 29 1995 sdh9
```

# 套接字

套接字用于创建到另一个网络或设备的连接。

```
crw-------  1 root  root    16,  0 Feb 18 1994 socket
crw-r--r--  1 root  root    30,  0 Aug 13 1995 socksys
```

# 输入/输出

在 Linux 编程中，你有两种输出形式和一种输入形式的命令。两种输出形式是标准输出（stdout）和标准错误（stderr）。标准输出是你在屏幕上看到的内容，前提是所有运行都顺利。标准错误可能会也可能不会显示在你的屏幕上，这取决于程序员如何定义它。

标准输入（stdin）是用户在使用程序时创建的输入。例如，在文字处理器中，标准输入对应你输入的文字；标准输出包括你在屏幕上看到的输入文字，以及你在执行保存文档等操作时在程序中激活的命令。然而，你可能看不到任何标准错误消息，且程序可能会在你毫无警告的情况下关闭。

```
lrwxrwxrwx  1 root  root  4 May 4 14:25 stderr -> fd/2
lrwxrwxrwx  1 root  root  4 May 4 14:25 stdin -> fd/0
lrwxrwxrwx  1 root  root  4 May 4 14:25 stdout -> fd/1
```

# 终端

tty 设备文件对应终端。每访问一个终端，你都会看到另一个登录提示符。每个 tty 编号（至少是 1 到 12）都与一个功能键（F# 键）相关联；如果你想转到其他终端，请按 Alt 键组合 F2、F3、F4、F5 等。当你登录 Linux 且计算机首次启动时，第一个终端（tty1）是默认终端。

```
crw-rw-rw-    1 root    tty      5,    0 Jul 17   1994 tty
crw----------    1 stripes users      4,    0 Jul 17   1994 tty0
crw-cw----    1 stripes tty      4,    1 Jun 17 10:47 tty1
crw-rw-rw-    1 root    tty      4,   10 Aug 18   1996 tty10
crw-rw-rw-    1 root    tty      4,   11 Aug 18   1996 tty11
crw-rw-rw-    1 root    tty      4,   12 Aug 18   1996 tty12
crw-rw-rw-    1 root    tty      4,   13 Aug 18   1996 tty13
crw-rw-rw-    1 root    tty      4,   14 Aug 18   1996 tty14
crw-rw-rw-    1 root    tty      4,   15 Aug 18   1996 tty15
crw-rw-rw-    1 root    tty      4,   16 Aug 18   1996 tty16
crw-rw-rw-    1 root    tty      4,   17 Aug 18   1996 tty17
crw-rw-rw-    1 root    tty      4,   18 Aug 18   1996 tty18
crw-rw-rw-    1 root    tty      4,   19 Aug 18   1996 tty19
crw-rw-rw-    1 root    root     4,    2 Jun 16 20:25 tty2
crw-rw-rw-    1 root    tty      4,   20 Aug 18   1996 tty20
crw-rw-rw-    1 root    tty      4,   21 Aug 18   1996 tty21
crw-rw-rw-    1 root    tty      4,   22 Aug 18   1996 tty22
crw-rw-rw-    1 root    tty      4,   23 Aug 18   1996 tty23
crw-rw-rw-    1 root    tty      4,   24 Aug 18   1996 tty24
crw-rw-rw-    1 root    tty      4,   25 Aug 18   1996 tty25
crw-rw-rw-    1 root    tty      4,   26 Aug 18   1996 tty26
crw-rw-rw-    1 root    tty      4,   27 Aug 18   1996 tty27
```

![](img/8ad518fddafc7f5e73715a2604b61d50_123_0.png)

你可以将 **/var/adm/messages** 和 **/var/adm/syslog** 的输出重定向到你的 *tty* 设备之一。这样做时，所使用的设备文件不再被视为终端——但你确实可以享受接收系统消息的好处，而无需总是登录为 root。

## 唯一文件

除了目录、文件和设备外，Linux 还使用其他特殊文件，如字符文件、块文件、命名管道和套接字。每种特殊类型的设备文件都有其适当的功能；例如，终端、鼠标、磁带驱动器、控制台和调制解调器的设备文件可以接受标准输入和标准输出。

*字符文件*，由单个字符标识，是通过内核访问的“原始”文件。“cooked”文件，作为“raw”文件的补充，是块文件。*块文件*可以对应特定的硬件，如软盘驱动器（例如 **/dev/fd0**）、硬盘（设备 **/dev/hda**-**h**）和 **/dev/sda**-**h**），以及内存。如果挂载了适当的设备文件，所有这些设备都可以使用。

