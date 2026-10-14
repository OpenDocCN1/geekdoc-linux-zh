

# odump -Dl /usr/sbin/caad

***LIBRARY LIST SECTION***
名称                时间戳        校验和      标志 版本
/usr/sbin/caad:
libpolicy.so        2002年1月16日 04:39:17 0x7958cdb5      0 osf.1
libbvm.so           2002年1月15日 17:37:17 0xde4a5d09      0 osf.1
libclcu.so          2002年1月15日 17:36:05 0xd148a817      0 osf.1
libm.so             2002年1月15日 17:20:50 0x07775704      0 osf.1
libpthread.so       2002年1月15日 17:26:48 0x4a2a0c94      0 osf.1
libcxx.so           2002年1月15日 17:29:14 0x9060972e      0 cxx6.3
libexc.so           2002年1月15日 17:20:58 0xb0f9a902      0 osf.1
libxc.so            2002年1月15日 17:19:09 0x1e4e245f      0 osf.1

以下命令输出列出了 Tru64 UNIX 中可用的共享库文件的位置和部分信息。

```
# ls /usr/shlib
.mrg.so_locations      libarmui.so        libmfs.so
.new.so_locations      libaud.so          libmxr.so
.proto.so_locations    libbwt.so          libnbd.so
TCR_libclcu.so         libbwt_g.so        libnet.so
X11                    libbkr.so          libnuma_g.so
null                   libbuma.so         libpacl.so
diagui_unix.uid       libc_r.so          libpota.so
ev5                    libcfrom.so        libota3.so
generic                libcfg.so          libpacl.so
libDSNLlinkAPI.so      libchf.so          libproplist.so
libbDXm.so             libclcu.so         libpset.so
libbDXterm.so          libclua.so         libpthread.so
libbDECOR.so           libcmail.so        libpthreaddebug.so
libbHelp.so            libcsa.so          libpthreada.so
libbDmail.so           libcurses.so       libpthreads.so
...
```

## 2.1.6 内存绑定

Tru64 UNIX 上大部分物理内存都是可分页的。这意味着内存页的内容可能会被分页到交换空间（磁盘上），或在系统的空闲页列表变得严重不足时被换出到交换空间。某些应用程序可能要求其内存的某些部分被视为不可分页。这种活动（称为“绑定”页面）仅限于由 root 拥有的进程。内核也可能绑定可分页页面以满足其动态内存需求。

以下示例以显示系统中绑定页面的统计信息部分结束。

![](img/a0df85c2e542a8d6c913113908553aa4_17_0.png)

## 2.1.7 非一致性内存访问（NUMA）

Tru64 UNIX 快速变化的另一个例子是包含了对非一致性内存访问（NUMA）系统的支持。传统的对称多处理（SMP）系统在添加更多处理器时扩展性不佳。Compaq（现为 HP）GS 系列计算机（GS80、GS160 和 GS320）分别可处理 8、16 和 32 个 CPU（未来会更多），并且具有出色的可扩展性。这需要专门的硬件，但

操作系统软件仍然只是好、老式的 *Tru64* UNIX。虽然有些人将 GS 系列称为“盒中集群”，但这绝对不是这些机器的意图（当然也不是我们推荐的），尽管硬件支持这种用法。

下一个序列将带你了解导致集群概念产生的计算机世界中的概念发展。在此过程中，将提及几个 *Tru64* UNIX 功能。

## 2.2 单 CPU 计算机

拆开任何一台计算机，你都会发现一些常见的硬件组件。有中央处理器（CPU），负责执行指令。它通常被认为是计算机的大脑。

有一些物理内存。内存保存正在执行的代码和 CPU 当前访问的数据。CPU 设计为执行存在于内存中的代码。如果代码仍在磁盘上，系统会抱怨（引发异常）并发生页面错误。页面错误完成后，包含出错指令的磁盘页将被调入内存并放置到页帧（物理内存）中。然后会重新执行导致错误的同一指令。

还会有一些 I/O 能力。这在不同机器之间可能差异很大，但通常包括磁盘、磁带、打印机、网络接口和其他硬件设备。

图 2-2 描述了一台具有一些物理内存和 I/O 能力的单 CPU 计算机。

本章讨论的大多数软件功能都不出现在上述硬件组件列表中。*Tru64* UNIX 和 *TruCluster* Server 主要是软件机制。负责管理硬件的软件是操作系统（在我们的例子中是 *Tru64* UNIX）。如果你想知道我们为什么带你回顾基本计算机概念，请耐心等待。我们的目标是提出实现集群所涉及的问题和难题，并确定 *TruCluster* Server 软件和组件如何解决这些问题。

第一步是考虑一个独立系统。它不允许除系统本身上运行的软件之外的任何访问其资源。在这种情况下，资源可能是内存、磁盘、其他 I/O 组件，甚至是 CPU 本身。通过使用处理模式和系统优先级级别（SPLs）来实现必要的协调和同步，以防止系统的各个组件相互干扰（或导致某种形式的损坏）。

![](img/a0df85c2e542a8d6c913113908553aa4_18_0.png)

图 2-2：计算机硬件组件

