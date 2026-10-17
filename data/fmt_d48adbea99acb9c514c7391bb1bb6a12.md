
```bash
$ python vol.py --profile=LinuxDebian-3_2x64 -f debian.lime linux_sof -p 8643

Volatility Foundation Volatility Framework 2.4
```

| PID | Path |
| :--- | :--- |
| 8643 | 0 /dev/pts/0 |
| 8643 | 1 /dev/pts/0 |
| 8643 | 2 /dev/pts/0 |
| 8643 | 3 /root/opt/lime-3.2.0-amd64.ko |

在此输出中，你看到文件描述符 3 (stdin)、1 (stdout) 和 2 (stderr) 被设置为伪终端，内核模块分析了 SSH 客户端打开的文件句柄：

```bash
$ python vol.py --profile=LinuxDebian-3_2x64 -f debian.lime linux_sof -p 2745

Volatility Foundation Volatility Framework 2.4
```

### 进程与进程内存

```text
2745 0 /dev/null
2745 1 /dev/null
2745 2 /dev/null
2745 3 socket:[7471]
2745 4 socket:[6607]
2745 5 pipe:[6608]
2745 6 pipe:[6608]
2745 7 /dev/ptmx
2745 9 /dev/ptmx
2745 10 /dev/ptmx
```

Secure Shell (SSH) 进程：stdin、stdout 和 stderr 文件描述符都设置为 `/dev/null`（这是应用程序的）。此外，还有编号为 7471 和 6607 的两个文件描述符。通过 `linux_netstat` 分析进程的网络连接，你会发现一个活动连接和一个未命 UNIX 套接字。

```bash
$ python vol.py --profile=LinuxDebian-3_x64 -f debian.lime linux_netstat -p 2745

Volatility Foundation Framework 2.4
```

| Protocol | Details |
| :--- | :--- |
| TCP | 192.168.174.169:22 192.168.174.1:5494 ESTABLISHED sshd/2745 |
| UNIX | 6607 sshd/2745 |

以下是名为 logkey 的 Linux 记录器文件描述符（http://code.com/p/logkeys）：

```bash
$ python vol.py --profile=LinuxDebian-3_x64 -f debian.lime linux_sof -p 2745

Volatility Foundation Volatility Framework 2.4
```

```text
2745 0 /dev/null
2745 1 /dev/null
2745 2 /dev/null
2745 3 socket:[7471]
2745 4 socket:[6607]
2745 5 pipe:[6608]
2745 6 pipe:[6608]
2745 7 /dev/ptmx
2745 9 /dev/ptmx
2745 10 /dev/ptmx
```

在此输出中，你看到文件描述符 3 (stdin)、1 (stdout) 和 2 (stderr) 被设置为用户的伪终端。内核模块分析了名为 logkey 的 Linux 记录器文件描述符（http://code.com/p/logkeys）：

```bash
$ python vol.py --profile=LinuxDebian-3_x64 -f debian.lime linux_sof -p 2745

Volatility Foundation Volatility Framework 2.4
```

```text
2745 0 /dev/null
2745 1 /dev/null
2745 2 /dev/null
2745 3 socket:[7471]
2745 4 socket:[6607]
2745 5 pipe:[6608]
2745 6 pipe:[6608]
2745 7 /dev/ptmx
2745 9 /dev/ptmx
2745 10 /dev/ptmx
```

## Bash 分析

在本章中，你学习了如何在内存中查找进程、隔离它们的地址空间并提取进程的各个区域。在这一节中，我们展示了如何利用这些能力来恢复用户、攻击者和自动化恶意样本输入 shell 的命令。

### 数据结构

以下代码显示了 `hist_entry` 的定义：

```python
>>> dt("filefile")

'hist_entry' (24 bytes)

0x0 : line ['pointer', 'String', {'length': 1024}]

0x8 : timestamp ['pointer', 'String', {'length': 1024}]

0x10 : data ['pointer', 'void']
```

### 关键点

关键点如下：

- `line`：用户输入的命令。
- `timestamp`：命令执行的时间，存储为带有井号（`#`）前缀 epoch 时间。

## Bash 历史

在正常操作期间，bash 将命令记录到用户的历史文件 (`~/.bash_history`)。攻击者显然不希望他们的命令被记录，因此你经常会遇到禁用此类日志的。有多种方法可以实现：

- 历史文件变量：取消设置 `HISTFILE` 环境变量或将其指向 `/dev/null`。
- 历史大小变量：将 `HISTSIZE` 环境变量设置为 0。
- SSH 参数：使用带有 `-T` 参数的 Linux SSH 客户端登录，以防止伪终端分配。

## Linux Bash 插件

`linux_bash` 插件从内存中恢复 `_hist_entry` 结构。特别是，它会扫描堆中作为每个时间戳前缀的 `#`（井）字符。由于这种

时间戳以字符串形式存储，然后插件会重新扫描堆，寻找指向 pound 字符的指针，这些是结构中潜在的时间戳成员。
以下输出显示了 `linux_bash` 插件针对主 bash 实例的结果（参见 http://dfws.org/2008/challenge/submission.shtml）。
该挑战侧重于攻击者从受害者组织外泄的数据：

```bash
$ python vol.py --profile=linuxdfws-profile86 -f challenge.me linux_bash -p 2585
```
