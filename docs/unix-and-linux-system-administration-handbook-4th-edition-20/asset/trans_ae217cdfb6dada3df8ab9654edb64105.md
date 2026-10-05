

# KVM

迁移。表 24.2 描述了相关选项；在默认的 Xen 安装中，这些选项都是被注释的。进行更改后，运行 `/etc/init.d/xend restart` 来重启 xend。

# 表 24.2 xend 配置文件中的实时迁移选项

| 选项 | 描述 |
| --- | --- |
| xend-relocation-server | 启用迁移；设置为 yes |
| xend-relocation-port | 用于迁移活动的网络端口 |
| xend-relocation-address | 监听迁移连接的接口。若未指定，xend 将在 dom0 的所有接口上监听 |
| xend-relocation-hosts-allow | 允许连接的主机* |

- a 此处绝不应为空；否则，将允许来自所有主机的连接。

在宿主机之间迁移虚拟机的过程中，domU 的内存镜像将以未加密的形式在网络中传输。如果客户机内存中含有敏感数据，管理员应当考虑安全问题。

在尝试迁移之前，源服务器和目标服务器上都必须存在客户机的配置文件。如果主机之间的磁盘镜像位置存在差异（例如，一台服务器将共享存储挂载在 /xend，另一台挂载在 /vm），则这种差异应反映在域配置文件的磁盘参数中。

迁移非常简单：

```
redhat$ sudo xm migrate --live chef server2.example.com
```

假设我们的客户主机正在运行，该命令将它迁移到另一个 Xen 宿主机 server2.example.com。省略 `-live` 标志将在迁移前暂停主程序。我们发现，在迁移期间对 chef 的 IP 地址运行 ping 命令以观察是否有丢包是非常有意思。

# KVM

KVM（基于内核的虚拟机）是一种全虚拟化工具，自 2.6.20 版本以来已包含在 Linux 主线内核中。它依赖于当前 CPU 上的 Intel 和 AMD-V 虚拟化扩展。它是 Ubuntu 默认的虚拟化技术，Red Hat 在收购 KVM 的母公司 Qranet 后，也将重心从 Xen 切换到了 KVM。

由于 KVM 虚拟化受到 CPU 硬件的支持，因此支持许多操作系统，包括 Windows。该软件还依赖于修改版本的 QEMU 处理器模拟器。

- 4. 你的 CPU 有这些功能吗？尝试运行 `grep 'vmx|svm' /proc/cpuinfo` 来查找。如果命令没有输出，则表示不存在这些扩展。在某些系统中，必须在系统 BIOS 中启用这些扩展才能可见。

![](img/579efec8c67772f31ecf34844bbb71a2_1043_0.png)

# 第 24 章 虚拟化

在 KVM 下，Linux 内核本身作为虚拟机程序；内存管理和调度通过主机内核处理，而虚拟机是普通的 Linux 进程。这种独特的虚拟化方法带来了巨大的优势。例如，多处理器引入的复杂性由内核处理，不需要虚拟机程序即可支持它们。`top`、`ps` 和 `kill` 等 Linux 命令可以像其他进程一样显示并控制虚拟机。与 Linux 的集成是无缝的。

管理员应当注意，KVM 是一项相对年轻的技术，在推广到生产环境之前应该经过测试。KVM 网站本身记录了在运行不同操作系统因素的客户机时的许多不兼容性。不同版本 KVM 之间实时迁移崩溃的报告并不罕见。请提前做好准备。

# KVM 安装与使用

虽然 Xen 和 KVM 之间使用的技术本质上不同，但安装和管理客户操作系统的工具是相似的。在 Xen 下，你可以使用 `virt-install` 创建新的 KVM 客户机。使用 `virsh` 命令管理它们。这些实用依赖于 Red Hat 的库。

在开始安装之前，主机必须配置为支持客户机中的网络。在大多数配置中，使用一个物理接口将网络连接桥接到每个客户机。在 Red Hat 下，网络设备配置文件位于 `/etc/sysconfig/network-scripts`。需要两个设备文件：一个用于桥接，一个用于物理设备。

