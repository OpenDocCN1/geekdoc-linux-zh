
# 806 第四部分：Mac 内存取证

### 关键点

`struct socket` 的键如下：

- `so_state`：连接状态（例如 ESTABLISHED、LISTENING）。目前仅适用于 TCP，因为它是唯一维护状态的协议。
- `so_pcb`：指向 Socket 协议控制块的不透明指针。对于 IPv4 和 IPv6 连接，其类型为 `inpcb`。

`struct protosw` 的键如下：

- `pr_domain`：Socket 域。对于 TCP 和 UDP 等常用 Socket，它是 `AF_INET`。
- `pr_protocol`：套协议，如 TCP、UDP、UNIX 或 RAW。

`struct inpcb` 结构的关键关键点是：

- `inp_dependaddr`: 连接的远程（外部）IP 地址和端口
- `inp_dependaddr`: 连接的本地 IP 地址和端口

## 文件描述符

`mac_netstat` 插件可以按进程为单位恢复网络连接。它通过继承 `mac_lsof` 来接收已分析进程的每个文件描述符。然后，它过滤类型为 `DTYPE_SOCKET` 的描述符。这些描述符被转换为 `socket` 结构并进行检查。以下显示了 10.8.3 系统上连接的 `mac_netstat` 输出：

```
$ python vol.py --profile=MacMountainLion10_8_3AMX64 -f 10.8.3x64.mem
  mac_netstat
```

| Volatility Foundation Framework 2.4 | Proto IP | 本地端口 | 远程 IP | 远程端口 | 状态 | 进程 |
|---|---|---|---|---|---|---|
| UDP | 0.0.0.0 | 137 | 0.0.0.0 | 0 | | launchd/1 |
| UDP | 0.0.0.0 | 138 | 0.0.0.0 | | | launchd/1 |
| TCP | : | 631 | : | | LISTEN | launchd/1 |
| TCP | 127.0.0.1 | 631 | 0.0.0.0 | 0 | LISTEN | launchd/1 |
| UDP | : | : | : | 0 | config/17 |
| UDP | 0 | : | : | 0 | config/17 |
| UDP | 0.0.0.0 | 58570 | 0.0.0.0 | | | syslog/19 |
| UDP | 0.0.0.0 | 5353 | 0.0.0.0 | | | mDNSResponder/34 |
| UDP | : | 5353 | : | | | mDNSResponder/34 |
| UDP | 0.0.0.0 | 49603 | : | | | mDNSResponder/34 |
| UDP | : | 49603 | : | | | mDNSResponder/34 |
| UDP | 0.0.0.0 | 53921 | 0.0.0.0 | | | mDNSResponder/34 |
| UDP | 0.0.0.0 | 123 | 0.0.0.0 | 0 | | ntpd/51 |
| UDP | fe80:1 | 123 | : | 0 | | ntpd/51 |
| UDP | 127.0.0.1 | 123 | 0.0.0.0 | 0 | | ntpd/51 |
| UDP | : | 123 | : | 0 | | ntpd/51 |
| UDP | 192.168.55.230 | : | : | 0 | | netbios/65 |
| UDP | 0.0.0.0 | 138 | 0.0.0.0 | | | |
| UDP | 0.0.0.0 | 137 | 0.0.0.0 | 0 | | netbios/65 |
| TCP | 192.168.55.230 | 49156 | 17.17.27.65 | 443 | ESTABLISHED | asd/34 |
| UDP | 0.0.0.0 | 0 | 0.0.0.0 | 0 | | location/185 |

除了连接信息外，`mac_netstat` 还会告诉你哪个进程启动了网络活动。

## 网络子系统

除了进程级 `socket` 结构外，内核还保留了记录，用于跟踪每个 `socket` 类型（TCP, UDP, IP, RAW）当前分配的网络结构。为这些协议存储的信息包括并行链表和 `inpcb` 结构的哈希表。`mac_network_conns` 插件列举这些数据结构，以恢复所有活跃的网络连接。

```
$ python vol.py --profile=MacMountain_10_8.3_AMD64 -f 10.8.3x64.vmem
  mac_network_conns
```

Volatility Foundation Volatility 2.4

| 偏移量 (V) | 协议链接 | 本地端口 | 远程 IP | 端口状态 |
|---|---|---|---|---|
| 0xffffff80305b646P | 192.168.55.230 | 49156 | 17.171.27.645 | ESTABLISHED |
| 0xffffff80305b64d8 | 127.0.0.1 | 631 | 0.0.0.0 | LISTEN |
| 0xffffff80305b8bc0 | 0.0.0.1 | 631 | 0.0.0.0 | LISTEN |
| 0xffffff80305b8c6c | 0.0.0.1 | 631 | 0.0.0.0 | |
| 0xffffff80305b8c6c | 0.0.0.1 | 631 | 0.0.0.0 | |
| 0xffffff80305b6466P | 192.168.55.230 | 49156 | 17.171.27.645 | ESTABLISHED |

这些信息仍然非常有用，因为包含了每个恢复的历史进程的名称、PID 和启动时间。

Volatility 还提供了 `mac_dead_sockets` 和 `mac_dead_inodes` 插件，可以恢复相应类型的历史信息。由于 Volatility 插件区域 API，如果在调查过程中需要其他类型的历史记录，你可以轻松编写一个插件来查找并报告这些产物。

## 从内存中恢复文件系统

正如你在学习 Windows 的 `dumpfiles` 插件（第 16 章）和 Linux 的 `linux_recover_filesystem` 插件（第 24 章）时看到的，从内存缓存中恢复文件可以极大地帮助分析。本节涵盖了用于检查和提取 Mac 系统上缓存文件的插件。在本节中，你将学习 Mac 如何在内存中缓存文件，以及你可以用来关注关键文件的策略。在第 31 章中，你将再次访问本节中的插件，以恢复许多对跟踪 Mac 系统用户活动有用的文件。

### 分析目标

你的目标如下：

- **从内存中恢复文件：** 在许多调查场景中，你只收一个内存样本，而没有相应的磁盘镜像。通过分析操作系统在内存中的文件缓存，你可以在不需要磁盘镜像的情况下恢复完整文件。
- **使用文件元数据创建时间线：** 内核会跟踪与文件相关的元数据，例如 MAC 时间、所有者和权限。这些来自内存的元数据可以帮助你创建时间线并进行关键词搜索（针对文件名）。

### 数据结构

内存中的每个文件都由一个 `vnode` 结构表示：

```
>>> dt ("vnode")
'vnode' (248 bytes)
0x0 : v_lock             ['__unnamed_14874329']
0x10 : v_freelist      ['__unnamed_14887332']
0x20 : v_mntodes       ['__unnamed_14887386']
<snip>
0x70 : v_un
```

<snip>
0xb0 : v_name                ['pointer', ['String', {'length': 256]]]
0xb8 : v_parent             ['pointer', 'vnode']
```

文件的内容存储方式取决于文件的类型：

```
>>> dt(*unnamed_14887713*)
'unnamed_14887713 (8 bytes)
0x0 : v_uinfo             ['pointer', ['fifoinfo']]
0x0 : v_mountheread       ['pointer', ['mount']]
0x0 : v_socket            ['pointer', ['socket']]
0x0 : v_specinfo          ['pointer', ['specinfo']]
0x0 : v_ucbinfo           ['pointer', ['ucb_info']]
```
