
**图 2.14.** 使用 SecondLook 对内存区域进行反汇编，显示注入到合法进程 (PID 32739) 中的 Jynx rootkit 关联的执行代码开头

## 调查考虑

- 如 `Phalan2` 等更高级的 rootkit 不加载其恶意内核模块，从而在不在“vmalloc”或“sysfs”下的“sys/modules”中留下任何痕迹的情况下有效地实现了其隐藏机制。上述内存取证工具中实现的方法无法检测这些基于内核模块的 rootkit。
- 在某些情况下，需要了解某个库的功能以确定其是否正常。例如，如果知道`libsol.so`提供 DNS 查询功能，那么当它被一个不需要网络访问的程序调用时，应该引起警觉。
- 如 `Phalan2` 等更高级的 rootkit 是静态编译的，不使用任何库。一方面，这使得基于加载库的分析来检测和分析变得更加困难；另一方面，没有任何库的进程是不寻常的，这可能是该进程可疑的线索。

## 打开的文件和套接

- 检查打开的文件和套接，以寻找与恶意软件相关的项，如配置文件、击键日志和网络连接。
- 每个进程访问的文件和套接可以深入了解它们在受感染系统上的运行情况。后门程序或 rootkit 可能会打开其监听端口，键盘记录器可能有一个日志文件来存储捕获的击键，而设计用于搜索磁盘中的个人身份信息 (PII) 或受保护健康信息 (PHI) 的恶意软件可能会有多个包含社会安全号、信用卡号和其他敏感数据的打开文件。

## 内存分析工具

- Volatility 中的 `linux_lsof` 插件可用于显示每个进程正在访问的文件。在图 2.15 中，列出了特定进程打开的文件，包括一个与下方所示调查相关的敏感数据文件。

```
$ python volatility/vol.py -f Phalanx2-20121031.dd linux_lsof -p 2793
<edited for length>
2793 0 /dev/pts/0
2793 1 /dev/pts/0
2793 2 /dev/pts/0
2793 3 socket:[26234]
2793 4 /usr/share/xxxxxxxxxxxxxx.xx/capture.pcap

2479 0 /dev/null
2479 1 /dev/null
2479 2 /dev/null
2479 3 socket:[21211]
2479 4 socket:[21212]
<edited for length>
```

**图 2.15**—使用 Volatility `linux_lsof` 选项解析目标内存

- 当某个打开的文件感兴趣时（例如恶意软件用于捕获用户名、密码或网络流量的文件），可以使用 `linux_find_file` Volatility 插件从内存中提取它以进行进一步检查。

为了执行此操作，必须首先获取文件的 inode 编号，然后将其内容转储到磁盘，如图 2.16 所示。

```
$ python volatility/vol.py -f Phalanx2-20121031.dd linux_find_file -F
/usr/share/xxxxxxxxxxxxxx.xx/capture.pcap"
Inode Number Inode
---------------- -----
276884 0x88001d0c1f80

$ python volatility/vol.py -f Phalanx2-20121031.dd linux_find_file -i
0x88001d0c1f80 -o output/capture.pcap
```

**图 2.16**—Volatility 插件从内存转储中提取感兴趣的文件

在许多情况下，将运行在受损系统上的进程与在网络上观察到的活动关联是非常必要的。

## Linux 系统恶意软件取证指南

- 建立这种关联的常用方法是确定每个进程使用的端口，并查找这些端口的网络活动。
- 如果内存中有与特定进程关联的打开端口或活动网络连接，可以使用 Volatility 插件提取。如图 2.17 所示，现有的内存取证无法区分正常条目和 rootkit 隐藏的条目，因此需要从活动系统获取结果进行比较。Volatility 还提供了 `linux_arp` 插件来显示 ARP 缓存。

```
$ python vol.py -f phalanx2-20121031.dd --profile=Linux linux_netstat
TCP 127.0.0.1:45842 127.0.0.1:45842 ESTABLISHED net/247
TCP 127.0.0.1:50271 127.0.0.1:45842 ESTABLISHED net/279
TCP 192.168.1.205:14901 192.168.1:59506 ESTABLISHED sshd/288
TCP 192.168.1.205:10202 192.168.1:59506 ESTABLISHED sshd/262
TCP 192.168.1.205:14901 192.168.1:59518 ESTABLISHED sshd/270
TCP 192.168.1.205:10202 192.168.1:59518 ESTABLISHED sshd/226
TCP 192.168.1.205:14901 192.168.1:49710 ESTABLISHED sshd/381
TCP 192.168.1.205:10202 192.168.1:49710 ESTABLISHED sshd/247
TCP 192.168.1.205:14901 192.168.1:52837 ESTABLISHED sshd/344
TCP 192.168.1.205:10202 192.168.1:52837 ESTABLISHED sshd/340
```

