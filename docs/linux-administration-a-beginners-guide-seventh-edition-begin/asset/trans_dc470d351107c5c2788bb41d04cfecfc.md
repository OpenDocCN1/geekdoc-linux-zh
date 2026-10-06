

## 792 Linux 管理：入门指南

| 选项 | 描述 | 值(s) |
| --- | --- | --- |
| --name | 虚拟机/客机实例的名称。 | abg-7e-vm |
| --ram | 分配给 虚拟机客机的 RAM（内存），单位为 MiB。 | 2000 |
| --disk | 指定你正在导入的 VM 镜像路径，以及其他存储相关的选项。 | /home/vms/abg-7e-vm.qcow2,bus=virtio,format=qcow2. 指定 VM 镜像文件的路径、virtio 总线选项和 qcow2 格式选项）。 |
| bus | 虚拟磁盘类型 | |
| --format | 磁盘镜像格式 | vnc,listen=0.0.0.0,port=5910,password=abg |
| --graphics | 指定图形显示配置。 | （这些选项将设置一个在主机系统上监听端口 5910 端口的 VNC 服务器。连接的密码为 abg。） |

- *noreboot | 防止请求在安装或导入完成后自动重启。
- * --import | 跳过操作系统安装过程，从现有镜像导入客机。

## 表 B-1 virt-install 选项

2.  使用 `virt-install` 工具导入 VM 镜像。`virt-install` 工具支持多个选项，允许你自定义新的 VM。所使用的要求/参数描述在表 B-1 中。运行以下命令导入 VM：

```
[root@host vms] # virt-install \
--name abg-7e-vm \
--memory 2000 \
--disk /home/vms/abg-7e-vm.qcow2,bus=virtio,format=qcow2 \
--graphics vnc,listen=0.0.0.0,port=5910,password=abg \
--noreboot \
--import
```

## 管理演示虚拟机

在上一节中，我们演示了从现有镜像导入并创建新虚拟机的过程。在本节中，我们将查看一些与管理客机虚拟机相关的典型任务。

## 附录 B 演示虚拟机

我们将使用并鼓励你学习使用功能丰富的 `virsh` 程序来完成大多数任务。`virsh` 用于对虚拟客机域（机器）执行管理任务，例如关机、重启、启动和暂停客机域。

`virsh` 可以通过适当选项直接从命令行运行，也可以直接在其自己的命令解释器内部运行。它还基于 `libvirt` C 库。在下面的示例中，我们将在自己的 shell 中使用 `virsh`：

- 1. 在自己的交互式 shell 中启动 virsh，请输入：

```
[root@host ~] # virsh
virsh #
```

- 2. virsh 对其支持的不同选项和参数有一套内置帮助系统。要查看所有支持参数的快速帮助摘要，输入：

```
virsh # help
attach-device attach device from an XML file
attach-disk attach disk device
...<输出已截断>...
```

- 3. 要列出虚拟机程序上所有活跃和非活跃的域，输入：

```
virsh # list --all
Id Name State
-------------------------------------------------
abg-7e-vm shut off
```

输出显示 abg-7e-vm 客机域目前处于关闭（非活跃）状态。

- 4. 要查看有关 abg-7e-vm 客机的详细信息，输入：

```
virsh # dominfo abg-7e-vm
Id:
Name: abg-7e-vm
UUID: gbhghcf36-6a9f-4f0e-b7a4-562b793c1234
OS Type: hvm
State: shut off
CPU(s): 1
Max memory: 2048000 KiB
Used memory: 2048000 KiB
Persistent: yes
Autostart: disable
...<输出已截断>...
```

## Linux 管理：入门指南

- 5. 假设 abg-7e-vm 当前未运行，你可以通过以下命令启动它：

```
virsh # start abg-7e-vm
```

> 提示：你可以直接从 Linux shell（例如 Bash）运行 virsh 命令，而无需通过使用 virsh 的 `--connect` 选项进入 virsh 交互式 shell。要启动运行在本地虚拟机程序上的演示虚拟机，我们
> # virsh --connect qemu:///system start abg-7e-vm
> # virsh start abg-7e-vm

可以通过使用 virsh 使用 `--connect` 选项支持的丰富连接联合资源标识符 (URI) 来连接和管理远程主机上的虚拟机程序。
例如，要连接并管理 IP 地址为 10.0.0.88 的远程主机，你需要运行
# virsh --connect qemu+ssh://root@10.0.0.88/

```
virsh # shutdown abg-7e-vm
```

```
virsh # destroy abg-7e-vm
```

```
virsh # undefine g-7e-vm
```

## 连接到演示虚拟机

- * 网络计算 (VNC)
- * 虚拟 TTY 控制台

## 附录 B 演示虚拟机

- * 安全外壳 (SSH)
- * Cockpit
- 为了方便操作，我们应该提前使用：

| IP 地址 | 提示 |
| --- | --- |
| 虚拟机程序的 IP 地址 | `ifconfig` |
| 演示虚拟机的 IP 地址 | `ip` |

## 网络计算 (VNC)

VNC 是通过 5910 端口实现的。为了避免冲突，可以使用 `abg`。

许多客户端包括 TightVNC、RealVNC 以及其他。

## Linux 管理：入门指南

- 1. 在虚拟机程序上启动 Finder。
2. 在 Finder 菜单中导航到：

- 4. 在虚拟机程序上，通过 IP 地址 10.0.0.88 连接。
演示信息显示如下：

![](img/66557924397c850)

- 5. 身份验证后，将看到类似的屏幕：

![](img/66557924397c851)

要以用户身份登录系统，请在提示符输入 root。
在这里，你可以像使用物理机器一样与虚拟机交互。
- 6. 或者，如果你想以超级用户身份登录系统，请在提示符输入 root。

## 附录 B 演示虚拟机

提示：我们在地址解析协议 (ARP) 在第 11 章中提到过。ARP 提供了一种将以太网地址 (MAC 地址) 映射到 IP 地址的机制。MAC 地址应该是唯一的。

虚拟机程序会自动生成并分配 MAC 地址。

虚拟机的 MAC 地址与其他信息一起保存在 `/etc/libvirt/qemu/` 下（通常为 XML 格式）。通过结合各种命令行工具，我们可以从主机获取 IP 地址。

例如，假设你已经启动了演示虚拟机且实例名为 abg-7e-vm，你可以运行以下命令获取其 MAC 地址和当前 IP 地址：

```
# arp -an | ...
```

示例输出为 (192.168.1.202) 在 99:99:00:fe:0f:75。由此我们得知 abg-7e-vm 的 IP 地址为 192.168.1.202。

## 虚拟串口 TTY 控制台

这种连接方法是使用串口连接或端口连接设备的非常老旧方法的实现。为了实现此功能，主机或虚拟机不需要实际物理端口或设备——因为它们都是虚拟的。
这种连接方法的巧妙之处在于，你不需要提前知道演示虚拟机的 IP 地址。但是，你需要通过任何可能的方法连接并登录到主机系统。步骤如下：

- 1. 登录到主机服务器后，运行以下命令连接并启动 virsh shell：
[root@host]# virsh -c qemu:session

- 2. 在 virsh shell 中，列出任何运行中的域：
virsh # list
Id Name State
----------------------------
1 abg-7e-vm running

注意输出中 Name 列下的虚拟机名称。在我们的示例中，名称是 abg-7e-vm。

- 3. 一旦你确保演示虚拟机正在运行，查看分配给运行中的演示虚拟机的虚拟 TTY 控制台：
virsh # ttyconsole abg-7e-vm
/dev/pts/8

