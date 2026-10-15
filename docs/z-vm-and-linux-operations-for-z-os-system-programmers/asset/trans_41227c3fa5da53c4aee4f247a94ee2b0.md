

## 示例 6-22 检查 Linux TCP/IP 配置

```
[root@mbase40 etc]# ifconfig -a
[...]
eth1 Link encap:Ethernet HWaddr 02:00:01:00:00:05
inet addr:172.0.0.1 Bcast:172.0.0.255 Mask:255.255.255.0
inet6 addr: fe80::200:100:5/64 Scope:Link
UP BROADCAST RUNNING MULTICAST MTU:1492 Metric:1
RX packets:0 errors:0 dropped:0 overruns:0 frame:0
TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1000
RX bytes:0 (0.0 b) TX bytes:936 (936.0 b)
[...]
```

在 z/VM 下运行 Linux 时，您可以动态地向已相应准备好的客户机添加虚拟 CPU，而无需重新 IPL。

## 设置

检查 LNXGUI 目录条目并修改其初始化参数。

### LNXGUI 目录条目

LNXGUI 目录是一个运行 ESA 架构的虚拟机，支持最多四个 CPU。在 IPL 时，客户机中定义了两个 CPU。参见示例 6-23。

### 示例 6-23 LNXGUI 目录条目的摘录

```
MACHINE ESA 4
CPU 00 BASE
CPU 01
```

### LNXGUI 初始化参数

在 Linux 端，您必须告诉内核它可以使用比 IPL 时实际检测到的更多的 CPU。这是通过在 zipl.conf 参数行中添加选项 additional_cpus 来完成的，如示例 6-24 所示。

### 示例 6-24 LNXGUI zipl.conf

```
# Modified by YaST2. Last modification on Tue May 20 19:07:54 UTC 2008
[defaultboot]
defaultmenu = menu
[...]

###Don't change this comment - YaST2 identifier: Original name: ipl###
[ipl]
    target = /boot/zipl
    image = /boot/image
    ramdisk = /boot/initrd,0x1000000
    parameters = "root=/dev/dasda1  TERM=dumb additional_cpus=2"
[...]
```

更新文件 /etc/zipl.conf 后，您必须通过运行命令 zipl 来更新引导记录以反映新配置。重新启动 Linux 使更改生效。

## 向正在运行的 Linux 客户机添加虚拟 CPU

如果客户机设置正确，您可以按如下方式向正在运行的 Linux 客户机添加 CPU：

- 1. 使用类 G 命令 DEFINE CPU 在 Linux 虚拟机中定义新的 CPU（示例 6-25）。

### 示例 6-25 在 Linux 虚拟机中定义新的虚拟 CPU

```
00: CPU 00 ID FF04DE5020978000 (BASE) CP CPUAFF ON
00: CPU 01 ID FF04DE5020978000 CP CPUAFF ON
00:
00: CP DEFINE CPU 02
00: CPU 02 defined
00:
00: CP Q CPUS
00: CPU 00 ID FF04DE5020978000 (BASE) CP CPUAFF ON
00: CPU 01 ID FF04DE5020978000 CP CPUAFF ON
00: CPU 02 ID FF04DE5020978000 CP CPUAFF ON
```

虚拟机在 IPL 时有两颗 CPU 处于活动状态，现在有三颗。Linux 客户机尚未意识到此额外 CPU 资源的可用性，如示例 6-26 所示。

### 示例 6-26 初始 CPU 配置

```
lnxguill:~ # cat /proc/cpuinfo
vendor_id : IBM/S390
# processors : 2
bogomips per cpu: 3735.55
processor 0: version = FF, identification = 04DE50, machine = 2097
processor 1: version = FF, identification = 04DE50, machine = 2097
```

- 2. 通过发出以下命令在 Linux 中激活 CPU：

```
lnxguill:~# echo 1 > /sys/devices/system/cpu/cpu2/online
```

CPU 被激活时，以下消息会列在日志文件中：

```
Jun 12 15:04:00 lnxguill kernel: cpu 2 phys_idx=2 vers=FF
ident=04DE50 machine=2097 unused=8000
```

- 3. 作为管理员，使用 cat /proc/cpuinfo 命令检查 Linux 看到的 CPU 数量，如示例 6-27 所示。

### 示例 6-27 查询 CPU 数量

```
lnxguill:~# cat /proc/cpuinfo
vendor_id      : IBM/S390
# processors    : 3
bogomips per cpu: 3735.55
processor 0: version = FF,  identification = 04DE50,  machine = 2097
processor 1: version = FF,  identification = 04DE50,  machine = 2097
processor 2: version = FF,  identification = 04DE50,  machine = 2097
```

## 性能监控和系统分析

在本章中，我们介绍 z/VM 调度概念和监控命令，并将这些命令与 z/OS 等价物联系起来。我们还介绍 z/VM 监控工具和性能调优概念。本章还讨论了与在 System z 上运行 Linux 相关的监控概念和技术。

### 目标

完成本章后，您应该能够：

- 了解 z/VM 调度概念的基础知识
- 了解与性能监控相关的 CP 命令的使用
- 描述 z/OS 命令和监控概念
- 识别 z/VM 可用的监控工具
- 讨论系统监控最佳实践