**图 2.17**—使用 `linux_netstat` 插件列出网络连接，包括被 Phalanx2 rootkit 隐藏的连接

- `linux_pkt_queues` 输出每个进程的数据包，而 `linux_sk_buff` 输出 "kmem_cache" 中 "sk_buff" 区域的数据包。

SecondLook 也可以列出打开的文件，如图 2.18 所示。此示例显示了一个“tcpdump”进程将输出保存到文件中。

| PID | 命令 | 文件描述符 | 类型 |  |

|---|---|---|---|---|

| Module text/root/mask | 2793 | tcpdump | Character | /dev/pts/0 |

| Active Files | 2793 | tcpdump | 1 | Character | /dev/pts/0 |

| Open Files | 2793 | tcpdump | 2 | Character | /dev/pts/0 |

| Memory Maps | 2793 | tcpdump | 3 | Socket |  |

| System Call Table | | | 4 | File | /usr/share/ |

| Kernel Modules | | | |  |

**图 2.18**—使用 SecondLook 解析内存转储中的打开文件（路径出于安全目的已屏蔽）

- 图 2.19 显示了 SecondLook 为图 2.17 中的 Phalanx2 rootkit 示例列出的网络连接。

## 第 2 章 Linux 内存取证

| 协议 | 源地址 | 源端口 | 目的地址 | 目的端口 |

|---|---|---|---|---|

| TCP | 0.0.0.0 | 22 | 0.0.0.0 | 0 |

| TCP | 0.0.0.0 | 111 | 0.0.0.0 | 0 |

| TCP | 127.0.0.1 | 50271 | 127.0.0.1 | 45842 |

| TCP | 127.0.0.1 | 45842 | 127.0.0.1 | 50271 |

| TCP | 127.0.0.1 | 25 | 0.0.0.0 | 0 |

| TCP | 192.168.1.205 | 22 | 192.168.1.119 | 55906 |

| TCP | 192.168.1.205 | 22 | 192.168.1.119 | 49710 |

| TCP | 192.168.1.205 | 192.168.1.119 | 5518 |

| TCP | 192.168.1.205 | 22 | 192.168.1.95 |

| TCP | 192.168.1.205 | 54901 | 192.168.1.119 | 5518 |

**图 2.19**—内存转储中被 Phalan 隐藏的连接

- 额外的连接信息可以使用提取方法从内存中恢复。例如，图 2.20 列出了由 DFR2008 参赛者从内存中提取的历史连接。

| 地址 | 源 | 目的 | 协议 |

|---|---|---|---|

| 0x08ce7b8 | 192.168.1.130:42137 | 219.93.175.67:80 | TCF |

| 0x08ff0b8 | 192.168.1.130:42137 | 219.93.175.67:80 | TCF |

| 0x0e449d8 | 192.168.1.130:56205 | 219.93.175.67:80 | TCP |

| 0x0e44c68 | 10.2.0.2:10333 | 198.105.193.114:80 | TCP |

| 0x0e54f00 | 10.2.0.2:10333 | 10.2.0.1:21 | TCF |

| 0x0e54fe48 | 10.2.0.2:10333 | 10.2.0.1:21 | TCP |

**图 2.20**—使用提取方法从 Linux 内存中恢复的网络连接

# Linux 系统恶意软件取证领域指南

- 恶意代码在计算机系统上创建的印象和痕迹证据，即使在这些制品从计算机中隐藏或删除后，也可以在内存中找到。
- 例如，与恶意软件相关的文件名、配置参数或系统日志条目在实际文件被删除或对操作系统隐藏后，可能仍然留在内存中以及相关的元数据。
- 内存取证工具正在开发中，以解释日益增加的数据结构。

> 计算机系统中存在的任何数据结构都可以在内存中找到。例如，文件系统信息通常缓存在内存中，这可能为数字调查人员提供与恶意软件及相关活动的线索。

> 当你对分析某个特定进程感兴趣时，有很多你想要寻找的内容，包括与恶意代码相关的 IP 地址、主机名、口令和加密密钥。这些信息中的部分可以通过提取字符串或执行关键字搜索找到。

# 系统详情与日志

> 在内存转储中，可能恢复从磁盘日志文件中删除的系统配置详情和“syslog”记录，这些显示了与恶意软件相关的活动。

- 使用第 3 章“关键字搜索”节描述的搜索技术，可以在内存转储中找到恶意活动的痕迹。
- 除了搜索特定关键字外，通常使用自动化方法提取信息和日志是理想的。例如，图 2.21 显示了从被 Phalanx2 rootkit 攻击系统的内存转储中提取的部分“dnsstat”信息，显示即使在删除条目从日志文件中删除后，它仍然显示了一个指向“**Xnext**”的加粗显著条目。
- 从内存转储中提取“ump”并获取连接到系统的用户列表可能是很有启发意义的。