在下面的示例中，path0 是物理设备，eth0 是桥接：

```
/etc/sysconfig/network-scripts/path0
DEVICE=eth0
ONBOOT=yes
BRIDGE=eth0
HWADDR=XX.XX.XX.XX:XX:XX
```

```
/etc/sysconfig/network-scripts/eth0
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes
TYPE=Bridge
```

在这里，eth0 设备通过 DHCP 获取 IP 地址。

传递给 `virt-install` 的标志与用于 Xen 安装的标志略有不同。首先，`-hvm` 标志表示客户机应该是硬件虚拟化的，而不是半虚拟化的。`--connect` 参数确保选择了正确的默认虚拟机程序，因此 `virt-install` 支持多个虚拟机程序端口。最后，建议使用 `--accelerate` 以利用 KVM 的加速能力。因此，从 CD-ROM 安装 Ubuntu 服务器客户机的完整命令示例为：

```
ubuntu$ sudo virt-install --connect qemu://system -n UbuntuHardy \
512 -f /ubuntu-hardy.img -s 12 -c /dev/vdd -os-type linux
--accelerate -hvm -vnc
```

你是否想要启用图形支持？（yes 或 no）

假设已插入 Ubuntu 安装 DVD，此命令将启动安装并将结果存储在 `ubuntu-hardy.img` 中。由于我们使用了 `-vnc`，可以通过 VNC 访问。

`virsh` 工具可以管理虚拟机。要查看虚拟机列表，可以运行 `virsh --connect qemu://system list`。

| ID | 名称 | 状态 |
|---|---|---|
| 3 | UbuntuHardy | 运行 |
| 7 | Fedora | 运行 |
| | Windows203 | |

```
virsh start Windows203
Domain 已启动
```

```
virsh shutdown Fedora
Domain 正在关闭
```

```
virsh quit
```

- 5. 你可以根据意愿使用 `virsh` 管理 Xen DomUs。
- 6. 这对于 Xen 同样适用，xend 在后台执行工作。

# 24.5 SOLARIS ZONES AND CONTAINERS

Sun 在 Solaris 10 中通过引入 zones 为系统带来了操作系统级的虚拟化。广泛的在线文档和活跃的支持社区使得该技术被广泛接受。

# 第 24 章 虚拟化

Zones 和 containers 不是 Solaris 唯一的虚拟化工具。xVM 项目包含一个名为 LDOM 的虚拟机程序，以及一个用于部署大量系统的强大工具。

Zones 和 containers。

“zone”和“container”术语在很大程度上是可以互换的。从严格来说，zone 是受保护的环境，而 container 是加上资源管理的 zone。在实践中，这些术语是等同的，这也是我们在本章中使用它们的方式。

所有 Solaris 系统都有一个“global zone”，它运行内核以及系统中所有的进程，包括 zone 中的进程。nlobal zone 是与 global zone 并行的一个虚拟 Solaris 系统。nlobal zone 中的网络流量和进程对其他 zone 可见，但 global zone 可以看到所有的活动。为了安全，限制对 global zone 的访问是重要的。

resource pool 是资源集合（如处理器），可以分配给 zone。系统中至少有一个 resource pool，默认 pool，它包含了系统所有的资源。所有 zone（包括 global zone）都必须至少有一个 resource pool。

resource pool 由至少一个资源集（目前仅限于 CPU 资源的划分）和一个调度算法组成。多个 zone 可以共享同一个 resource pool，调度器将决定在使用该池的 zone 之间如何共享 CPU。

让我们通过一个具体的例子来说说明这些细节。假设一个系统运行两个虚拟 Solaris 系统：一个运行需要至少一个完整 CPU 的专用应用程序，另一个是没有特殊资源需求的轻量级 Web 服务器。图 D 显示了 Solaris 对此架构的实现。

