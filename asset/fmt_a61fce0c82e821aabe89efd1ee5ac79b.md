
在 AMD 平台上，显示支持全虚拟化的标志是 `svm`。要检查 AMD 处理器是否支持 `svm`，可以查看 `/proc/cpuinfo`：

```
[root@amd-server ~] grep "svm" /proc/cpuinfo

flags : fvm vme pse ... (省略) ... svm ...
```

# KVM 示例

如前所述，KVM 具有出色的跨平台/发行版支持。在本节中，我们将查看 Fedora 发行版上的 KVM 实现。

我们将使用基于 `libvirt` 库的一系列工具。特别是，我们将使用虚拟机管理器 `virt-manager` 工具包，它提供了管理虚拟机的工具。它包含图形界面和命令行界面。

在示例中，我们将使用 `virt-install` 工具，这是一个提供创建虚拟机简便方式的命令行工具。它还为 `virt-manager` 暴露了 API。

以下是示例主机的规格：

- 硬件支持全虚拟化（特别是 AMD-V）
- 32GB 内存
- 主机操作系统上有足够的剩余空间
- 主机运行 Fedora 发行版

我们的示例虚拟化环境目标如下：

使用内置的 KVM 虚拟化平台。
- 安装一个运行 Fedora 发行版的操作系统（虚拟机）。我们将使用下载并保存到主机系统 `/media/Fedora-Server-DVD-x86_64.iso` 的 ISO 镜像来安装 Fedora。如果你想设置运行 Fedora 或其他 Linux 发行版的虚拟机，请将此处使用的示例 ISO 文件名替换为你拥有的真实 ISO 文件名。
- 为虚拟机分配总计 10GB 的磁盘空间。
- 为虚拟机分配 2GB 内存。

# 742 Linux 管理：入门指南

我们将使用以下步骤来实现我们的目标：

- 1. 使用 `dnf` 安装虚拟化包组。该包组包含了各种单独软件包（例如 `virt-install`、`qemu-kvm` 和 `virt-manager`），它们提供了虚拟化环境。输入：
```bash
[root@fedora-server ~]# dnf -y groupinstall 'Virtualization'
```

- 2. 在 Fedora、Debian、Ubuntu 等启用了 `systemd` 的发行版上，使用 `systemctl` 工具如下启动 `libvird` 服务：
```bash
[root@fedora-server ~]# systemctl start libvird
```

- 3. 在使用 `systemd` 作为服务器的 Linux 发行版上，使用 `systemctl` 工具确保 `libvird` 服务在下次系统启动时自动启动：
```bash
[root@fedora-server ~]# systemctl enable libvird.service
```

- 4. 使用 `virsh` 工具确保虚拟化在系统上正常运行：
```bash
[root@fedora-server ~]# virsh list

Id    Name                 State
```

只要前面的输出没有返回任何错误，我们就没问题。

- 5. 在我们的示例服务器上，我们将所有与每个虚拟机（VM）相关的后端存储文件存储在自定义目录路径 `/home/vms` 下。
我们将首先创建存放 VM 镜像的目录结构：
```bash
[root@fedora-server ~]# mkdir -p /home/vms/
```

- 6. 使用 `virt-install` 工具设置虚拟机。`virt-install` 工具支持多个选项，允许您在安装时自定义虚拟机。运行以下命令启动 `virt-install`：
```bash
[root@fedora-server ~]# virt-install \
  --name fedora-demo-VM --memory 2000 \
  --disk /home/vms/fedora-demo-VM.qcow2,size=10 \
  --cdrom /media/Fedora-Server-DVD-x86_64*.iso
```

上述参数的含义在此处解释。

| 选项 | 描述 | 值 |
|---|---|---|
| --name | 虚拟机/客户机的名称 | fedora-demo-VM |
| --memory | 分配给虚拟机客户机的内存 | 2000 mebibytes (MiB) |
| --disk | 指定虚拟机文件/设备所需的路径及其他存储相关选项。如果未指定路径或名称，将使用默认存储池路径：/var/lib/libvirt/images/。由于您未指定名称，磁盘将自动命名为与虚拟机类似的名称。 | /home/vms/fedora-demo-VM.qcow2,size=10 (我们在这里指定了 10GB 的存储大小选项) |
| --cdrom | 作为虚拟 CD-ROM 设备的文件或设备。 | /media/Fedora-Server-DVD-x86_64*.iso |

**注意** 尽管您可以使用连接到主机的物理驱动器进行操作系统安装，但直接使用原始版本的 ISO 镜像文件来安装和维护虚拟机客户机更加方便。这样，您就不需要每次重新加载 Linux 发行版新版本时都去创建 CD、DVD 或驱动器。如果您需要使用插入物理光驱驱动器的 CD/DVD 介质，只需将命令行工具或 GUI KVM 管理器指向相应的设备文件即可。
例如，您可以提供代表第一个光驱驱动器的设备路径，例如 `/dev/sdb`——当然，前提是您已经准备并将操作系统构建到空白 CD/DVD-ROM 磁盘上并将其插入主机系统。

- 7. 新配置的虚拟机应该立即在 Virt Viewer 中启动。虚拟机将尝试安装 `--cdrom` 选项值所引的光驱中的介质。将弹出一个类似于所示的窗口：

![](img/9f6657924397c33f088db5321b751a83_756_0.png)

从这里开始，您可以像在普通机器上安装一样继续安装（见第 2 章）。就是这样！

> **提示** `virt-install` 命令提供了丰富的选项。您绝对应该花几分钟看一眼它的手册（`man virt-install`）。例如，它拥有 `--os-variant` 等选项，允许您开箱即为不同的客户操作系统平台（如 Windows、Unix、Linux、UNIX 等）优化配置。

# 管理 KVM 虚拟机

在上一节中，我们学习了虚拟机的安装和配置。在本节中，我们将查看与管理客户虚拟机相关的某些任务。

我们将使用功能丰富的 `virsh` 程序来完成大多数任务。`virsh` 用于对虚拟域（机器）执行管理任务，如关闭、重启、启动和暂停客户域。`virsh` 也基于 `libvirt` C 语言。

`virsh` 可以使用适当的选项直接从命令行运行，也可以直接在其自己的命令解释器内部运行。在接下来的示例中，我们将在其内部 shell 使用 `virsh`。

- 1. 要在其最小交互式 shell 中启动 `virsh`，请输入以下内容：
```bash
[root@fedora-server ~]# virsh

virsh #
```

- 2. `virsh` 针对不同的选项和参数有一套内置的系统。要查看它支持的所有参数快速摘要，输入：
```bash
[root@fedora-server ~]# virsh

virsh # help

attach-device      XML file

attach-disk        attach device

list              list domains

...（省略）...
```

- 3. 要列出宿主机上已配置和激活的域，输入：
```bash
[root@fedora-server ~]# virsh list --all

Id Name             State

fedora-demo-VM     shut off
```

- 4. 查看有关 `fedora-demo-VM` 域的详细信息：
```bash
[root@fedora-server ~]# virsh dominfo fedora-demo-VM

Id: fedora-demo-VM

UUID: dbbd3c-6a9f-4f0e-b7a4-562b7342097

OS Type: hvm

State: shut off

CPU(s): 1

Max memory: 204800 KiB

Used memory: 0 KiB

Persistent: yes

Autostart: disable
```

- 5. 假设 `fedora-demo-VM` 虚拟机未运行，可以通过以下命令启动它：
```bash
virsh # start fedora-demo-VM
```

- 6. 使用 `shutdown` 参数关闭 `fedora-demo-VM` 虚拟机：
```bash
virsh # shutdown fedora-demo-VM
```
