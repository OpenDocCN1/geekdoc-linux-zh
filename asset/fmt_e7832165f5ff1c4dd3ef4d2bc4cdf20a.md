
```bash
# mount -o noac /home/public /plum.public
# mount | grep plum
plum:/home/public on /plum.public type nfs4 (rw,relatime,sync,vers=4,rsize=13102,wsize=13102,namen=255,acregmin=0,acregmax=0,acdirmin=0,acdirmax=0,hard,proto=tcp,port=0,time=600,retrans=2,sec,clientaddr=172.16.192.150,minversion=0,local_lock=none,)
```

## 属性缓存

`inode`（第 515 页）存储了提供文件相关信息的属性，例如文件修改时间、大小、链接和所有者。文件本身不包含存储在文件中的数据。对于普通文件，属性通常不会频繁更改；对于目录文件，更改频率甚至更低。即使是大小属性也不会随着每次写入指令而改变：当客户端向 NFS 挂载的文件写入数据时，某些文件访问（如 `ls` 执行的访问）是额外的快速操作，此外，许多文件访问不会更改文件的属性或内容。客户端可以缓存这些属性，以避免昂贵的网络带宽消耗。

内核使用文件的修改时间来确定其缓存何时过期。如果属性缓存是在文件本身修改时间之后保存的，则缓存中的数据是当前的。服务器必须定期刷新 NFS 挂载文件的属性缓存。该周期对于普通文件和目录文件被指定为最小和最大秒数。以下是影响属性缓存的选项列表：

- `ac` (`noac`)（属性缓存）允许属性缓存。`noac` 选项禁用属性缓存。虽然 `noac` 会减慢服务器速度，但它可以避免当两个客户端活动写入公共目录层次结构时出现过时属性的问题。上一节的示例显示，当你指定 `noac` 时，`mount` 将以下每个选项都设置为 0，效果是属性不会被缓存。默认值为 `ac`。
- `acdirmax=n`（属性缓存目录文件最大值）`n` 是 NFS 在刷新目录文件属性之前等待的最大秒数。默认值为 60 秒。
- `acdirmin=n`（属性缓存目录文件最小值）`n` 是 NFS 在刷新目录文件属性之前等待的最小秒数。默认值为 30 秒。
- `acregmax=n`（属性缓存文件最大值）`n` 是 NFS 在刷新普通文件属性之前等待的最大秒数。默认值为 60 秒。
- `acregmin=n`（属性缓存文件最小值）`n` 是 NFS 在刷新普通文件属性之前等待的最小秒数。默认值为 30 秒。
- `actime=n`（属性缓存超时）将 `acregmin`、`acregmax`、`acdirmin` 和 `acdirmax` 设置为 `n` 秒。如果没有此选项，每个单独选项将采用其分配或默认的值。

## 错误处理

以下选项控制当服务器未响应或发生 I/O 错误时 NFS 的行为。为了允许位于挂载设备上的挂载点，挂载点被视为超时。

- `fg`（前台）：如果前台挂载失败，则以错误状态退出。`bg`（后台）选项会在后台重试失败的 NFS 挂载尝试。默认值为 `fg`。
- `hard` (`soft`)：使用 `soft` 选项时，当 NFS 请求超时，NFS 将无限重试。使用 `soft` 选项时，NFS 将重连并向调用程序报告 I/O 错误。通常情况下不建议使用 `soft`。挂载页面显示“通常会引起很多麻烦”。更多信息请参阅第 800 页的“提高性能”。
- `retrans=n`（重传值）：NFS 在 `n` 次超时后会生成“未响应”的消息。如果设置了 `hard` 且失败，NFS 在 `n` 次超时后继续。默认值为 3。
- `retry`（重试值）：NFS 在放弃之前重试挂载操作的分钟数。设置为 0 则在失败时立即退出。前台挂载（`fg`）默认为 2 分钟；后台挂载（`bg`）默认为 10 分钟。
- `timeout=n`（超时值）：`n` 是 NFS 在重传之前等待的秒数。对于基于 TCP 的 NFS，默认值为 60。在繁忙的网络中或请求通过路由器时，增加此值可能会提高性能。参见下一页的“超时”。

## 杂项选项

以下是一些实用的选项：

