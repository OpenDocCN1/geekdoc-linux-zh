
### 本系统与其他系统之间活动的 TCP 连接

`oxygen:root> netstat --inet -n`

```
Active Internet connections (w/o servers)

Proto Recv-Q Local Address Foreign Address State

tcp 0 192.168.18.1:2089 192.168.18.2:113 TIME_WAIT

tcp 0 192.168.16.1:23 192.168.18.2:1107 ESTABLISHED

tcp 0 192.168.18.1:2086 192.168.18.2:23 ESTABLISHED

tcp 0 192.168.101.2:23 192.168.16.2:1026 ESTABLISHED

tcp 1 38.29.61.100:1995 209.81.8.242:80 LAST_ACK

tcp 57 38.29.61.100:1809 207.179.18.134:22 CLOSE_WAIT
```

### 本系统上活跃的 TCP 连接以及监听连接的所有“服务器”进程
只要看看这些潜在的安全漏洞……

```bash
oxygen:root> netstat --inet -a

Active Internet connections (including servers)

Proto Recv-Q Local Address Foreign Address State

tcp 57 0 oxy.mancill.com:1809 ftp.kde.org:ftp CLOSE_WAIT

tcp 0 *:auth **: LISTEN

tcp 0 *:exec **: LISTEN

tcp 0 *:login **: LISTEN

tcp 0 *:shell **: LISTEN

tcp 0 *:telnet **: LISTEN

tcp 0 *:ftp **: LISTEN

tcp 0 *:time **: LISTEN

tcp 0 *:daytime **: LISTEN

tcp 0 *:discard **: LISTEN

tcp 0 *:sunprpc **: LISTEN

tcp 0 *:ssh **: LISTEN

tcp 0 *:printer **: LISTEN

tcp 0 *:snpp **: LISTEN

udp 0 *:bootps **

udp 0 *:791 **

udp 0 *:2049 **

udp 0 *:talk **

udp 0 *:ntalk **

udp 0 *:time **

udp 0 *:discard **

udp 0 *:sunpc **

raw 0 *:1 **

raw 0 *:1 **

raw 0 *:6 **

raw 0 *:1 **

raw 0 *:6 **
```

熟悉`lsof`等工具是为了获取一个功能更强大的`netstat`版本。它遍历内核的打开文件描述符列表，收集有关文件描述符如何使用的详细信息。如果你好奇这对你有什么用，你应该意识到`Unix`内核中的许多事物在内部都被表示为文件描述符。摘自`lsof`帮助页：

> 一个打开的文件可以是普通文件、目录、块设备文件、字符设备文件、执行的可文本引用、库、网络文件（`Internet` socket）、`NFS`文件或`Unix` socket。

许多`Unix`系统有自己的方法来获取这些信息（对于`Linux`，你可以通过遍历`/proc/pid/fd/`下的每个单独的文件描述符文件来获取），而`lsof`使用相同的开关，并在不同的变体中一致地格式化信息。它还支持将输出以脚本易于读取的格式导出，即`-F`选项。

它几乎适用于每种`Unix`变体（目前有 18 种变体，通常有两个三个版本）。它对于调试客户端-服务器问题非常有用，特别是当你无法访问源代码时。（我在`HP-UX`上用过它，因为他们的版本的`netstat`不显示 socket 另一端的端口号，只显示 IP 地址）。你如何发现什么连接到了你这里？你使用`Linux`自带的基础工具更好，但你仍然喜欢`lsof`的某些功能。

- 使用`-i`列出 socket 时，你可以通过指定特定的[主机]:端口来过滤输出。还有有限的或（OR）功能——详情请参见更多信息。
- `lsof`有重复模式（`-r`），它会迭代运行。当与`-i`配合使用时，它是监控连接启动或关闭的简单方法。
- 你可以通过`-p`（`PID`）、`-u`（`UID`）和`-g`（进程组`PGRP`）列出文件描述符。`PGRP`是所有子进程集合。只需将父进程`PID`作为`-g`的参数即可。你可能想使用`-a`选项查看由`inetd`产生的文件描述符，可以使用：

```bash
oxygen:/root# lsof -a -g $(pidof inetd)

COMMAND PID PGROUP USER FD NAME

inetd 241 241 4u 162 TCP (LISTEN)

inetd 241 241 5u 163 UDP :discard

inetd 241 241 6u 164 TCP (daytime)

inetd 241 241 7u 165 UDP :daytime

inetd 241 241 8u 166 TCP (time)

inetd 241 241 9u 167 UDP :time

inetd 241 241 10u 168 TCP (ftp)

inetd 241 241 11u 169 TCP (telnet)

inetd 241 241 12u 170 UDP :ntalk

inetd 241 241 13u 171 UDP :shell)

inetd 241 241 14u 172 TCP (login)

inetd 241 241 15u 173 TCP (exec)

inetd 241 241 16u 174 TCP (finger)

inetd 241 241 17u 175 TCP (smtp)

inetd 241 241 18u 176 TCP (finger)

inetd 241 241 19u 177 TCP (auth)
```