```bash
$ python vol.py -f Phalanx220210213.dump --profile=LinuxFedora14x64 linux_dump
edited for length:
<7> 03.38382 SELinux: initialized (dev, file type, fuse) uses gens_contexts
<6> 276.103966 Program Xnext tried to access /dev/mem 0->8000000.
<6> 1468.610156 abrt-hook-ccomp[2643]: segfault at 0 0000005ebbf25df sp
000000007b6daec 0x12.90.50 (15be0000+199000)
<4> 1468.610156 Process 2643 (abrt-hook-ccomp) has LIMIT_CORE set to 1
<4> 1468.610156 Aborting core
edited for length:
```

图 2.21- 使用 volatility 从内存转储中从 dnsstat 提取的信息

> Andrew Case (2012) “Average Coder Rootkit, Bash History, and Elevated Processes,” http://volatility-labs.blogspot.com/2012/09/movp-14-average-coder-rootkit-bash.html。

# 临时文件

存储在内存驻留临时文件系统（如 RAM 磁盘、加密磁盘以及某些 Linux 系统上的“tmp”）可能包含与恶意软件事件相关的信息。虽然临时文件不会出现在被入侵系统的文件中，但它们可以从内存中恢复。可以使用 `linux_tmpfs` 插件列出所有挂载的临时系统，并使用 `-D` 提取文件内容进行进一步的取证检查，如图 2.22 所示。

```bash
% python vol.py -f Evo4Dhomeo linux_tmpfs -L
1 -> /mnt/app-cache
2 -> /mnt/obb
3 -> /mnt/abc
4 -> /mnt/sdcard

% python vol.py -f Evo4Dhomeo linux_tmpfs -S 4 -D Android/sdcard-secure
<files in /mnt/sdcard/ android_secure>
```

图 2.22- 使用 `linux_tmpfs` Volatility 插件从内存转储中提取的 Android 设备上的 tmpfs 系统

# 命令历史

- 如第 1 章所述，获取 Linux shell 中执行的命令历史可以深入了解系统上的攻击活动。作为研究人员，入侵者为了掩盖足迹可能会删除被入侵系统的命令历史文件。在这种情况下，仍然可能从内存中恢复命令历史。
- 使用 Volatility `linux_bash` 插件从内存转储中提取在给定 shell 中运行的命令历史。然而，必须通过检查相关系统的“bin/bash”二进制文件来定义内存中历史列表的偏移。当内存转储中存在多个 Bash 会话时，可以通过指定 PID 提取每个进程的命令历史。在内存中与磁盘不同，bash 历史每个命令都带有时间戳，如图 2.23 所示，日期字符串位于最后一行。

> Andrew Case (2012) “Recovering tmpfs from Memory with Volatility,” http://memoryforensics.blogspot.com/2012/08/recovering-tmpfs-from-memory-with.

# Linux 系统恶意软件取证领域指南

```bash
$ gdb /evidence/bin/bash
GNU gdb (Ubuntu-Linaro 7.4) 7.4
<edited for length>
Reading symbols from /bin/bash... (no debugging symbols found)....done.
(gdb) disassemble history_list
Dump of assembler code for history_list:
0x08ea40 mov %e,0x%abc
0x08ea45 ret
End of assembler.

$ python volatility/vol.py -f evidence/memory_dump.vmem \
--profile=Ubuntu12x86 linux_bash -H 0x812dabc

Command
ssh owned@192.168.15.6
scp valuable.tar@192.168.15.6:
sudo .bash_history
sudo shutdown -h now

user@ubuntu:~ $ date
Mon Oct 31 17:37:31 EDT
```

图 2.23— 使用 `gdb` 确定内存中历史列表的偏移（offset = 0x812dabc）并使用 Volatility `linux_bash` 插件从内存转储中提取历史

# 加密密钥与密码

恶意软件可以使用身份验证和加密机制执行深度取证分析。与常用加密方案加密密钥可以从内存转储中提取，可能允许调查人员解锁攻击者试图隐藏的信息。

- `aeskeyfind` 和 `rsakeyfind` 程序包专门用于搜索内存转储中的加密密钥。
- 另一个名为 `interrogate` 的工具可用于从内存搜索内存转储中的加密密钥，该示例支持 AES、RSA 及其。图 2.24 显示

```bash
$ interrogate -a aes -k 256 evidence/memory_dump
Interrogate Copyright (C) 2008 Maarten-Moeca <email>
This is free software, you are welcome to redistribute under certain conditions; see licence.txt

Using key size: 256 bits.
Using input file: evidence/memory_dump.
Attempting to load entire file into memory...
Success, starting search.
```

图 2.24— 使用 `interrogate` 在内存转储中搜索 AES 密钥

- `aeskeyfind` 和 `rsakeyfind` 大多数 Linux 版本可以通过相应的包管理器原生提供

# 第 2 章 Linux 内存取证

使用 `interrogate` 搜索内存转储中的加密密钥，
