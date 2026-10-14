
```
| COMMAND USER FD TYPE SIZE NODE NAME |
|---|---|---|---|---|---|---|
| gnome-session 2408 john | 15u unix 0xc3562540 | 6830 | /tmp/.ICE-unix/2408 |
| gnome-session 2408 john | 19u unix 0xc2709c0 | 7036 | /tmp/.ICE-unix/2408 |
| gnome-session 2408 john | 20u unix 0xc270940 | 7054 | /tmp/.ICE-unix/2408 |
| gnome-session 2408 john | 22u unix 0xc356c100 | 7072 | /tmp/.ICE-unix/2408 |
| gnome-session 2408 john | 23u unix 0xc3d3ac0 | 7103 | /tmp/.ICE-unix/2408 |
| gnome-session 2408 john | 24u unix 0xc183140 | 7138 | /tmp/.ICE-unix/2408 |
| gnome-session 2408 john | 25u unix 0xc690b1c | 7437 | /tmp/.ICE-unix/2408 |
```

该套接字的名称是 `gnome-session` 进程的进程 ID。通过 `lsof` 查看可以看到该文件是如何被多个进程打开的：

当使用工具查看套接字时，请注意每个套接字都有像文件一样的 `inode` 编号。这对于网络套接字和本地套接字都是如此，而且对于本地套接字更为重要，`inode` 通常是套接字的唯一标识符。考虑以下来自 `netstat` 的本地套接字输出：

```
Active UNIX domain sockets (w/o servers)

| Proto Refcnt Type State I-Node Path |
|---|---|---|---|---|---|---|
| unix | 2 | [] | DGRAM | | 3478 | @udev |
| unix | 2 | [] | DGRAM | | 5448 | @var/run/... |
| unix | 8 | [] | DGRAM | | /dev/log |
| unix | 3 | [] | STREAM | CONNECTED | 642738 |
| unix | 3 | [] | STREAM | CONNECTED | 642737 |
| unix | 2 | [] | DGRAM | | 487450 |
| unix | 2 | [] | DGRAM | | 341168 |
| unix | 3 | [] | STREAM | CONNECTED | 7633 |
| unix | 3 | [] | STREAM | CONNECTED | 7632 |
```

`lsof` 不显示属于任何进程的套接字。这些是处于套接字关闭时发生的所谓“等待状态”的 TCP 套接字。当一个进程死亡时，它的连接可能会进入 `TIME_WAIT` 状态。在这种情况下，`lsof` 将不会显示该套接字，因为它不再属于任何进程。相反，`netstat` 会显示。要查看所有 TCP 套接字，请对 `netstat` 使用 `--tcp` 选项，如下：

```
$ netstat -n --tcp

Active Internet connections (w/o servers)

Proto Recv-Q Send-Q Local Address Foreign Address State

tcp 0 127.0.0.1:60526 127.0.0.1:5000 TIME_WAIT
```

术语 `inode` 源自 UNIX 术语。它指的是保存在磁盘上的结构。每个文件都有 `inode` 编号，该编号在文件系统中是唯一的。然而，网络套接字处理方式不同。在 Linux 中，网络套接字拥有 `inode`，`lsof` 和 `netstat`（在 Linux 之外的操作系统上运行）则假装没有。

现在 `procfs` 使用的文件描述符 5 的数字与 `lsof` 相同，尽管它显示在文件名的括号内。然而，这仍然并不就能看出这就是 `inode`（索引节点），因为 `lsof` 和 `procfs` 在报告它方面都相当晦涩。为了证明这确实是 `inode`，可以使用 `stat` 命令，它是 `stat` 系统调用的封装器：

```
$ stat -L /proc/$(pgrep xinet)/fd/5

File: /proc/2838/fd/5

Size: 0 Blocks: 0 IO Block: 1024 socket

Devise: 4h/4d Inode: 28178 Links: 1

Access: (0777/srxrkrwx) UID: ( 0 / root) Gid: ( 0 / root)

Access: 1969-12-31 18:00:0000000000 -0600

Modify: 1969-12-31 18:00:0000000000 -0600

Change: 1969-12-31 18:00:0000000000 -0600
```
