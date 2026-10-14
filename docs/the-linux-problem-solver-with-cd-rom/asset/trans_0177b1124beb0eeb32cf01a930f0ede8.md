

现在让我们转向 Netatalk 包的核心守护进程 atalkd，它处理基本的 AppleTalk 通信服务，例如名称查找和服务注册。atalk 的配置文件是 atalkd.conf，通常只包含接口名称，就像 Linux 以太网驱动的这个例子：

```
eth0
```

随 Netatalk 发行版提供的 atalkd.conf 文件包含一个大段注释，概述了复杂安装的选项。atalk（8）手册页详细说明了这些选项。其中最重要的是 -zone 选项，用于设置默认的 AppleTalk 区域。

## PROBLEM 40

**Symptom：** 你的更改似乎没有生效。
**Problem：** atalkd 找不到它的 atalkd.conf 配置文件。
**Fix：** 如果你不知道 atalkd 期望在哪里找到 atalkd.conf，请用以下方式启动它：

```
# atalkd -f fullpath
```

其中 fullpath 是配置文件的完整路径名，例如

```
/usr/local/etc/atalkd.conf
```

atalkd 启动需要一些时间，因此如果你把它放在启动脚本中，你应该将整个 AppleTalk 启动过程放在后台——当机器启动后不久它启动时，你不太可能错过它。

像这样启动一个测试 atalk（记得先运行 insmod appletalk.o）：

```
# atalk
# nbprgstr -p 4 hostname:Workstation
# nbprgstr -p 4 hostname:netatalk
```

其中 hostname 是你的机器名称。通过进程列表验证 atalkd 是否正在运行。如果正在运行，请尝试以下操作：

```
$ nbplkup
```

如果 atalkd 正常运行，你应该会得到类似这样的列表：

```
deskprint:LaserWriter      65280.166:128
atlantic:AFPServer          65280.166:130
atlantic: netatalk          65280.166:4
atlantic: Workstation      65280.166:4
fur: ARA - Client-Only     41201.173:2
fur: Power Macintosh      41201.173:252
fur: Workstation          41201.173:4
```

此输出来自仅有两台会说 AppleTalk 的机器的网络：atlantic 和 fur。在 fur:Workstation 这样的名称中，fur 是 nbp 对象，Workstation 是 nbp 类型。如列表所示，atlantic 是一台运行 Netatalk 的 Linux 机器，并提供文件共享服务（第二行的 AFPServer 部分就是指的这个）。它还为打印机运行 deskprint 打印机客户端。请注意，第二列中 deskprint 和 atlantic 行的点号数字是相同的。你可能会猜测 fur 是一台 Mac，因为它在倒数第二行将自己宣传为 Power Macintosh 类型。

Netatalk 提供了一个类似 ping 的实用程序 aecho，它使用 AppleTalk Echo Protocol 来查看远程主机是否存活。你可以指定远程主机为 object:type 对、object（nbp 类型默认为 Workstation）或数字。这意味着以下所有命令的作用相同：

```
$ aecho fur::Workstation
$ aecho fur
$ aecho 41201.173
```

响应与 ping 命令非常相似：

```
14 bytes from 41201.173: aep_seq=0. time=0. ms
14 bytes from 41201.173: aep_seq=1. time=0. ms
14 bytes from 41201.173: aep_seq=2. time=0. ms

--41201.173 AEP Statistics--
3 packets sent, 3 packets received, 0% packet loss
round-trip (ms)  min/avg/max = 0/0/0
```

你必须使用 CTRL-C 来中断 aecho。

## Netatalk Startup Script

Netatalk 发行版附带了一个 rc.atalk 脚本，它是编写启动脚本的良好起点。它包括 NBP 字符串初始化，以及 papd 和 afpd（AppleTalk 打印和文件服务守护进程；我们将在第 4.3.1 节和 4.3.2 节中讨论这些）。在随附的 CD-ROM 上，你还可以在 support/atalk/samba 中找到一个示例 init.d 脚本。此脚本在启动 AppleTalk 守护进程之前查找配置文件，因此你可以将其分发到多台主机。

## PROBLEM 41

Symptom：守护进程和应用程序因“Unknown service”消息而死亡。

Problem：/etc/services 中缺少行。

Fix：向 /etc/services 添加以下行：

```
rtmp     1/ddp     # Routing Table Maintenance Protocol
nbp      2/ddp     # Name Binding Protocol
echo     4/ddp     # AppleTalk Echo Protocol
zip      6/ddp     # Zone Information Protocol
```

## PROBLEM 42

Symptom：你的 AppleTalk 启动脚本花费太长，因此你的 Linux 机器启动需要很长时间。

Problem：atalkd 和相关守护进程启动花费太长时间。

Fix：使你的 AppleTalk init.d 脚本类似于以下内容（其中 netatalk 是你的安装前缀）：

```
( netatalk/atalkd ;
    netatalk/nbpstr hostname:Workstation ;
    netatalk/nbpstr hostname:netatalk ;
    netatalk/afpd ;
    netatalk/papd ) &
```

这种方法有一个小缺点：如果在机器启动时有任何打印作业被卡在 AppleTalk 打印机的队列中，打印过滤器很可能会静默地在打印作业上失败，并将它们发送到位桶，因为 atalkd 尚未启动。

相关手册页：atalkd（8），nbplkup（1），nbp_name（3）

