
```
name = "chef"
uuid = "a8e20f4-d11b-d4f7-1429-7339b1d0d051"
maxmem = 512
memory = 512
vcpus = 1
bootloader = "/usr/bin/pygrub"
on_poweroff = "destroy"
on_reboot = "restart"
on_crash = "restart"
vfb = [ ]
disk = [ "tap:ao:/vm/chef.dsk,xvda,w" ]
vif = [ "mac=00:16:3e:1e:57:79,bridge=xenbr0" ]
```

有关 VNC 的更多详细信息，请参阅第 1138 页。

你可以看到网卡默认采用桥接模式。在这种情况下，虚拟块设备（VBD）是一个“块设备映射”文件，其性能优于标准的回环文件。这个可写的磁盘镜像文件以 `/dev/xvda` 的形式呈现给客户机。Xen 团队出于性能考虑推荐使用这种名为 `tap:aio` 的磁盘设备定义。

`xm` 工具非常适合日常管理虚拟机，例如启动和停止虚拟机、连接到其控制台以及查看当前状态。下面，我们先列出正在运行的客户域，然后连接到 `chef` 的控制台。ID 按客户域创建顺序递增分配，宿主机重启后会重置。

```
redhat$ sudo xm list
Name              ID  Mem(MiB)  VCPUs  State  Time(s)
Domain-0           0      2502      2  r-----     397.2
chef              19       512      1  b----      12.8
redhat$ sudo xm console 19
```

要对客户域进行自定义设置，例如挂载另一个磁盘或将网络从桥接模式改为 NAT 模式，你需要编辑 `/etc/xen` 下的客户机配置文件，然后重启客户机。`xmdomain.cfg` 的手册页详细介绍了客户域的更多选项。

### Xen 在线迁移

域迁移是将 domU 从一个物理主机移动到另一个物理主机的过程，在线迁移则不会造成任何服务中断。实际上，对于系统管理员来说，这是最便捷、最神奇的虚拟化技巧之一。开放的网络连接会一直保持，因此任何 SSH 会话或活动的 HTTP 连接都不会中断。硬件维护、操作系统升级和物理服务器重启都是使用迁移魔法的好时机。

实现迁移的一个重要要求是存储必须共享。domU 所需的任何存储（例如存放虚拟机的磁盘镜像文件）都必须能被两台宿主机访问。基于文件的虚拟机最便于在线迁移，因为它们通常包含在单个可移植文件中。但 SAN、NAS、NFS 共享或 iSCSI 单元都是系统间共享文件的可接受方法。无论 VBD 如何共享，请务必确保 domU 在同一时间只在一台物理服务器上运行。Linux 文件系统不支持多台主机直接并发访问。

此外，由于虚拟机的 IP 和 MAC 地址会随着它从一台主机迁移到另一台主机，因此每台服务器都必须位于相同的二层网络和 IP 子网中。一旦虚拟机开始通过网络发送流量，网络硬件就会学习到 MAC 地址的新位置。

满足这些基本要求后，只需对虚拟机监控程序配置文件 `/etc/xen/xend-config.sxp` 做几处配置更改，即可启用迁移。表 24.2 描述了相关选项；在默认的 Xen 安装中，这些选项都被注释掉了。修改后，运行 `/etc/init.d/xend restart` 重启 xend。

**表 24.2  xend 配置文件中的在线迁移选项**

| 选项 | 描述 |

|---|---|

| `xend-relocation-server` | 启用迁移；设为 yes |

| `xend-relocation-port` | 用于迁移活动的网络端口 |

| `xend-relocation-address` | 监听迁移连接的接口。如果未指定，Xen 将监听 dom0 中的所有接口。 |

| `xend-relocation-hosts-allow` | 允许连接的主机⁽ᵃ⁾ |

ᵃ. 此选项绝不应留空；否则，所有主机都将被允许连接。

在主机之间迁移虚拟机的过程中，domU 的内存镜像会以未加密的格式通过网络传输。如果客户机内存中包含敏感数据，管理员应牢记安全方面的考量。