- `lock` (`nolock`)：允许锁定。`nolock` 禁用锁定。
- `nfsvers=n`：`n` 指定 NFS 版本。
- `port=n`：`n` 指定 NFS 端口。
- `rsize=n`（read）：`n` 是 NFS 读取时允许的最大读取字节数。
- `wsize=n`（write）：`n` 是 NFS 写入时允许的最大字节数。
- `udp`：使用 UDP。
- `tcp`：使用 TCP。

## 提高性能

- `hard`/`soft`：多个参数会影响性能，特别是在连接较慢时，使用 `hard`（第 799 页）可能会导致执行。
- Block size：提高性能的最简单方法是更改块大小，即 `rsize` 和 `wsize`，实验直到找到最佳块大小。访问 `nfs.sourceforge.org/net-nfs` 获取相关信息。
- Timeouts：NFS 等待 `timeo`（第 799 页）指定的时间响应。如果在此时间内没有收到响应，NFS 将发送另一个传输。在慢连接的情况下，第二次传输可能会降低速度。你可能通过增加 `timeo` 来提高性能。

你可以使用 `ping -s (size)` 选项测试连接的数据包大小：

```bash
$ ping -s 4096 plum
PING plum (172.16.192.151) 4096(124) bytes of data.
4104 bytes from (172.16.192.151): icmp_req=1 ttl=64 time=0.469 ms
4104 bytes from (172.16.192.151): icmp_req=2 ttl=64 time=0.540 ms
4104 bytes from (172.16.192.151): icmp_req=3 ttl=64 time=0.459 ms
4104 bytes from (172.16.192.151): icmp_req=4 ttl=64 time=0.520 ms
...
4104 bytes from (172.16.192.151): icmp_req=26 ttl=64 time=0.501 ms
--- plum ping statistics
26 packets transmitted, 26 received, 0% packet loss, time 25014ms
rtt min/avg/max/mdev = 0.443/0.506/0.550/0.032 ms
```

## 设置 NFS 服务器

预计需要几秒钟。如果连接正在处理其他流量，时间将更长。请在流量高峰期运行测试。尝试将超时时间增加到往返时间的三倍或四倍（以允许异常糟糕的网络状况，例如建立连接时），并查看性能是否提高。请记住，超时值是以秒分之一为单位的（100 毫秒 = 十分之一秒秒）。

## /etc/fstab：自动挂载目录层次结构

`/etc/fstab` 文件（第 524 页）列出了系统在启动时可能自动挂载的目录层次结构。您可以在命令行或 `fstab` 文件中使用前面节中讨论的选项。

`guava` 中 `fstab` 文件中的以下行将 `plum` 的 `/home/public` 目录挂载到本地的 `/plum.public` 挂载点上：

```
plum:/home/public /plum.public nfs rsize=8192,wsize=8192 0 0
```

挂载点应该是空的本地目录。（当目录层次结构挂载到挂载点上时，挂载点中的文件将被隐藏）。使用 NFS 挂载的文件系统类型为 `n4`，无论其在本地系统上的类型如何。您可以增加 `rsize` 和 `wsize` 选项以提高性能。请参阅第 800 页的“提高性能”。

`fstab` 文件的下一个示例挂载了 `dog` 的文件系统：

```
dog:/export /dog.export nfs4 timeout=50,hard 0 0
```

由于本地系统通过慢速连接到 `dog`，因此超时时间增加到 5 秒（50 秒分之一）。请参阅第 800 页的“超时”。此外，设置 `hard` 是为了确保 NFS 在发生严重超时后继续与服务器通信。请参阅第 800 页的“hard/soft”。

`fstab` 文件的最后一个示例显示了远程挂载的家目录。由于 `dog` 是本地服务器，且通过可靠的高速连接连接，因此超时时间缩短了，并大幅增加了了 `rsize` 和 `wsize`：

```
dog:/home /dog.home nfs4 timeout=4,rsize=16384,wsize=16384 0 0
```

### 前提条件

安装以下软件包：

- `nfs-utils`
- `rpcbind`（随 `nfs-utils` 安装）
- `system-config-nfs`（Fedora；可选）

`rpcbind`：在启动 `nfsd` 守护进程之前，必须运行 `rpcbind` 守护进程。
