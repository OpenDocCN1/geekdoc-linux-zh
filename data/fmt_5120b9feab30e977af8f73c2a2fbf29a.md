
5. 并且你从第二个网站获得的链接是 `http://linuxserverexperts.com/7e/v2..ux`，你可以使用 `wget` 下载第二个文件：

```bash
[root@host ~#] wget -c -O abg-7e-vm.qcow2.tar.xz \
http://linuxserverexperts.com/7e/v2.ux
```

6. 使用 `cat` 命令合并（连接）文件：

```bash
[root@host ~#] cat file.part1 file.part2 > abg-7e-vm.qcow2.tar.xz
```

7. 解压（提取并解压缩）文件：

```bash
[root@host ~] # tar xvf abg-7e-vm.qcow2.tar.xz
```

8. 一会儿之后，你将得到一个虚拟机磁盘镜像。通过运行以下命令验证这一点：

```bash
[root@host ~] # ls -lh abg-7e-vm.qcow2
```

## 硬件与网络注意事项

运行在宿主机上的虚拟机共享主机的有限资源。对于分配给虚拟机的几乎所有组件（磁盘空间、内存、网卡、CPU、USB 端口等）都是如此。如果你的主机总容量为例如 500GB，那么为一个虚拟机分配 250GB 是不明智的。同样，如果主机有 8GB 内存，那么为一个虚拟机分配 4GB 是不明智的。在构建虚拟机并分配虚拟硬件时，你必须运用大量的常识。

不同的虚拟机程序平台以各种方式处理虚拟机网络配置。特别是 KVM 和 `libvirt` 平台支持多种处理虚拟机连接的方法。其中某些方法围绕着宿主机上桥接的概念，涉及大量的“黑魔法”。

最简单的方法是所谓的桥接网络方法。复杂度稍高的是 NAT 网络和用户模式网络（SLIRP），后者允许非特权用户运行和管理具有网络功能的虚拟机。最后是更奇特的解决方案，例如分布式以太网（YDE）。

本附录中的演示虚拟机演示使用了桥接网络，这使得虚拟机与宿主机相同的局域网具有完全的出站和入站连接。

## 导入演示虚拟机镜像并创建新的虚拟机实例

在完成所有先备工作后，我们现在可以实例化虚拟机了。我们将使用之前安装的 `virt-install` 工具。步骤如下：

### 1. 备份原始镜像

为原始/纯净的虚拟机镜像制作备份副本，以确保在需要时总有一个干净的镜像可以回溯。这些副本也可以用于启动额外的虚拟机实例，例如，当你决定为各种目的建立整个虚拟机网络时。

在 `/home/v` 目录下，运行以下命令创建原始虚拟机镜像的副本并命名为 `abg-7e-vm.qcow2.original`：

```bash
[root@host vm]# cp abg-7e-vm.qcow2 abg-7e-vm.qcow2.original
```

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

2. 使用 `virt-install` 工具导入 VM 镜像。`virt-install` 工具支持多个选项，允许你自定义新的 VM。所使用的要求/参数描述在表 B-1 中。运行以下命令导入 VM：

```bash
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

1. 在自己的交互式 shell 中启动 virsh，请输入：

```bash
[root@host ~] # virsh
virsh #
```

2. `virsh` 对其支持的不同选项和参数有一套内置帮助系统。要查看所有支持参数的快速帮助摘要，输入：

```bash
virsh # help
attach-device attach device from an XML file
attach-disk attach disk device
...<输出已截断>...
```

3. 要列出虚拟机程序上所有活跃和非活跃的域，输入：

```bash
virsh # list --all
Id Name State
-------------------------------------------------
abg-7e-vm shut off
```

输出显示 `abg-7e-vm` 客机域目前处于关闭（非活跃）状态。

4. 要查看有关 `abg-7e-vm` 客机的详细信息，输入：

```bash
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

5. 假设 `abg-7e-vm` 当前未运行，你可以通过以下命令启动它：

```bash
virsh # start abg-7e-vm
```

> 提示：你可以直接从 Linux shell（例如 Bash）运行 `virsh` 命令，而无需通过使用 `virsh` 的 `--connect` 选项进入 `virsh` 交互式 shell。要启动运行在本地虚拟机程序上的演示虚拟机，我们
> # virsh --connect qemu:///system start abg-7e-vm
> # virsh start abg-7e-vm

可以通过使用 `virsh` 使用 `--connect` 选项支持的丰富连接联合资源标识符 (URI) 来连接和管理远程主机上的虚拟机程序。
例如，要连接并管理 IP 地址为 10.0.0.88 的远程主机，你需要运行
# virsh --connect qemu+ssh://root@10.0.0.88/

```bash
virsh # shutdown abg-7e-vm
```

```bash
virsh # destroy abg-7e-vm
```

```bash
virsh # undefine g-7e-vm
```