在尝试迁移之前，客户机的配置文件必须同时存在于源服务器和目标服务器上。如果磁盘镜像文件的位置在两台主机上不同（例如，一台服务器将共享存储挂载到 `/xen`，另一台挂载到 `/vm`），则应在域配置文件的 `disk =` 参数中体现这一差异。

迁移本身很简单：

```
redhat$ sudo xm migrate --live chef server2.example.com
```

假设我们的客户域 `chef` 正在运行，该命令会将其迁移到另一台 Xen 主机 `server2.example.com`。省略 `--live` 标志会在迁移前暂停域。我们发现在迁移过程中对 `chef` 的 IP 地址执行 `ping` 来观察丢包情况是件很有趣的事。

### KVM

KVM（基于内核的虚拟机）是一种完全虚拟化工具，自 2.6.20 版本起就包含在 Linux 主线内核中。它依赖于当前 CPU 上提供的 Intel VT 和 AMD-V 虚拟化扩展。⁴ 它是 Ubuntu 中的默认虚拟化技术，Red Hat 在收购 KVM 的母公司 Qumranet 后，也从 Xen 转向了 KVM。

由于 KVM 虚拟化由 CPU 硬件支持，因此支持许多客户操作系统，包括 Windows。该软件还依赖于 QEMU 处理器模拟器的修改版本。

4. 你的 CPU 有这些扩展吗？试试 `egrep '(vmx|svm)' /proc/cpuinfo` 来查明。如果该命令没有输出，说明扩展不存在。在某些系统上，必须先在系统 BIOS 中启用这些扩展，它们才会可见。

在 KVM 中，Linux 内核本身就充当虚拟机监控程序（hypervisor）；内存管理和调度由宿主机内核完成，客户机就是普通的 Linux 进程。这种独特的虚拟化方式带来了巨大的好处。例如，多核处理器带来的复杂性由内核处理，无需修改 hypervisor 即可支持它们。像 `top`、`ps` 和 `kill` 这样的 Linux 命令可以显示和控制虚拟机，就像对待其他进程一样。与 Linux 的集成天衣无缝。

管理员应注意，KVM 是一项相对年轻的技术，在投入生产环境使用前应经过充分测试。KVM 网站本身也记录了运行不同操作系统类型的客户机时存在的诸多不兼容问题。KVM 不同版本之间在线迁移失败的报告也很常见。这里算是提前提醒过你了。

### KVM 的安装与使用

虽然 Xen 和 KVM 背后的技术有本质区别，但安装和管理客户操作系统的工具是相似的。与 Xen 一样，你可以使用 `virt-install` 创建新的 KVM 客户机，并使用 `virsh` 命令管理它们。[^5] 这些工具依赖于 Red Hat 的 `libvirt` 库。

安装开始之前，宿主机必须配置为支持客户机中的网络。[^6] 在大多数配置中，使用一个物理接口将网络连接桥接到每个客户机。在 Red Hat 中，网络设备配置文件位于 `/etc/sysconfig/network-scripts`。需要两个设备文件：网桥和物理设备各一个。

在下面的示例中，`peth0` 是物理设备，`eth0` 是网桥：

`/etc/sysconfig/network-scripts/peth0`

```
DEVICE=peth0
ONBOOT=yes
BRIDGE=eth0
HWADDR=XX:XX:XX:XX:XX:XX
```

`/etc/sysconfig/network-scripts/eth0`

```
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes
TYPE=Bridge
```

这里，eth0 设备通过 DHCP 获取 IP 地址。

传给 `virt-install` 的选项与 Xen 安装所用的选项略有不同。首先，`--hvm` 选项表示客户机应采用硬件虚拟化，而非半虚拟化（paravirtualized）。此外，`--connect` 参数确保选择正确的默认 hypervisor，因为 `virt-install` 支持多个 hypervisor。最后，建议使用 `--accelerate` 以利用 KVM 的加速能力。因此，从 CD-ROM 安装 Ubuntu 服务器客户机的完整命令示例如下：

```
ubuntu$ sudo virt-install --connect qemu:///system -n UbuntuHardy \
        -r 512 -f ~/ubuntu-hardy.img -s 12 -c /dev/dvd --os-type linux \
        --accelerate --hvm
```

是否启用图形支持？（yes 或 no）
