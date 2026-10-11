
# KVM 示例

如前所述，KVM 具有出色的跨平台/跨发行版支持。在本节中，我们将查看在 Fedora Linux 发行版上的一个 KVM 实现示例。

我们将使用一组一组基于 `libvirt` C API 的工具。特别是，我们将使用虚拟机管理器 `virt-manager` 应用程序套件，它提供了用于管理虚拟机的工具。它包含了完整的 GUI 前端和命令行实用程序。

在示例中，我们将使用 `virt-install` 工具，这是一种提供简单置备虚拟机方式的 CLI 工具。它还向 GUI 应用 `virt-manager` 暴露了 API，后者利用该 API 作为其图形化虚拟机创建向导。以下是我们的宿主机系统的规格：

- 支持全虚拟化的硬件（特别是 AMD-V）
- 32GB 内存和宿主机磁盘上足够的剩余空间
- 运行 Fedora Linux 发行版的宿主机操作系统

对于我们的示例虚拟化环境，我们的目标如下：

- 使用内置的 KVM 虚拟化平台。
- 设置一个运行 Fedora Linux 发行版的客体操作系统（VM）。我们将使用 ISO 文件形式的安装介质安装 Fedora，该文件是下载并保存为宿主机系统 `/media/Fedora-Server-dvd-x86*.iso` 的文件。如果你想设置一个运行 Fedora 或某些其他 Linux 发行版的客体 VM……
- 为 VM 分配总 10GB 的磁盘空间。
- 为 VM 分配 2GB 内存。

我们将使用以下步骤来实现我们的目标：

## 1. 安装虚拟化软件包组

使用 `dnf` 安装虚拟化软件包组。该包由各种单独软件包（如 `virt-install`、`qemu-kvm` 和 `virt-manager`）组成，提供了虚拟化环境。

```
[master@fedora-server ~]$ sudo dnf -y groupinstall 'Virtualization'
```

## 2. 启动 libvirtd 服务

在启用 systemd 的发行版上，你可以启动 `libvirtd` 服务：

```
[master@fedora-server ~]$ sudo systemctl start libvirtd
```

## 3. 启用开机自启

使用 `systemctl` 工具确保 `libvirtd` 服务在系统启动时自动启动：

```
[master@fedora-server ~]$ sudo systemctl enable libvirtd
```

## 4. 验证虚拟化

使用 `virsh` 工具确保虚拟化在系统上启用并正常运行：

```
[master@fedora-server ~]$ sudo virsh list
```

只要之前的输出没有返回任何错误，我们就没问题了。

## 5. 创建存储目录

在我们的示例服务器上，我们将与每个 VM 相关的后端存储文件存储在命名为 `/home/vms` 的自定义目录路径下。

我们将开始创建存放 VM 镜像的目录：

```
[master@fedora-server ~]$ sudo mkdir -p /home/vms/
```

## 6. 创建虚拟机

使用 `virt-install` 工具设置虚拟机。`virt-install` 工具支持多个选项，你可以使用它们来自定义新 VM。运行以下命令启动 `virt-install`：

```
[master@fedora-server ~]$ sudo virt-install \
--name fedora-demo-VM --memory 2000 \
--disk /home/vms/fedora-demo-VM.qcow2,size=10 \
--cdrom /media/Fedora-Server-dvd-x86*.iso
```

此示例输出中出现 `vmx` 表示 Intel 处理器上已配备了必要的 CPU 扩展。

参数说明如下：

| 选项 | 描述 | 值 |
| :--- | :--- | :--- |
| --name | VM 的名称 | fedora-demo-VM |
| --memory | 分配给 VM 的内存（MB） | 2000 |
| --disk | 磁盘路径和大小 | /home/vms/fedora-demo-VM.qcow2,size=10 |
| --cdrom | 光驱介质路径 | /media/Fedora-Server-dvd-x86*.iso |

`/proc/cpuinfo` 伪文件系统条目提供了 Linux 系统上运行的 CPU 的详细信息。除外，该条目还显示了运行的 CPU 所支持的特殊标志或扩展。
